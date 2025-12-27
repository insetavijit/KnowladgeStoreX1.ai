## 1. Project Definition & Requirements

### 1.1 Core Objectives

- **Normalize Markdown structure**: Standardize heading levels, list formatting, and spacing
- **Clean whitespace**: Remove empty lines, trailing spaces, and inconsistent indentation
- **Preserve content integrity**: Maintain semantic meaning, code blocks, inline code, and YAML frontmatter
- **Ensure idempotency**: Running the agent multiple times on the same file produces identical results

### 1.2 Success Criteria

- Zero semantic changes to content
- 100% preservation of code blocks and frontmatter
- Measurable improvement in structure consistency
- Safe rollback capability via backups
- Performance: Process 100KB file in under 30 seconds

### 1.3 Non-Goals

- Grammar correction or content enhancement
- Translation or language detection
- Image processing or link validation

## 2. Technology Stack Selection

### 2.1 Core Framework: LangGraph

LangGraph is a low-level orchestration framework for building stateful, long-running workflows and agents, providing durable execution, human-in-the-loop capabilities, and comprehensive memory management.

**Why LangGraph?**

- Built-in state management tracks information throughout the workflow
- Supports conditional branching for error handling
- Provides debugging capabilities with LangSmith integration for tracing execution paths and capturing state transitions
- Enables cyclical graph patterns for retry logic

**Installation**:

```bash
pip install langgraph==1.0.4
```

### 2.2 LLM Selection: Hugging Face Models

**Recommended Models** (based on current performance benchmarks):

1. **Primary Choice**: `meta-llama/Meta-Llama-3-8B-Instruct`
    
    - Strong instruction-following capability
    - Rivals proprietary models when fine-tuned for specific tasks
    - Suitable for 24GB+ GPUs
2. **Alternative**: `mistralai/Mistral-7B-Instruct-v0.2`
    
    - Efficient for resource-constrained environments
    - Good balance of performance and speed
3. **Lightweight Option**: `google/gemma-7b-it`
    
    - Optimized for deployment in resource-constrained environments with 7B parameters, featuring 28 layers and extended context length of 8,000 tokens

**Model Requirements**:

- Instruction-tuned variant (not base model)
- Context window: 4K+ tokens
- Support for system prompts

---

## 3. Environment Setup

### 3.1 Project Structure

```
markdown-restructure-agent/
├── .env                    # Environment variables
├── .gitignore             # Git ignore patterns
├── README.md              # Project documentation
├── requirements.txt       # Python dependencies
├── config/
│   └── model_config.yaml  # Model and runtime configuration
├── src/
│   ├── __init__.py
│   ├── agent/
│   │   ├── __init__.py
│   │   ├── graph.py       # LangGraph workflow definition
│   │   ├── nodes.py       # Individual node implementations
│   │   └── state.py       # State schema definition
│   ├── models/
│   │   ├── __init__.py
│   │   └── llm.py         # Model loading and inference
│   ├── utils/
│   │   ├── __init__.py
│   │   ├── file_ops.py    # File I/O operations
│   │   ├── validation.py  # Pre/post validation
│   │   └── diff.py        # Content comparison
│   └── cli.py             # Command-line interface
├── tests/
│   ├── __init__.py
│   ├── fixtures/          # Test Markdown files
│   └── test_agent.py      # Unit and integration tests
└── examples/
    └── sample_files/      # Example input files
```

### 3.2 Virtual Environment & Dependencies

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install --upgrade pip
pip install -r requirements.txt
```

**requirements.txt**:

```
langgraph==1.0.4
transformers==4.36.0
torch>=2.1.0
accelerate>=0.25.0
bitsandbytes>=0.41.0  # For 4-bit quantization
pyyaml>=6.0
click>=8.1.0
python-dotenv>=1.0.0
difflib  # Standard library, no version needed
pytest>=7.4.0
```

### 3.3 Model Access Configuration

**Local Model Setup**:

```python
# src/models/llm.py
from transformers import AutoTokenizer, AutoModelForCausalLM, BitsAndBytesConfig
import torch

def load_model(model_id="meta-llama/Meta-Llama-3-8B-Instruct", use_4bit=True):
    """Load instruction-tuned model with optional quantization."""
    
    quantization_config = None
    if use_4bit:
        quantization_config = BitsAndBytesConfig(
            load_in_4bit=True,
            bnb_4bit_quant_type="nf4",
            bnb_4bit_compute_dtype=torch.float16,
            bnb_4bit_use_double_quant=True,
        )
    
    tokenizer = AutoTokenizer.from_pretrained(model_id)
    model = AutoModelForCausalLM.from_pretrained(
        model_id,
        quantization_config=quantization_config,
        device_map="auto",
        trust_remote_code=True,
    )
    
    return model, tokenizer
```

**Hugging Face Token** (for gated models):

```bash
# .env file
HF_TOKEN="your_hugging_face_token_here"
```

---

## 4. Agent State Design

### 4.1 State Schema

```python
# src/agent/state.py
from typing import TypedDict, Optional, List
from datetime import datetime

class AgentState(TypedDict):
    """Tracks the complete state throughout the workflow."""
    
    # File tracking
    file_path: str
    original_content: str
    processed_content: Optional[str]
    
    # Processing metadata
    status: str  # 'pending', 'processing', 'success', 'failed', 'skipped'
    current_node: str
    processing_start: datetime
    
    # Validation results
    has_frontmatter: bool
    has_code_blocks: bool
    validation_errors: List[str]
    
    # Diff tracking
    changes_detected: bool
    diff_summary: Optional[str]
    
    # Error handling
    error_message: Optional[str]
    retry_count: int
    
    # Output control
    backup_path: Optional[str]
    dry_run: bool
```

### 4.2 State Update Patterns

LangGraph supports two state update modes:

1. **Override**: Completely replace a value

```python
return {"status": "processing"}
```

2. **Append**: Add to existing list values

```python
return {"validation_errors": ["New error"]}  # Appends to list
```

---

## 5. Graph Node Implementation

### 5.1 Node Architecture Overview

In LangGraph, nodes represent individual components that interact in a specific workflow sequence. Our workflow includes:

```
START → discover_files → load_file → pre_validate 
    → llm_restructure → post_validate → check_diff 
    → persist_results → generate_report → END
```

### 5.2 Node: File Discovery

```python
# src/agent/nodes.py
import os
from pathlib import Path
from typing import List

def discover_files(state: AgentState) -> AgentState:
    """Discover Markdown files in the specified path."""
    
    path = state["file_path"]
    markdown_files = []
    
    if os.path.isfile(path):
        if path.endswith(('.md', '.markdown')):
            markdown_files.append(path)
    elif os.path.isdir(path):
        for root, _, files in os.walk(path):
            for file in files:
                if file.endswith(('.md', '.markdown')):
                    markdown_files.append(os.path.join(root, file))
    
    return {
        "discovered_files": markdown_files,
        "status": "discovered" if markdown_files else "no_files",
        "current_node": "discover_files"
    }
```

### 5.3 Node: File Loading

```python
def load_file(state: AgentState) -> AgentState:
    """Load file content with error handling."""
    
    try:
        with open(state["file_path"], 'r', encoding='utf-8') as f:
            content = f.read()
        
        return {
            "original_content": content,
            "status": "loaded",
            "current_node": "load_file"
        }
    except Exception as e:
        return {
            "status": "failed",
            "error_message": f"File loading error: {str(e)}",
            "current_node": "load_file"
        }
```

### 5.4 Node: Pre-validation

```python
import re

def pre_validate(state: AgentState) -> AgentState:
    """Validate file structure before processing."""
    
    content = state["original_content"]
    errors = []
    
    # Check for frontmatter
    has_frontmatter = content.startswith('---')
    
    # Detect code blocks
    code_block_pattern = r'```[\s\S]*?```'
    has_code_blocks = bool(re.search(code_block_pattern, content))
    
    # Validate Markdown syntax
    if not content.strip():
        errors.append("File is empty")
    
    # Check for basic Markdown elements
    if not re.search(r'^#+\s', content, re.MULTILINE):
        errors.append("No headings found - may not be valid Markdown")
    
    return {
        "has_frontmatter": has_frontmatter,
        "has_code_blocks": has_code_blocks,
        "validation_errors": errors,
        "status": "validated" if not errors else "validation_failed",
        "current_node": "pre_validate"
    }
```

### 5.5 Node: LLM Restructuring (Core)

````python
from transformers import AutoTokenizer, AutoModelForCausalLM

def llm_restructure(state: AgentState) -> AgentState:
    """Use LLM to restructure Markdown content."""
    
    # Load model (cache in production)
    model, tokenizer = load_model()
    
    # Construct prompt
    system_prompt = """You are a Markdown formatting expert. Your ONLY task is to normalize the structure of Markdown documents.

RULES:
1. NEVER change the semantic meaning or content
2. PRESERVE all code blocks exactly as-is (including language identifiers)
3. PRESERVE YAML frontmatter exactly as-is
4. PRESERVE inline code and links
5. Remove empty lines between paragraphs (use single line break)
6. Remove trailing spaces
7. Normalize heading hierarchy (ensure proper nesting)
8. Standardize list formatting (consistent indentation)
9. Output ONLY the restructured Markdown - no explanations

If you cannot safely restructure without changing meaning, output the original unchanged."""

    user_prompt = f"""Restructure this Markdown file:

```markdown
{state['original_content']}
````

Output the restructured Markdown:"""

```
# Generate with chat template
messages = [
    {"role": "system", "content": system_prompt},
    {"role": "user", "content": user_prompt}
]

inputs = tokenizer.apply_chat_template(
    messages, 
    return_tensors="pt",
    add_generation_prompt=True
).to(model.device)

# Generate with constraints
outputs = model.generate(
    inputs,
    max_new_tokens=8192,
    temperature=0.1,  # Low temperature for deterministic output
    do_sample=False,
    pad_token_id=tokenizer.eos_token_id
)

processed_content = tokenizer.decode(outputs[0], skip_special_tokens=True)

# Extract only the Markdown portion (remove prompt echo)
processed_content = extract_markdown_response(processed_content)

return {
    "processed_content": processed_content,
    "status": "processed",
    "current_node": "llm_restructure"
}
```

def extract_markdown_response(full_response: str) -> str: """Extract just the Markdown content from model response.""" # Remove system/user prompt echo if "`markdown" in full_response: match = re.search(r'`markdown\n(.*?)```', full_response, re.DOTALL) if match: return match.group(1).strip()

```
# Fallback: take content after last prompt marker
lines = full_response.split('\n')
start_idx = 0
for i, line in enumerate(lines):
    if line.startswith('---') or line.startswith('#'):
        start_idx = i
        break

return '\n'.join(lines[start_idx:]).strip()
```

````

### 5.6 Node: Post-validation

```python
def post_validate(state: AgentState) -> AgentState:
    """Validate processed content maintains critical elements."""
    
    original = state["original_content"]
    processed = state["processed_content"]
    errors = []
    
    # Check frontmatter preservation
    if state["has_frontmatter"]:
        if not processed.startswith('---'):
            errors.append("Frontmatter was removed or corrupted")
    
    # Check code block count
    if state["has_code_blocks"]:
        original_blocks = len(re.findall(r'```', original))
        processed_blocks = len(re.findall(r'```', processed))
        if original_blocks != processed_blocks:
            errors.append(f"Code block count mismatch: {original_blocks} → {processed_blocks}")
    
    # Check heading structure
    original_headings = re.findall(r'^#+\s.*$', original, re.MULTILINE)
    processed_headings = re.findall(r'^#+\s.*$', processed, re.MULTILINE)
    if len(original_headings) != len(processed_headings):
        errors.append("Heading count changed - possible content loss")
    
    return {
        "validation_errors": errors,
        "status": "post_validated" if not errors else "validation_failed",
        "current_node": "post_validate"
    }
````

### 5.7 Node: Diff Check

```python
import difflib

def check_diff(state: AgentState) -> AgentState:
    """Generate and analyze differences."""
    
    original = state["original_content"]
    processed = state["processed_content"]
    
    # Generate unified diff
    diff = difflib.unified_diff(
        original.splitlines(keepends=True),
        processed.splitlines(keepends=True),
        fromfile='original',
        tofile='processed',
        lineterm=''
    )
    
    diff_text = ''.join(diff)
    changes_detected = bool(diff_text.strip())
    
    # Generate summary
    stats = {
        'lines_added': diff_text.count('\n+'),
        'lines_removed': diff_text.count('\n-'),
        'total_changes': diff_text.count('\n+') + diff_text.count('\n-')
    }
    
    summary = f"Changes: +{stats['lines_added']} -{stats['lines_removed']}"
    
    return {
        "changes_detected": changes_detected,
        "diff_summary": summary,
        "diff_content": diff_text,
        "status": "diff_complete",
        "current_node": "check_diff"
    }
```

### 5.8 Node: Persist Results

```python
import shutil
from datetime import datetime

def persist_results(state: AgentState) -> AgentState:
    """Save processed content with backup."""
    
    if state["dry_run"]:
        return {
            "status": "dry_run_complete",
            "current_node": "persist_results"
        }
    
    file_path = state["file_path"]
    
    # Create backup
    timestamp = datetime.now().strftime('%Y%m%d_%H%M%S')
    backup_path = f"{file_path}.backup_{timestamp}"
    shutil.copy2(file_path, backup_path)
    
    # Write processed content
    try:
        with open(file_path, 'w', encoding='utf-8') as f:
            f.write(state["processed_content"])
        
        return {
            "backup_path": backup_path,
            "status": "persisted",
            "current_node": "persist_results"
        }
    except Exception as e:
        # Restore from backup
        shutil.copy2(backup_path, file_path)
        return {
            "status": "failed",
            "error_message": f"Persist error: {str(e)}",
            "current_node": "persist_results"
        }
```

---

## 6. LLM Prompt Engineering

### 6.1 Prompt Design Principles

**Critical Requirements**:

1. **Specificity**: Explicitly forbid content changes
2. **Preservation directives**: List all elements to preserve
3. **Output format**: Request raw Markdown only
4. **Error handling**: Instruct to return original if uncertain

### 6.2 Production Prompt Template

```python
SYSTEM_PROMPT = """You are a Markdown formatting specialist. Your task is to normalize document structure while preserving all content.

STRICT RULES:
✓ DO normalize whitespace and formatting
✓ DO standardize heading hierarchy
✓ DO fix list indentation

✗ DO NOT change wording or meaning
✗ DO NOT modify code blocks or inline code
✗ DO NOT alter YAML frontmatter
✗ DO NOT remove or add content

PRESERVATION REQUIREMENTS:
- YAML frontmatter (between --- delimiters)
- Code blocks (``` fenced blocks with language identifiers)
- Inline code (`backticks`)
- Links [text](url)
- Images ![alt](url)
- HTML comments <!-- -->

OUTPUT FORMAT:
Return ONLY the restructured Markdown. No explanations, no wrapper text.

SAFETY:
If you cannot safely restructure without changing meaning, return the original content unchanged."""

USER_PROMPT_TEMPLATE = """Restructure this Markdown file:

{content}

---
Restructured version:"""
```

### 6.3 Prompt Testing Strategy

````python
# Test cases for prompt validation
test_cases = [
    {
        "name": "frontmatter_preservation",
        "input": """---
title: Test
---
# Content""",
        "check": lambda output: output.startswith("---")
    },
    {
        "name": "code_block_preservation",
        "input": """```python
def test():
    pass
```""",
        "check": lambda output: "```python" in output and "def test():" in output
    },
    {
        "name": "inline_code_preservation",
        "input": "Use `python` for scripting",
        "check": lambda output: "`python`" in output
    }
]
````

---

## 7. LangGraph Workflow Construction

### 7.1 Graph Definition

```python
# src/agent/graph.py
from langgraph.graph import StateGraph, END
from .state import AgentState
from .nodes import *

def create_restructure_graph():
    """Create the complete LangGraph workflow."""
    
    # Initialize graph with state schema
    workflow = StateGraph(AgentState)
    
    # Add nodes
    workflow.add_node("discover_files", discover_files)
    workflow.add_node("load_file", load_file)
    workflow.add_node("pre_validate", pre_validate)
    workflow.add_node("llm_restructure", llm_restructure)
    workflow.add_node("post_validate", post_validate)
    workflow.add_node("check_diff", check_diff)
    workflow.add_node("persist_results", persist_results)
    workflow.add_node("generate_report", generate_report)
    
    # Define edges (sequential flow)
    workflow.add_edge("discover_files", "load_file")
    workflow.add_edge("load_file", "pre_validate")
    
    # Conditional edge: skip if validation fails
    workflow.add_conditional_edges(
        "pre_validate",
        route_after_validation,
        {
            "continue": "llm_restructure",
            "skip": "generate_report"
        }
    )
    
    workflow.add_edge("llm_restructure", "post_validate")
    
    # Conditional edge: retry or proceed
    workflow.add_conditional_edges(
        "post_validate",
        route_after_post_validation,
        {
            "continue": "check_diff",
            "retry": "llm_restructure",
            "fail": "generate_report"
        }
    )
    
    workflow.add_edge("check_diff", "persist_results")
    workflow.add_edge("persist_results", "generate_report")
    workflow.add_edge("generate_report", END)
    
    # Set entry point
    workflow.set_entry_point("discover_files")
    
    return workflow.compile()

def route_after_validation(state: AgentState) -> str:
    """Determine next step after pre-validation."""
    if state["status"] == "validation_failed":
        return "skip"
    return "continue"

def route_after_post_validation(state: AgentState) -> str:
    """Determine next step after post-validation."""
    if state["validation_errors"] and state["retry_count"] < 3:
        return "retry"
    elif state["validation_errors"]:
        return "fail"
    return "continue"
```

### 7.2 Branch Logic (Retry Mechanism)

```python
def llm_restructure_with_retry(state: AgentState) -> AgentState:
    """Enhanced restructure node with retry tracking."""
    
    result = llm_restructure(state)
    
    if state["retry_count"] > 0:
        # Adjust prompt for retry
        result["prompt_adjustment"] = f"Previous attempt failed validation. Retry {state['retry_count']}/3"
    
    result["retry_count"] = state.get("retry_count", 0) + 1
    return result
```

---

## 8. CLI Interface Implementation

### 8.1 Command Structure

```python
# src/cli.py
import click
from pathlib import Path
from .agent.graph import create_restructure_graph
from .agent.state import AgentState

@click.command()
@click.argument('path', type=click.Path(exists=True))
@click.option('--dry-run', is_flag=True, help='Preview changes without writing')
@click.option('--model', default='meta-llama/Meta-Llama-3-8B-Instruct', help='Hugging Face model ID')
@click.option('--recursive/--no-recursive', default=True, help='Process directories recursively')
@click.option('--output', type=click.Choice(['summary', 'detailed', 'json']), default='summary')
@click.option('--backup/--no-backup', default=True, help='Create backups before modification')
def restructure(path, dry_run, model, recursive, output, backup):
    """Restructure Markdown files using AI agent."""
    
    click.echo(f"🤖 Markdown Restructure Agent")
    click.echo(f"📁 Target: {path}")
    click.echo(f"🧠 Model: {model}")
    
    # Initialize graph
    graph = create_restructure_graph()
    
    # Prepare initial state
    initial_state = AgentState(
        file_path=path,
        dry_run=dry_run,
        status="pending",
        retry_count=0,
        validation_errors=[],
        processing_start=datetime.now()
    )
    
    # Execute workflow
    with click.progressbar(length=100, label='Processing') as bar:
        final_state = graph.invoke(initial_state)
        bar.update(100)
    
    # Output results
    if output == 'json':
        click.echo(json.dumps(final_state, indent=2, default=str))
    elif output == 'detailed':
        display_detailed_report(final_state)
    else:
        display_summary_report(final_state)

if __name__ == '__main__':
    restructure()
```

### 8.2 Output Formatting

```python
def display_summary_report(state: AgentState):
    """Display concise processing summary."""
    
    status_icon = "✅" if state["status"] == "success" else "❌"
    
    click.echo(f"\n{status_icon} Status: {state['status']}")
    
    if state["changes_detected"]:
        click.echo(f"📊 Changes: {state['diff_summary']}")
    else:
        click.echo("📊 No changes needed - file already optimal")
    
    if state["backup_path"]:
        click.echo(f"💾 Backup: {state['backup_path']}")
    
    if state["error_message"]:
        click.echo(f"⚠️  Error: {state['error_message']}", err=True)
```

---

## 9. Safety Controls & Best Practices

### 9.1 Backup Strategy

```python
class BackupManager:
    """Manages file backups with rotation."""
    
    def __init__(self, max_backups=5):
        self.max_backups = max_backups
    
    def create_backup(self, file_path: str) -> str:
        """Create timestamped backup."""
        backup_dir = Path(file_path).parent / '.md_backups'
        backup_dir.mkdir(exist_ok=True)
        
        timestamp = datetime.now().strftime('%Y%m%d_%H%M%S')
        backup_path = backup_dir / f"{Path(file_path).name}.{timestamp}.bak"
        
        shutil.copy2(file_path, backup_path)
        self._rotate_backups(backup_dir, Path(file_path).name)
        
        return str(backup_path)
    
    def _rotate_backups(self, backup_dir: Path, filename: str):
        """Keep only N most recent backups."""
        backups = sorted(
            backup_dir.glob(f"{filename}.*.bak"),
            key=lambda p: p.stat().st_mtime,
            reverse=True
        )
        
        for old_backup in backups[self.max_backups:]:
            old_backup.unlink()
```

### 9.2 Idempotence Verification

```python
def verify_idempotence(file_path: str, graph) -> bool:
    """Verify that processing the same file twice yields identical results."""
    
    # First pass
    state1 = graph.invoke({"file_path": file_path, "dry_run": True})
    content1 = state1["processed_content"]
    
    # Second pass on first pass output
    state2 = graph.invoke({
        "file_path": file_path,
        "original_content": content1,
        "dry_run": True
    })
    content2 = state2["processed_content"]
    
    return content1 == content2
```

### 9.3 Timeout & Resource Management

```python
import signal
from contextlib import contextmanager

@contextmanager
def timeout(seconds):
    """Context manager for operation timeout."""
    def timeout_handler(signum, frame):
        raise TimeoutError(f"Operation exceeded {seconds}s timeout")
    
    signal.signal(signal.SIGALRM, timeout_handler)
    signal.alarm(seconds)
    try:
        yield
    finally:
        signal.alarm(0)

# Usage in node
def llm_restructure_with_timeout(state: AgentState) -> AgentState:
    try:
        with timeout(120):  # 2 minute timeout
            return llm_restructure(state)
    except TimeoutError:
        return {
            "status": "failed",
            "error_message": "LLM processing timeout",
            "current_node": "llm_restructure"
        }
```

---

## 10. Testing Strategy

### 10.1 Unit Tests

```python
# tests/test_agent.py
import pytest
from src.agent.nodes import pre_validate, post_validate
from src.agent.state import AgentState

def test_pre_validate_detects_frontmatter():
    """Test frontmatter detection."""
    state = AgentState(
        original_content="---\ntitle: Test\n---\n# Content",
        file_path="test.md"
    )
    
    result = pre_validate(state)
    assert result["has_frontmatter"] == True

def test_pre_validate_detects_code_blocks():
    """Test code block detection."""
    state = AgentState(
        original_content="```python\nprint('test')\n```",
        file_path="test.md"
    )
    
    result = pre_validate(state)
    assert result["has_code_blocks"] == True

def test_post_validate_catches_code_loss():
    """Test validation catches code block removal."""
    state = AgentState(
        original_content="```python\ncode\n```",
        processed_content="No code here",
        has_code_blocks=True,
        file_path="test.md"
    )
    
    result = post_validate(state)
    assert "Code block count mismatch" in result["validation_errors"]
```

### 10.2 Integration Tests

```python
def test_end_to_end_processing(tmp_path):
    """Test complete workflow."""
    # Create test file
    test_file = tmp_path / "test.md"
    test_file.write_text("""# Title


Extra blank lines


- List item 1
- List item 2""")
    
    # Run graph
    graph = create_restructure_graph()
    result = graph.invoke({
        "file_path": str(test_file),
        "dry_run": False
    })
    
    assert result["status"] == "success"
    
    # Verify output
    processed = test_file.read_text()
    assert "\n\n\n" not in processed  # No triple blank lines
    assert processed.count("\n\n") < 3  # Minimal double breaks
```

### 10.3 Test Fixtures

````python
# tests/fixtures/complex_document.md
"""
---
title: Complex Test Document
tags: [test, validation]
---

# Main Heading

This is a paragraph with `inline code` and [a link](https://example.com).

## Subheading

```python
def example():
    """Docstring"""
    return 42
````

- List item 1
    - Nested item
- List item 2

<!-- HTML comment to preserve -->

### Deep heading

Final paragraph. """

````

---

## 11. Packaging & Documentation

### 11.1 README.md Template

```markdown
# Markdown Restructuring AI Agent

AI-powered tool for normalizing Markdown structure while preserving content integrity.

## Features

- 🤖 LLM-powered structural optimization
- 🔒 Content preservation guarantees
- 💾 Automatic backups
- 🔄 Idempotent processing
- 🎯 Dry-run mode for safe previews

## Quick Start

```bash
# Install
pip install -r requirements.txt

# Process single file
python -m src.cli document.md

# Process directory
python -m src.cli ./docs --recursive

# Preview changes
python -m src.cli document.md --dry-run
````

## Configuration

Edit `config/model_config.yaml`:

```yaml
model:
  id: "meta-llama/Meta-Llama-3-8B-Instruct"
  quantization: "4bit"
  max_tokens: 8192

processing:
  timeout: 120
  max_retries: 3
  backup_rotation: 5
```

## Safety Features

- Automatic backups before modification
- Post-processing validation
- Idempotence verification
- Configurable timeouts

## License

MIT License - see LICENSE file

````

### 11.2 Configuration Management

```yaml
# config/model_config.yaml
model:
  id: "meta-llama/Meta-Llama-3-8B-Instruct"
  quantization: "4bit"  # Options: "4bit", "8bit", null
  max_new_tokens: 8192
  temperature: 0.1
  device_map: "auto"

processing:
  timeout_seconds: 120
  max_retries: 3
  retry_delay_seconds: 2
  
validation:
  strict_mode: true
  allow_heading_changes: false
  allow_list_reordering: false

backup:
  enabled: true
  max_backups_per_file: 5
  backup_directory: ".md_backups"

output:
  default_format: "summary"  # Options: "summary", "detailed", "json"
  show_diff: true
  color_output: true
````

### 11.3 Usage Examples

```bash
# Basic usage
python -m src.cli README.md

# Dry run with detailed output
python -m src.cli docs/ --dry-run --output detailed

# Use different model
python -m src.cli notes.md --model mistralai/Mistral-7B-Instruct-v0.2

# Process non-recursively
python -m src.cli docs/ --no-recursive

# JSON output for CI/CD integration
python -m src.cli content/ --output json > results.json
```

---

## 12. Production Deployment & Integration

### 12.1 Git Pre-commit Hook

```bash
#!/bin/bash
# .git/hooks/pre-commit

echo "🤖 Running Markdown restructure..."

# Get staged .md files
STAGED_MD=$(git diff --cached --name-only --diff-filter=ACM | grep '\.md)

if [ -n "$STAGED_MD" ]; then
    for file in $STAGED_MD; do
        python -m src.cli "$file" --no-backup
        git add "$file"
    done
    echo "✅ Markdown files restructured"
fi
```

### 12.2 GitHub Actions Workflow

```yaml
# .github/workflows/markdown-check.yml
name: Markdown Structure Check

on:
  pull_request:
    paths:
      - '**.md'

jobs:
  check-markdown:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.10'
    
    - name: Install dependencies
      run: |
        pip install -r requirements.txt
    
    - name: Check Markdown structure
      run: |
        python -m src.cli . --dry-run --output json > results.json
        
    - name: Upload results
      uses: actions/upload-artifact@v3
      with:
        name: markdown-check-results
        path: results.json
    
    - name: Comment PR
      uses: actions/github-script@v6
      with:
        script: |
          const fs = require('fs');
          const results = JSON.parse(fs.readFileSync('results.json'));
          const comment = `## 📝 Markdown Structure Check\n\n${results.summary}`;
          github.rest.issues.createComment({
            issue_number: context.issue.number,
            owner: context.repo.owner,
            repo: context.repo.repo,
            body: comment
          });
```

### 12.3 Docker Deployment

```dockerfile
# Dockerfile
FROM python:3.10-slim

WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application
COPY src/ ./src/
COPY config/ ./config/

# Set up model cache
ENV TRANSFORMERS_CACHE=/app/model_cache
RUN mkdir -p /app/model_cache

# Entry point
ENTRYPOINT ["python", "-m", "src.cli"]
CMD ["--help"]
```

```bash
# Build and run
docker build -t md-restructure-agent .

# Process local files
docker run -v $(pwd):/workspace md-restructure-agent /workspace/docs
```

### 12.4 Scheduled Maintenance (Cron)

```bash
# crontab entry for weekly documentation cleanup
0 2 * * 0 cd /path/to/docs && /usr/bin/python3 -m src.cli . --output json >> /var/log/md-restructure.log 2>&1
```

---

## 13. Performance Optimization

### 13.1 Model Caching Strategy

```python
# src/models/model_cache.py
from functools import lru_cache
from transformers import AutoModelForCausalLM, AutoTokenizer

@lru_cache(maxsize=1)
def get_cached_model(model_id: str):
    """Cache model in memory for multiple invocations."""
    model = AutoModelForCausalLM.from_pretrained(
        model_id,
        device_map="auto",
        torch_dtype="auto"
    )
    tokenizer = AutoTokenizer.from_pretrained(model_id)
    return model, tokenizer
```

### 13.2 Batch Processing

```python
def process_files_batch(file_paths: List[str], batch_size: int = 5) -> List[AgentState]:
    """Process multiple files with batching."""
    results = []
    
    for i in range(0, len(file_paths), batch_size):
        batch = file_paths[i:i + batch_size]
        
        # Process batch in parallel (if model supports it)
        batch_results = []
        for file_path in batch:
            state = graph.invoke({"file_path": file_path})
            batch_results.append(state)
        
        results.extend(batch_results)
        
        # Progress indicator
        print(f"Processed {min(i + batch_size, len(file_paths))}/{len(file_paths)}")
    
    return results
```

### 13.3 Performance Metrics

```python
# src/utils/metrics.py
import time
from dataclasses import dataclass

@dataclass
class ProcessingMetrics:
    file_path: str
    file_size_kb: float
    processing_time_seconds: float
    tokens_processed: int
    
    @property
    def throughput_kb_per_second(self) -> float:
        return self.file_size_kb / self.processing_time_seconds

def collect_metrics(state: AgentState) -> ProcessingMetrics:
    """Extract performance metrics from processing state."""
    return ProcessingMetrics(
        file_path=state["file_path"],
        file_size_kb=len(state["original_content"]) / 1024,
        processing_time_seconds=(
            datetime.now() - state["processing_start"]
        ).total_seconds(),
        tokens_processed=estimate_tokens(state["original_content"])
    )
```

---

## 14. Troubleshooting Guide

### 14.1 Common Issues

**Issue**: Model fails to load with CUDA out of memory

```bash
# Solution: Enable 4-bit quantization
python -m src.cli document.md --model meta-llama/Meta-Llama-3-8B-Instruct

# Or use smaller model
python -m src.cli document.md --model google/gemma-7b-it
```

**Issue**: Processing hangs indefinitely

```python
# Add timeout in config/model_config.yaml
processing:
  timeout_seconds: 60  # Reduce from 120
```

**Issue**: Content validation fails repeatedly

```bash
# Run with detailed logging
python -m src.cli document.md --output detailed

# Check validation errors in output
```

### 14.2 Debugging Tips

```python
# Enable LangGraph visualization
from langgraph.graph import StateGraph

graph = create_restructure_graph()

# Export graph structure
graph.get_graph().draw_mermaid_png(output_file_path="workflow.png")
```

```python
# Add verbose logging
import logging

logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)

logger = logging.getLogger('md_agent')
```

### 14.3 Model-Specific Issues

|Model|Known Issue|Solution|
|---|---|---|
|LLaMA-3-8B|Occasionally adds explanatory text|Update prompt to emphasize "output ONLY Markdown"|
|Mistral-7B|May reorder list items|Set `allow_list_reordering: false` in config|
|Gemma-7B|Slower inference|Reduce `max_new_tokens` to 4096|

---

## 15. Advanced Features

### 15.1 Custom Validation Rules

```python
# src/utils/custom_validators.py
from typing import Callable, List

class CustomValidator:
    """Extensible validation framework."""
    
    def __init__(self):
        self.rules: List[Callable] = []
    
    def add_rule(self, rule: Callable[[str, str], List[str]]):
        """Add custom validation rule."""
        self.rules.append(rule)
    
    def validate(self, original: str, processed: str) -> List[str]:
        """Run all validation rules."""
        errors = []
        for rule in self.rules:
            errors.extend(rule(original, processed))
        return errors

# Example: Preserve specific formatting
def check_table_preservation(original: str, processed: str) -> List[str]:
    """Ensure Markdown tables aren't corrupted."""
    original_tables = original.count('|')
    processed_tables = processed.count('|')
    
    if original_tables != processed_tables:
        return [f"Table structure changed: {original_tables} → {processed_tables} pipes"]
    return []

# Usage
validator = CustomValidator()
validator.add_rule(check_table_preservation)
```

### 15.2 Multi-Model Comparison

```python
def compare_models(file_path: str, models: List[str]) -> dict:
    """Compare output from multiple models."""
    results = {}
    
    for model_id in models:
        graph = create_restructure_graph(model_id=model_id)
        state = graph.invoke({"file_path": file_path, "dry_run": True})
        results[model_id] = {
            "output": state["processed_content"],
            "changes": state["diff_summary"],
            "time": state["processing_time"]
        }
    
    return results

# Usage
comparison = compare_models(
    "README.md",
    models=[
        "meta-llama/Meta-Llama-3-8B-Instruct",
        "mistralai/Mistral-7B-Instruct-v0.2"
    ]
)
```

---

## 16. Maintenance & Updates

### 16.1 Model Update Checklist

- [ ] Test new model with existing prompt templates
- [ ] Run full test suite on sample corpus
- [ ] Benchmark performance metrics
- [ ] Update model_config.yaml with new default
- [ ] Document any prompt adjustments needed
- [ ] Update README with compatibility notes

### 16.2 Monitoring Production Usage

```python
# src/utils/telemetry.py
import json
from pathlib import Path

class UsageLogger:
    """Track agent usage for monitoring."""
    
    def __init__(self, log_path: str = "logs/usage.jsonl"):
        self.log_path = Path(log_path)
        self.log_path.parent.mkdir(exist_ok=True)
    
    def log_processing(self, state: AgentState):
        """Log processing event."""
        event = {
            "timestamp": datetime.now().isoformat(),
            "file": state["file_path"],
            "status": state["status"],
            "changes": state["changes_detected"],
            "duration": (datetime.now() - state["processing_start"]).total_seconds()
        }
        
        with open(self.log_path, 'a') as f:
            f.write(json.dumps(event) + '\n')
```

---

## 17. Resources & References

### 17.1 Documentation Links

- **LangGraph**: [https://langchain-ai.github.io/langgraph/](https://langchain-ai.github.io/langgraph/)
- **Hugging Face Transformers**: [https://huggingface.co/docs/transformers](https://huggingface.co/docs/transformers)
- **Markdown Specification**: [https://spec.commonmark.org/](https://spec.commonmark.org/)

### 17.2 Recommended Reading

1. "Building LLM-Powered Applications" - LangChain documentation
2. "Prompt Engineering Guide" - OpenAI best practices
3. "Quantization Methods" - Hugging Face optimization guide

### 17.3 Community & Support

- GitHub Issues: Report bugs and request features
- Discussions: Share use cases and implementations
- Discord: Real-time community support

---

## Appendix A: Complete Requirements File

```txt
# requirements.txt - Production dependencies

# Core framework
langgraph==1.0.4
langchain-core==0.3.28

# LLM and model handling
transformers==4.36.0
torch>=2.1.0
accelerate>=0.25.0
bitsandbytes>=0.41.0
sentencepiece>=0.1.99
protobuf>=3.20.0

# File and data handling
pyyaml>=6.0
python-dotenv>=1.0.0

# CLI interface
click>=8.1.0
rich>=13.0.0  # For enhanced terminal output

# Testing
pytest>=7.4.0
pytest-cov>=4.1.0
pytest-mock>=3.12.0

# Development tools
black>=23.12.0
flake8>=6.1.0
mypy>=1.7.0
```

---

## Appendix B: Example Output

### Dry-Run Output

```
🤖 Markdown Restructure Agent
📁 Target: docs/guide.md
🧠 Model: meta-llama/Meta-Llama-3-8B-Instruct

Processing ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100%

✅ Status: success
📊 Changes: +3 -7 (10 total)
🔍 Validation: Passed
💾 Backup: Not created (dry-run mode)

Changes preview:
  - Removed 4 empty lines
  - Normalized list indentation
  - Preserved 2 code blocks
  - Preserved YAML frontmatter
```

### Detailed Output

```
🤖 Markdown Restructure Agent v1.0.0
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📄 File: docs/guide.md
📏 Size: 8.4 KB
🕒 Started: 2024-12-26 14:32:10

Workflow Steps:
  ✅ discover_files (0.02s)
  ✅ load_file (0.01s)
  ✅ pre_validate (0.03s)
     • Frontmatter detected
     • 2 code blocks found
  ✅ llm_restructure (12.45s)
     • Model: meta-llama/Meta-Llama-3-8B-Instruct
     • Tokens: 2,847
  ✅ post_validate (0.05s)
     • All checks passed
  ✅ check_diff (0.02s)
  ✅ persist_results (0.08s)
  ✅ generate_report (0.01s)

📊 Summary:
  Lines added: 3
  Lines removed: 7
  Net change: -4 lines
  Processing time: 12.67s
  Throughput: 0.66 KB/s

💾 Backup: docs/.md_backups/guide.md.20241226_143222.bak
✅ Complete
```

---

## Conclusion

This guide provides a complete, production-ready framework for building a Markdown restructuring agent. The system combines the orchestration power of LangGraph with state-of-the-art instruction-tuned models from Hugging Face to deliver reliable, safe, and efficient document processing.

Key takeaways:

- **Modularity**: Each node is independently testable and maintainable
- **Safety**: Multiple validation layers and automatic backups protect content
- **Scalability**: Batch processing and model caching enable production deployment
- **Extensibility**: Custom validators and multi-model support allow adaptation to specific needs

For questions, issues, or contributions, please refer to the project repository or community channels listed in the Resources section.