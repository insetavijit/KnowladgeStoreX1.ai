### What is LangGraph?

LangGraph is a low-level orchestration framework for building, managing, and deploying long-running, stateful agents. It represents a paradigm shift from simple LLM chains to complex, cyclical agent workflows.

**Core Innovation:**

```
Traditional Chains (LangChain):          LangGraph Workflows:
Input → LLM → Output                     Input → Node1 → Node2
(Linear, DAG only)                         ↑       ↓
                                          Node4 ← Node3
                                         (Cyclical, stateful)
```

### Key Differentiators

**What Makes LangGraph Different:**

1. **Graph-Based Architecture** - Workflows modeled as directed graphs
2. **Stateful Execution** - Persistent state across multiple steps
3. **Cyclical Workflows** - Loops and branching, not just linear chains
4. **Built-in Persistence** - Automatic checkpointing and state management
5. **Human-in-the-Loop** - Native support for human intervention
6. **Production-Ready** - Designed for reliability and scale

### Core Capabilities

**What LangGraph Enables:**

```python
# Core features
from langgraph.graph import StateGraph
from langgraph.checkpoint.memory import MemorySaver

# 1. Stateful workflows
# 2. Cyclical execution (agent-tool loops)
# 3. Conditional branching
# 4. Persistent memory
# 5. Human intervention points
# 6. Error recovery
```

### Real-World Use Cases

**Production Deployments:**

- Uber uses LangGraph to streamline large-scale code migrations with specialized agent networks
- Elastic employs LangGraph for real-time threat detection with orchestrated AI agents
- LinkedIn, Replit, Klarna in production

### Architecture Philosophy

**Design Principles:**

```
Low-Level & Flexible:
- No black-box abstractions
- Full control over agent logic
- Descriptive primitives

Production-First:
- Durability over convenience
- Control over simplicity
- Reliability over rapid prototyping
```

### Ecosystem Position

**LangGraph in Context:**

```
LangChain Ecosystem:
├── LangChain Core (chains, tools, models)
├── LangGraph (agent orchestration)
├── LangSmith (observability, evals)
└── LangGraph Platform (deployment)
```

### Interview Talking Points

- LangGraph enables complex, stateful agent workflows beyond simple chains
- Built for durable execution, streaming, and human-in-the-loop capabilities
- Designed for production from first principles
- Lower-level than LangChain agents - trades ease of use for control
- Supports cycles and loops, unlike traditional DAG-based chains
- Used by major companies for production AI agents

**One-liner:** "LangGraph models agent logic as a stateful graph of steps."

---

## Installation & Environment Setup

### Interview Learning Goals

Demonstrate proper setup for LangGraph development environment.

### Basic Installation

**Core Package:**

```bash
# Install LangGraph
pip install langgraph

# With checkpointing support
pip install langgraph langgraph-checkpoint-sqlite

# Full installation with LangChain
pip install langgraph langchain langchain-openai
```

**Version Check:**

```python
import langgraph
print(langgraph.__version__)  # Verify installation
```

### Environment Management

**Using Virtual Environments:**

```bash
# Using venv
python -m venv langgraph-env
source langgraph-env/bin/activate  # Unix
# or
langgraph-env\Scripts\activate  # Windows

pip install langgraph

# Using poetry
poetry init
poetry add langgraph
poetry add langchain langchain-openai
poetry install
```

**Using conda:**

```bash
conda create -n langgraph python=3.11
conda activate langgraph
pip install langgraph
```

### Python Version Requirements

**Compatibility:**

```python
# LangGraph requires Python 3.9+
# Recommended: Python 3.11 or 3.12 for best performance

import sys
assert sys.version_info >= (3, 9), "Python 3.9+ required"
```

### API Keys Configuration

**Environment Variables:**

```bash
# .env file
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...
TAVILY_API_KEY=tvly-...

# Optional for LangSmith tracing
LANGCHAIN_TRACING_V2=true
LANGCHAIN_API_KEY=ls__...
LANGCHAIN_PROJECT=my-langgraph-project
```

**Loading Environment:**

```python
import os
from dotenv import load_dotenv

load_dotenv()

# Verify keys loaded
assert os.getenv("OPENAI_API_KEY"), "OpenAI API key not found"
```

### Development Tools

**Recommended Tools:**

```bash
# LangGraph CLI (for local development)
pip install "langgraph[cli]"

# Development server
langgraph dev

# LangSmith for observability
pip install langsmith
```

**LangGraph Studio:**

```bash
# Start local development server
langgraph dev

# Access Studio at:
# https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024
```

### Dependencies for Common Use Cases

**Minimal Agent Setup:**

```python
# requirements.txt
langgraph>=0.2.0
langchain-core>=0.3.0
langchain-openai>=0.2.0
python-dotenv>=1.0.0
```

**Production Setup:**

```python
# requirements.txt
langgraph>=0.2.0
langgraph-checkpoint-postgres>=0.1.0
langchain>=0.3.0
langchain-openai>=0.2.0
langgraph-sdk>=0.1.0  # For API client
pydantic>=2.0.0
python-dotenv>=1.0.0
```

### Verification Script

**Test Installation:**

```python
# test_setup.py
import sys

def verify_installation():
    """Verify LangGraph setup"""
    checks = []
    
    # Python version
    py_version = sys.version_info >= (3, 9)
    checks.append(("Python 3.9+", py_version))
    
    # LangGraph import
    try:
        import langgraph
        checks.append(("LangGraph", True))
    except ImportError:
        checks.append(("LangGraph", False))
    
    # LangChain import
    try:
        import langchain
        checks.append(("LangChain", True))
    except ImportError:
        checks.append(("LangChain", False))
    
    # Environment variables
    import os
    has_api_key = bool(os.getenv("OPENAI_API_KEY"))
    checks.append(("API Keys", has_api_key))
    
    # Print results
    for check, status in checks:
        symbol = "✓" if status else "✗"
        print(f"{symbol} {check}")
    
    return all(status for _, status in checks)

if __name__ == "__main__":
    success = verify_installation()
    sys.exit(0 if success else 1)
```

### Common Installation Issues

**Troubleshooting:**

```python
# Issue: Import errors
# Solution: Reinstall in clean environment
pip uninstall langgraph langchain -y
pip install langgraph langchain

# Issue: Version conflicts
# Solution: Use specific versions
pip install "langgraph==0.2.0" "langchain==0.3.0"

# Issue: Missing checkpoint dependencies
# Solution: Install checkpoint package
pip install langgraph-checkpoint-sqlite
```

### Docker Setup (Optional)

**Containerized Environment:**

```dockerfile
# Dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["python", "app.py"]
```

```yaml
# docker-compose.yml
version: '3.8'
services:
  langgraph-app:
    build: .
    environment:
      - OPENAI_API_KEY=${OPENAI_API_KEY}
    ports:
      - "8000:8000"
    volumes:
      - ./:/app
```

### Interview Talking Points

- LangGraph requires Python 3.9+ with 3.11+ recommended
- Can be installed standalone or with LangChain
- Environment variables crucial for API keys
- LangGraph CLI provides development server
- LangSmith integration optional but valuable for debugging
- Checkpoint packages separate (SQLite, Postgres)
- Virtual environments recommended for project isolation

**One-liner:** "Proper setup ensures LangGraph runs reliably in your environment."

---

## LangChain Dependency

### Interview Learning Goals

Explain LangGraph's relationship with LangChain and when each is used.

### The Relationship

**LangChain Foundation:**

LangGraph is built by the creators of LangChain and can be used without LangChain, though they often complement each other.

```python
# LangGraph standalone
from langgraph.graph import StateGraph

# LangGraph with LangChain components
from langgraph.graph import StateGraph
from langchain_openai import ChatOpenAI
from langchain.tools import Tool
```

### Shared Abstractions

**What LangGraph Inherits:**

```python
# 1. Model interfaces
from langchain_openai import ChatOpenAI
from langchain_anthropic import ChatAnthropic

model = ChatOpenAI(model="gpt-4")  # Works in LangGraph

# 2. Tool abstractions
from langchain.tools import tool

@tool
def search_web(query: str) -> str:
    """Search the web for information"""
    return "Search results..."

# 3. Message types
from langchain_core.messages import HumanMessage, AIMessage, SystemMessage

messages = [
    SystemMessage(content="You are helpful"),
    HumanMessage(content="Hello!")
]

# 4. Prompt templates
from langchain_core.prompts import ChatPromptTemplate

prompt = ChatPromptTemplate.from_messages([
    ("system", "You are {role}"),
    ("human", "{input}")
])
```

### Compatibility Matrix

**Integration Points:**

```python
# Components that work seamlessly
Integration Areas:
├── Models (ChatOpenAI, ChatAnthropic, etc.)
├── Tools (LangChain tool decorators)
├── Retrievers (vector stores, document loaders)
├── Memory (conversation buffers)
├── Prompts (templates, few-shot examples)
└── Output Parsers (structured outputs)
```

### When to Use Each

**LangChain Use Cases:**

```python
# Simple chains - use LangChain
from langchain.chains import LLMChain

chain = LLMChain(llm=model, prompt=prompt)
result = chain.run("What is AI?")

# Retrieval QA - use LangChain
from langchain.chains import RetrievalQA

qa = RetrievalQA.from_chain_type(
    llm=model,
    retriever=vectorstore.as_retriever()
)
```

**LangGraph Use Cases:**

```python
# Complex agents - use LangGraph
from langgraph.graph import StateGraph
from langgraph.prebuilt import ToolExecutor

# Multi-step reasoning with loops
# Human-in-the-loop workflows
# Stateful conversations
# Conditional branching
```

### Hybrid Approach

**Best of Both Worlds:**

```python
from langchain_openai import ChatOpenAI
from langchain.tools import tool
from langgraph.graph import StateGraph, END
from langgraph.prebuilt import ToolNode

# LangChain components
model = ChatOpenAI(model="gpt-4")

@tool
def calculator(expression: str) -> float:
    """Evaluate mathematical expression"""
    return eval(expression)

tools = [calculator]

# LangGraph orchestration
class State(TypedDict):
    messages: list

workflow = StateGraph(State)

def call_model(state: State):
    # Use LangChain model in LangGraph node
    response = model.invoke(state["messages"])
    return {"messages": [response]}

# Combine LangChain tools with LangGraph nodes
tool_node = ToolNode(tools)

workflow.add_node("agent", call_model)
workflow.add_node("tools", tool_node)
```

### Version Compatibility

**Keeping Versions Aligned:**

```python
# requirements.txt
langgraph>=0.2.0
langchain>=0.3.0  # Must be compatible
langchain-core>=0.3.0
langchain-openai>=0.2.0

# Check compatibility
from langgraph import __version__ as lg_version
from langchain import __version__ as lc_version

print(f"LangGraph: {lg_version}")
print(f"LangChain: {lc_version}")
```

### Migration from LangChain

**Upgrading to LangGraph:**

```python
# Before: LangChain Agent
from langchain.agents import AgentExecutor, create_openai_functions_agent

agent = create_openai_functions_agent(llm, tools, prompt)
executor = AgentExecutor(agent=agent, tools=tools)

result = executor.invoke({"input": "What's 2+2?"})

# After: LangGraph (more control)
from langgraph.prebuilt import create_react_agent

app = create_react_agent(model, tools)

result = app.invoke({
    "messages": [("human", "What's 2+2?")]
})
```

### Standalone LangGraph

**Using Without LangChain:**

```python
# Pure LangGraph implementation
from langgraph.graph import StateGraph
from typing import TypedDict
import openai

class State(TypedDict):
    question: str
    answer: str

def query_llm(state: State):
    """Call OpenAI directly without LangChain"""
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": state["question"]}]
    )
    return {"answer": response.choices[0].message.content}

workflow = StateGraph(State)
workflow.add_node("llm", query_llm)
workflow.set_entry_point("llm")
workflow.set_finish_point("llm")

app = workflow.compile()
```

### Interview Talking Points

- LangGraph builds on LangChain primitives but can work standalone
- Shares model, tool, and prompt abstractions with LangChain
- Use LangChain for simple chains, LangGraph for complex agents
- Most production systems combine both frameworks
- LangChain provides integrations, LangGraph provides orchestration
- Version compatibility important for seamless integration
- Migration path exists from LangChain Agents to LangGraph

**One-liner:** "LangGraph builds on LangChain primitives for tools and models."

---

## Project Structure

### Interview Learning Goals

Organize LangGraph code for maintainability and scalability.

### Recommended Structure

**Standard Project Layout:**

```
my-langgraph-project/
├── src/
│   ├── agents/
│   │   ├── __init__.py
│   │   ├── customer_support.py
│   │   └── research_agent.py
│   ├── graphs/
│   │   ├── __init__.py
│   │   ├── main_graph.py
│   │   └── sub_graphs.py
│   ├── nodes/
│   │   ├── __init__.py
│   │   ├── llm_nodes.py
│   │   ├── tool_nodes.py
│   │   └── human_nodes.py
│   ├── tools/
│   │   ├── __init__.py
│   │   ├── search.py
│   │   ├── database.py
│   │   └── api_clients.py
│   ├── state/
│   │   ├── __init__.py
│   │   ├── schemas.py
│   │   └── reducers.py
│   ├── config/
│   │   ├── __init__.py
│   │   ├── settings.py
│   │   └── prompts.py
│   └── utils/
│       ├── __init__.py
│       └── helpers.py
├── tests/
│   ├── test_agents.py
│   ├── test_nodes.py
│   └── test_tools.py
├── langgraph.json
├── requirements.txt
├── .env.example
├── Dockerfile
└── README.md
```

### Module Organization

**agents/ - Agent Definitions:**

```python
# src/agents/customer_support.py
from langgraph.graph import StateGraph
from ..state.schemas import SupportState
from ..nodes import llm_nodes, tool_nodes

def create_support_agent() -> StateGraph:
    """Create customer support agent graph"""
    workflow = StateGraph(SupportState)
    
    workflow.add_node("classifier", llm_nodes.classify_intent)
    workflow.add_node("responder", llm_nodes.generate_response)
    workflow.add_node("escalate", tool_nodes.create_ticket)
    
    workflow.set_entry_point("classifier")
    workflow.add_conditional_edges("classifier", route_intent)
    
    return workflow
```

**graphs/ - Graph Compositions:**

```python
# src/graphs/main_graph.py
from langgraph.graph import StateGraph
from ..agents.customer_support import create_support_agent
from ..agents.research_agent import create_research_agent

def create_main_graph():
    """Compose multiple sub-graphs"""
    workflow = StateGraph(MainState)
    
    # Add sub-graphs as nodes
    support_graph = create_support_agent().compile()
    research_graph = create_research_agent().compile()
    
    workflow.add_node("support", support_graph)
    workflow.add_node("research", research_graph)
    
    return workflow.compile()
```

**nodes/ - Reusable Node Functions:**

```python
# src/nodes/llm_nodes.py
from langchain_openai import ChatOpenAI
from ..config.settings import get_settings

settings = get_settings()
model = ChatOpenAI(model=settings.MODEL_NAME)

def classify_intent(state: dict) -> dict:
    """Classify user intent"""
    prompt = f"Classify intent: {state['question']}"
    response = model.invoke(prompt)
    return {"intent": response.content}

def generate_response(state: dict) -> dict:
    """Generate final response"""
    response = model.invoke(state["question"])
    return {"answer": response.content}
```

```python
# src/nodes/tool_nodes.py
from ..tools.search import web_search
from ..tools.database import query_db

def search_node(state: dict) -> dict:
    """Execute web search"""
    results = web_search(state["query"])
    return {"search_results": results}

def database_node(state: dict) -> dict:
    """Query database"""
    data = query_db(state["sql"])
    return {"db_results": data}
```

**state/ - State Schemas:**

```python
# src/state/schemas.py
from typing import TypedDict, Annotated, Sequence
from operator import add

class AgentState(TypedDict):
    """Base agent state"""
    messages: Annotated[Sequence[str], add]
    next_step: str

class SupportState(AgentState):
    """Customer support specific state"""
    customer_id: str
    intent: str
    priority: str
    resolved: bool

class ResearchState(AgentState):
    """Research agent state"""
    query: str
    sources: list[str]
    summary: str
```

```python
# src/state/reducers.py
def merge_messages(left: list, right: list) -> list:
    """Custom reducer for messages"""
    return left + right

def update_priority(left: str, right: str) -> str:
    """Update priority, keeping highest"""
    priority_order = {"low": 1, "medium": 2, "high": 3}
    if priority_order.get(right, 0) > priority_order.get(left, 0):
        return right
    return left
```

**tools/ - Tool Implementations:**

```python
# src/tools/search.py
from langchain.tools import tool
import requests

@tool
def web_search(query: str) -> str:
    """Search the web for information"""
    # Implementation
    results = search_api.search(query)
    return format_results(results)

@tool
def research_paper_search(topic: str) -> list[dict]:
    """Search academic papers"""
    # Implementation
    return papers
```

**config/ - Configuration:**

```python
# src/config/settings.py
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    """Application settings"""
    MODEL_NAME: str = "gpt-4"
    TEMPERATURE: float = 0.7
    MAX_TOKENS: int = 1000
    
    OPENAI_API_KEY: str
    DATABASE_URL: str
    
    class Config:
        env_file = ".env"

def get_settings() -> Settings:
    return Settings()
```

```python
# src/config/prompts.py
from langchain_core.prompts import ChatPromptTemplate

CLASSIFIER_PROMPT = ChatPromptTemplate.from_messages([
    ("system", "You are an intent classifier."),
    ("human", "Classify this query: {query}")
])

RESPONDER_PROMPT = ChatPromptTemplate.from_messages([
    ("system", "You are a helpful assistant."),
    ("human", "{question}")
])
```

### Entry Points

**main.py:**

```python
# main.py
from src.graphs.main_graph import create_main_graph
from src.config.settings import get_settings
from langgraph.checkpoint.sqlite import SqliteSaver

def main():
    """Application entry point"""
    settings = get_settings()
    
    # Create graph with persistence
    memory = SqliteSaver.from_conn_string(":memory:")
    app = create_main_graph()
    graph = app.compile(checkpointer=memory)
    
    # Run
    config = {"configurable": {"thread_id": "1"}}
    result = graph.invoke({
        "messages": ["Hello!"]
    }, config)
    
    print(result)

if __name__ == "__main__":
    main()
```

### LangGraph Configuration

**langgraph.json:**

```json
{
  "dependencies": ["."],
  "graphs": {
    "agent": "./src/graphs/main_graph.py:create_main_graph"
  },
  "env": ".env"
}
```

### Testing Structure

**tests/ Organization:**

```python
# tests/test_nodes.py
import pytest
from src.nodes.llm_nodes import classify_intent

def test_classify_intent():
    state = {"question": "I want to cancel my order"}
    result = classify_intent(state)
    assert "intent" in result
    assert result["intent"] in ["cancel", "support"]

# tests/test_graphs.py
from src.graphs.main_graph import create_main_graph

def test_graph_compilation():
    graph = create_main_graph()
    assert graph is not None
    
def test_graph_execution():
    graph = create_main_graph()
    result = graph.invoke({"messages": ["test"]})
    assert "answer" in result
```

### Interview Talking Points

- Clean separation of concerns (agents, nodes, tools, state)
- State schemas centralized for reusability
- Configuration separated from logic
- Tools organized by functionality
- Tests mirror source structure
- Entry points clearly defined
- LangGraph.json for deployment configuration

**One-liner:** "Clean structure keeps agent projects maintainable."

---

## Core Concepts: Graphs

### Interview Learning Goals

Explain workflow topology and how graphs define agent execution.

### What is a Graph?

In LangGraph, a graph is a directed structure where each node represents an LLM agent or computational step, and edges are communication channels between agents.

```python
# Basic graph structure
from langgraph.graph import StateGraph

class State(TypedDict):
    message: str

# Create graph
workflow = StateGraph(State)
```

### Graph Types

**DAG vs Cyclical:**

```python
# Directed Acyclic Graph (DAG)
# Linear flow, no loops
workflow.add_node("step1", func1)
workflow.add_node("step2", func2)
workflow.add_edge("step1", "step2")
#  step1 → step2 (one direction only)

# Cyclical Graph
# Can loop back
workflow.add_node("agent", agent_func)
workflow.add_node("tools", tool_func)
workflow.add_edge("tools", "agent")  # Loops back
workflow.add_conditional_edges("agent", should_continue)
#  agent ⇄ tools (bidirectional)
```

### Key Components

**Graph Anatomy:**

```python
from langgraph.graph import State Graph, END

# 1. State Schema
class AgentState(TypedDict):
    messages: list
    next_action: str

# 2. Initialize Graph
workflow = StateGraph(AgentState)

# 3. Add Nodes
workflow.add_node("start", start_node)
workflow.add_node("process", process_node)
workflow.add_node("end", end_node)

# 4. Add Edges
workflow.add_edge("start", "process")
workflow.add_conditional_edges(
    "process",
    lambda x: "end" if x["done"] else "process"
)

# 5. Set Entry/Exit
workflow.set_entry_point("start")
workflow.set_finish_point("end")

# 6. Compile
app = workflow.compile()
```

### Start and End Nodes

**Entry and Exit Points:**

```python
# Entry point - where execution begins
workflow.set_entry_point("initial_node")

# Exit points - where execution can end
workflow.set_finish_point("final_node")

# Or use END constant
from langgraph.graph import END

workflow.add_conditional_edges(
    "decision_node",
    router_function,
    {
        "continue": "next_node",
        "stop": END
    }
)
```

### Graph Visualization

**Understanding Flow:**

```
Simple Linear Graph:
START → node1 → node2 → node3 → END

Agent-Tool Loop:
START → agent → [decision]
             ↓         ↑
           tools ──────┘
             ↓
           END

Multi-Path Graph:
        ┌──> pathA ──┐
START ──┤            ├──> END
        └──> pathB ──┘
```

### StateGraph vs MessageGraph

**Choosing the Right Graph:**

```python
# StateGraph - custom state schema
from langgraph.graph import StateGraph

class MyState(TypedDict):
    count: int
    data: list

workflow = StateGraph(MyState)

# MessageGraph - pre-built for messages
from langgraph.graph import MessageGraph

# Automatically handles message list
workflow = MessageGraph()
```

### Compilation

**Creating Executable Graph:**

```python
from langgraph.checkpoint.memory import MemorySaver

# Without persistence
app = workflow.compile()

# With persistence
memory = MemorySaver()
app = workflow.compile(checkpointer=memory)

# With interrupt points
app = workflow.compile(
    checkpointer=memory,
    interrupt_before=["human_review"],
    interrupt_after=["critical_step"]
)
```

### Example: Complete Graph

**Practical Implementation:**

```python
from langgraph.graph import StateGraph, END
from typing import TypedDict

class State(TypedDict):
    input: str
    output: str
    steps: int

def process(state: State) -> State:
    return {
        "output": f"Processed: {state['input']}",
        "steps": state.get("steps", 0) + 1
    }

def should_continue(state: State) -> str:
    if state["steps"] >= 3:
        return "end"
    return "continue"

# Build graph
workflow = StateGraph(State)

workflow.add_node("processor", process)

workflow.set_entry_point("processor")

workflow.add_conditional_edges(
    "processor",
    should_continue,
    {
        "continue": "processor",  # Loop
        "end": END
    }
)

app = workflow.compile()

# Execute
result = app.invoke({"input": "Hello", "steps": 0})
print(result)
# {"input": "Hello", "output": "Processed: Hello", "steps": 3}
```

### SubGraphs

**Composing Graphs:**

```python
# Create sub-graph
def create_subgraph():
    sub_workflow = StateGraph(SubState)
    sub_workflow.add_node("sub_node1", func1)
    sub_workflow.add_node("sub_node2", func2)
    return sub_workflow.compile()

# Use in main graph
main_workflow = StateGraph(MainState)
subgraph = create_subgraph()

main_workflow.add_node("subgraph", subgraph)
main_workflow.add_edge("start", "subgraph")
```

### Interview Talking Points

- Graphs define the topology of agent workflows
- StateGraph for custom state, MessageGraph for conversations
- Can be DAGs (linear) or cyclical (loops)
- Entry points define where execution starts
- END or finish_point marks termination
- Conditional edges enable branching logic
- Compilation creates executable application
- Sub-graphs enable modular composition

**One-liner:** "Graphs define the overall flow of agent execution."

---

## Nodes & Functions

### Interview Learning Goals

Explain execution units and how nodes encapsulate agent steps.

### What are Nodes?

Nodes are the building blocks of LangGraph, representing distinct units of work or computational steps. Each node is a Python function that processes state.

### Node Function Signature

**Basic Structure:**

```python
from typing import TypedDict

class State(TypedDict):
    message: str
    count: int

def my_node(state: State) -> dict:
    """
    Node function signature:
    - Input: Current state
    - Output: Dict with state updates
    """
    return {
        "message": f"Processed: {state['message']}",
        "count": state.get("count", 0) + 1
    }
```

### Node Types

**Common Node Patterns:**

```python
# 1. LLM Node - Call language model
def llm_node(state: State) -> dict:
    from langchain_openai import ChatOpenAI
    model = ChatOpenAI()
    response = model.invoke(state["messages"])
    return {"messages": [response]}

# 2. Tool Node - Execute tools
def tool_node(state: State) -> dict:
    tool_call = state["tool_calls"][-1]
    result = execute_tool(tool_call)
    return {"tool_results": [result]}

# 3. Router Node - Decision making
def router_node(state: State) -> dict:
    intent = classify_intent(state["input"])
    return {"next_action": intent}

# 4. Transform Node - Data processing
def transform_node(state: State) -> dict:
    processed = process_data(state["raw_data"])
    return {"processed_data": processed}

# 5. Human Node - Human-in-the-loop
def human_node(state: State) -> dict:
    # Wait for human input
    approval = get_human_approval(state["draft"])
    return {"approved": approval}
```

### Inputs and Outputs

**State Flow:**

```python
class State(TypedDict):
    input: str
    intermediate: str
    output: str
    metadata: dict

def node1(state: State) -> dict:
    # Read from state
    user_input = state["input"]
    
    # Process
    result = process(user_input)
    
    # Return updates (partial state)
    return {
        "intermediate": result,
        "metadata": {"step": "node1", "timestamp": time.time()}
    }
    # Only updates specified keys

def node2(state: State) -> dict:
    # Use previous node's output
    data = state["intermediate"]
    
    # Final processing
    final = finalize(data)
    
    return {"output": final}
```

### Side Effects

**Handling External Operations:**

```python
def node_with_side_effects(state: State) -> dict:
    """Node can perform side effects"""
    
    # Database writes
    save_to_db(state["user_id"], state["data"])
    
    # API calls
    notify_webhook(state["event"])
    
    # Logging
    logger.info(f"Processing {state['id']}")
    
    # File operations
    with open("log.txt", "a") as f:
        f.write(f"{state['message']}\n")
    
    # Return state updates
    return {"processed": True, "timestamp": time.time()}

# Best practice: Keep side effects explicit and logged
```

### Error Handling in Nodes

**Robust Node Implementation:**

```python
def robust_node(state: State) -> dict:
    """Node with error handling"""
    try:
        result = risky_operation(state["input"])
        return {
            "output": result,
            "error": None,
            "status": "success"
        }
    except ValueError as e:
        logger.error(f"Validation error: {e}")
        return {
            "error": str(e),
            "status": "validation_error"
        }
    except Exception as e:
        logger.exception("Unexpected error")
        return {
            "error": "Internal error",
            "status": "failed"
        }

# Graph can route based on error status
def route_after_node(state: State) -> str:
    if state["status"] == "success":
        return "continue"
    return "error_handler"
```

### Async Nodes

**Asynchronous Execution:**

```python
import asyncio

async def async_node(state: State) -> dict:
    """Async node for I/O operations"""
    
    # Parallel API calls
    results = await asyncio.gather(
        fetch_data_api_1(state["query"]),
        fetch_data_api_2(state["query"]),
        fetch_data_api_3(state["query"])
    )
    
    return {
        "combined_results": combine(results)
    }

# Use in graph
workflow.add_node("async_fetch", async_node)

# Invoke with async
result = await app.ainvoke({"query": "test"})
```

### Parameterized Nodes

**Creating Flexible Nodes:**

```python
def create_llm_node(model_name: str, temperature: float):
    """Factory function for configurable nodes"""
    from langchain_openai import ChatOpenAI
    
    model = ChatOpenAI(
        model=model_name,
        temperature=temperature
    )
    
    def llm_node(state: State) -> dict:
        response = model.invoke(state["messages"])
        return {"messages": [response]}
    
    return llm_node

# Use in graph
workflow.add_node(
    "gpt4_creative",
    create_llm_node("gpt-4", 0.9)
)

workflow.add_node(
    "gpt4_precise",
    create_llm_node("gpt-4", 0.1)
)
```

### Node Composition

**Building Complex Nodes:**

```python
def compose_nodes(*funcs):
    """Compose multiple functions into one node"""
    def composed_node(state: State) -> dict:
        result = state
        for func in funcs:
            updates = func(result)
            result = {**result, **updates}
        return updates  # Return only last updates
    
    return composed_node

# Usage
def step1(state): return {"count": state.get("count", 0) + 1}
def step2(state): return {"doubled": state["count"] * 2}
def step3(state): return {"message": f"Result: {state['doubled']}"}

combined_node = compose_nodes(step1, step2, step3)
workflow.add_node("multi_step", combined_node)
```

### Testing Nodes

**Unit Testing:**

```python
import pytest

def test_node_output():
    """Test node in isolation"""
    state = {"input": "test", "count": 0}
    result = my_node(state)
    
    assert "message" in result
    assert result["count"] == 1
    assert "test" in result["message"]

def test_node_error_handling():
    """Test error cases"""
    state = {"input": None}
    result = robust_node(state)
    
    assert result["status"] == "validation_error"
    assert result["error"] is not None

@pytest.mark.asyncio
async def test_async_node():
    """Test async node"""
    state = {"query": "test"}
    result = await async_node(state)
    
    assert "combined_results" in result
```

### Best Practices

**Node Design Principles:**

```python
# 1. Single Responsibility
def focused_node(state: State) -> dict:
    """Do one thing well"""
    result = single_task(state["input"])
    return {"output": result}

# 2. Pure Functions (when possible)
def pure_node(state: State) -> dict:
    """Same input → same output"""
    # No external dependencies
    # No side effects
    return {"result": transform(state["data"])}

# 3. Clear Naming
def classify_user_intent(state: State) -> dict:
    """Name describes what node does"""
    # Not: node1, process, handle
    # Instead: descriptive verb_noun pattern
    pass

# 4. Small State Updates
def efficient_node(state: State) -> dict:
    """Return only what changed"""
    # Bad: return entire state
    # Good: return only updates
    return {"new_field": "value"}

# 5. Document Expectations
def documented_node(state: State) -> dict:
    """
    Process user input.
    
    Expects state keys:
    - input: str (user message)
    - context: dict (conversation context)
    
    Returns:
    - intent: str (classified intent)
    - confidence: float (0-1)
    """
    # Implementation
    pass
```

### Interview Talking Points

- Nodes are Python functions that process state
- Input is current state, output is dict of updates
- Can be sync or async
- Should be focused and testable
- Can have side effects but keep explicit
- Error handling within nodes recommended
- Parameterized nodes enable reusability
- Node composition creates complex behaviors

**One-liner:** "Nodes encapsulate individual steps in the agent."

---

## Edges & Routing Logic

### Interview Learning Goals

Explain how transitions work and how edges control agent flow.

### What are Edges?

Edges define the transitions between nodes in a LangGraph workflow. They determine the order of execution and enable complex routing logic.

### Edge Types

**Three Types of Edges:**

```python
from langgraph.graph import StateGraph, END

workflow = StateGraph(State)

# 1. Regular Edges - Always follow same path
workflow.add_edge("node_a", "node_b")
# node_a always → node_b

# 2. Conditional Edges - Dynamic routing
workflow.add_conditional_edges(
    "decision_node",
    routing_function,
    {
        "path_a": "node_a",
        "path_b": "node_b",
        "end": END
    }
)

# 3. Entry/Finish Points
workflow.set_entry_point("start_node")
workflow.set_finish_point("end_node")
```

### Regular Edges

**Simple Transitions:**

```python
# Direct connection
workflow.add_edge("step1", "step2")
workflow.add_edge("step2", "step3")
workflow.add_edge("step3", END)

# Creates linear flow:
# step1 → step2 → step3 → END
```

### Conditional Edges

**Dynamic Routing:**

```python
def route_based_on_intent(state: State) -> str:
    """Router function determines next node"""
    intent = state.get("intent", "unknown")
    
    if intent == "question":
        return "qa_node"
    elif intent == "task":
        return "task_node"
    elif intent == "chitchat":
        return "chitchat_node"
    else:
        return "fallback_node"

# Add conditional edge
workflow.add_conditional_edges(
    "classifier",  # Source node
    route_based_on_intent,  # Router function
    {
        "qa_node": "qa_node",
        "task_node": "task_node",
        "chitchat_node": "chitchat_node",
        "fallback_node": "fallback_node"
    }
)
```

### Routing Functions

**Router Patterns:**

```python
# Pattern 1: Simple condition
def simple_router(state: State) -> str:
    return "next_node" if state["condition"] else "other_node"

# Pattern 2: Multi-way routing
def multi_router(state: State) -> str:
    score = state["confidence"]
    
    if score > 0.9:
        return "high_confidence"
    elif score > 0.6:
        return "medium_confidence"
    else:
        return "low_confidence"

# Pattern 3: State-based routing
def stateful_router(state: State) -> str:
    if state["retry_count"] > 3:
        return "give_up"
    elif state["has_error"]:
        return "retry"
    else:
        return "continue"

# Pattern 4: Tool-based routing
def tool_router(state: State) -> str:
    """Route based on tool calls"""
    if state.get("tool_calls"):
        return "execute_tools"
    else:
        return END
```

### Branching Logic

**Complex Routing:**

```python
class State(TypedDict):
    question: str
    requires_search: bool
    requires_calc: bool
    requires_db: bool

def capability_router(state: State) -> list[str]:
    """Route to multiple nodes (parallel)"""
    next_nodes = []
    
    if state["requires_search"]:
        next_nodes.append("search_node")
    
    if state["requires_calc"]:
        next_nodes.append("calc_node")
    
    if state["requires_db"]:
        next_nodes.append("db_node")
    
    return next_nodes if next_nodes else ["respond"]

# LangGraph handles parallel execution
# Then continues when all complete
```

### Loops and Cycles

**Implementing Feedback Loops:**

```python
def should_continue_loop(state: State) -> str:
    """Decide whether to loop or exit"""
    
    # Exit conditions
    if state["max_iterations"] >= 10:
        return "end"
    
    if state["goal_achieved"]:
        return "end"
    
    if state["stuck"]:
        return "end"
    
    # Continue looping
    return "continue"

# Create loop
workflow.add_node("agent", agent_node)
workflow.add_node("tools", tool_node)

workflow.add_edge("agent", "tools")

workflow.add_conditional_edges(
    "tools",
    should_continue_loop,
    {
        "continue": "agent",  # Loop back
        "end": END
    }
)

# Creates cycle: agent ⇄ tools
```

### Human-in-the-Loop Routing

**Interrupt for Human Input:**

```python
def human_review_router(state: State) -> str:
    """Route to human review when needed"""
    
    # Criteria for human review
    if state["confidence"] < 0.7:
        return "human_review"
    
    if state["contains_sensitive_data"]:
        return "human_review"
    
    if state["high_stakes_decision"]:
        return "human_review"
    
    return "auto_process"

workflow.add_conditional_edges(
    "decision_maker",
    human_review_router,
    {
        "human_review": "human_input",
        "auto_process": "finalize"
    }
)

# Compile with interrupt
app = workflow.compile(
    checkpointer=memory,
    interrupt_before=["human_input"]
)
```

### Error Routing

**Handling Failures:**

```python
def error_router(state: State) -> str:
    """Route based on error state"""
    
    if not state.get("error"):
        return "success_path"
    
    error_type = state["error_type"]
    retry_count = state.get("retry_count", 0)
    
    if retry_count >= 3:
        return "give_up"
    
    if error_type == "rate_limit":
        return "wait_and_retry"
    elif error_type == "validation":
        return "fix_input"
    else:
        return "retry"

workflow.add_conditional_edges(
    "risky_operation",
    error_router,
    {
        "success_path": "next_step",
        "wait_and_retry": "delay_node",
        "fix_input": "input_validator",
        "retry": "risky_operation",
        "give_up": "error_handler"
    }
)
```

### Dynamic Edge Mapping

**Runtime Edge Determination:**

```python
def dynamic_router(state: State) -> str:
    """Dynamically determine routing"""
    
    # Load routing rules from config
    routing_rules = state.get("routing_config", {})
    
    for rule in routing_rules:
        if evaluate_condition(rule["condition"], state):
            return rule["target_node"]
    
    return "default_node"

# Flexible routing based on runtime config
workflow.add_conditional_edges(
    "router",
    dynamic_router,
    # Build mapping from possible nodes
    {node: node for node in all_possible_nodes}
)
```

### Testing Routing Logic

**Unit Testing Routers:**

```python
def test_router():
    """Test routing function"""
    
    # Test path A
    state_a = {"intent": "question", "confidence": 0.9}
    assert route_based_on_intent(state_a) == "qa_node"
    
    # Test path B
    state_b = {"intent": "task", "confidence": 0.8}
    assert route_based_on_intent(state_b) == "task_node"
    
    # Test default
    state_c = {"intent": "unknown"}
    assert route_based_on_intent(state_c) == "fallback_node"

def test_loop_termination():
    """Test that loops eventually exit"""
    state = {"max_iterations": 10, "goal_achieved": False}
    assert should_continue_loop(state) == "end"
    
    state = {"max_iterations": 5, "goal_achieved": True}
    assert should_continue_loop(state) == "end"
```

### Best Practices

**Edge Design Principles:**

```python
# 1. Clear routing logic
def clear_router(state: State) -> str:
    """Explicit, readable conditions"""
    # Bad: complex nested ifs
    # Good: clear logical flow
    
    if is_simple_question(state):
        return "simple_answer"
    
    if requires_research(state):
        return "research_path"
    
    return "general_response"

# 2. Deterministic when possible
def deterministic_router(state: State) -> str:
    """Same state → same route"""
    # Easier to test and debug
    return route_map[state["category"]]

# 3. Handle all cases
def complete_router(state: State) -> str:
    """Always return valid route"""
    intent = state.get("intent")
    
    # Explicit cases
    if intent == "A": return "node_a"
    if intent == "B": return "node_b"
    
    # Always have default
    return "default_node"

# 4. Log routing decisions
import logging
logger = logging.getLogger(__name__)

def logged_router(state: State) -> str:
    """Log routing for debugging"""
    route = determine_route(state)
    logger.info(f"Routing to {route}", extra={
        "state_summary": summarize(state),
        "route": route
    })
    return route
```

### Interview Talking Points

- Edges determine transitions between nodes
- Regular edges for fixed paths, conditional for dynamic
- Router functions evaluate state and return next node
- Loops enabled by routing back to previous nodes
- Human-in-the-loop via conditional routing with interrupts
- Error handling through routing logic
- Routing logic should be testable and deterministic
- Always handle default/fallback cases

**One-liner:** "Edges decide how control moves between nodes."

---

## State Management

### Interview Learning Goals

Explain how shared memory works and how state carries data across graph steps.

### What is State?

State in LangGraph is the shared data structure that flows through the graph, carrying information between nodes. It's the "memory" of the agent.

### State Schema

**Defining State:**

```python
from typing import TypedDict, Annotated
from operator import add

# Basic state
class BasicState(TypedDict):
    input: str
    output: str

# State with annotations (reducers)
class AnnotatedState(TypedDict):
    # Simple fields
    question: str
    answer: str
    
    # Accumulated fields (using reducer)
    messages: Annotated[list[str], add]
    # add operator appends instead of replacing
    
    # Computed fields
    iteration: int
```

### State Updates

**How State Changes:**

```python
# Initial state
initial = {"input": "Hello", "counter": 0}

# Node returns partial update
def node1(state):
    return {"counter": state["counter"] + 1}
# Result: {"input": "Hello", "counter": 1}

# Next node updates different key
def node2(state):
    return {"output": f"Processed: {state['input']}"}
# Result: {"input": "Hello", "counter": 1, "output": "Processed: Hello"}

# Updates are merged with existing state
```

### Reducers

**Custom State Merging:**

```python
from typing import Annotated
from operator import add

# Built-in reducers
class State(TypedDict):
    # Default: replace
    name: str
    
    # add: append to list
    messages: Annotated[list, add]
    
    # Custom reducer
    count: Annotated[int, lambda x, y: x + y]

# Custom reducer function
def merge_dicts(left: dict, right: dict) -> dict:
    """Custom merge logic"""
    return {**left, **right}

class StateWithCustom(TypedDict):
    metadata: Annotated[dict, merge_dicts]

# Usage in nodes
def node(state: State) -> dict:
    return {
        "messages": ["new message"],  # Appended
        "name": "Updated",  # Replaced
        "count": 1  # Added to existing
    }
```

### Common Reducer Patterns

**Useful Reducers:**

```python
from operator import add
from typing import Annotated

# 1. Accumulate messages
messages: Annotated[list, add]

# 2. Track history
history: Annotated[list[dict], add]

# 3. Collect errors
errors: Annotated[list[str], add]

# 4. Aggregate scores
scores: Annotated[list[float], add]

# 5. Merge metadata
def merge_metadata(left: dict, right: dict) -> dict:
    """Deep merge with conflict resolution"""
    result = left.copy()
    for key, value in right.items():
        if key in result and isinstance(result[key], dict):
            result[key] = merge_metadata(result[key], value)
        else:
            result[key] = value
    return result

metadata: Annotated[dict, merge_metadata]

# 6. Keep latest with timestamp
def keep_latest(left: tuple, right: tuple) -> tuple:
    """Keep value with latest timestamp"""
    if right[1] > left[1]:  # Compare timestamps
        return right
    return left

value_with_time: Annotated[tuple, keep_latest]
```

### Immutability

**State Mutation Patterns:**

```python
# Bad: Mutating state directly
def bad_node(state: State) -> dict:
    state["messages"].append("New")  # Don't do this!
    return {}

# Good: Return new values
def good_node(state: State) -> dict:
    return {
        "messages": state["messages"] + ["New"]
    }

# Good: With reducer
def good_node_with_reducer(state: State) -> dict:
    # Reducer handles appending
    return {
        "messages": ["New"]
    }
```

### Complex State Structures

**Nested State:**

```python
from dataclasses import dataclass
from typing import Optional

@dataclass
class User:
    id: str
    name: str
    email: str

@dataclass
class Task:
    id: str
    title: str
    status: str
    assigned_to: Optional[User] = None

class ComplexState(TypedDict):
    # Scalar values
    session_id: str
    iteration: int
    
    # Structured data
    user: User
    current_task: Optional[Task]
    
    # Collections
    tasks: list[Task]
    messages: Annotated[list[str], add]
    
    # Metadata
    metadata: dict
    errors: Annotated[list[str], add]

# Usage
def node(state: ComplexState) -> dict:
    user = state["user"]
    task = Task(
        id="task-1",
        title="New Task",
        status="pending",
        assigned_to=user
    )
    return {
        "current_task": task,
        "tasks": state["tasks"] + [task]
    }
```

### State Validation

**Ensuring State Integrity:**

```python
from pydantic import BaseModel, validator

class ValidatedState(BaseModel):
    """Use Pydantic for validation"""
    count: int
    message: str
    confidence: float
    
    @validator("confidence")
    def confidence_range(cls, v):
        if not 0 <= v <= 1:
            raise ValueError("Confidence must be 0-1")
        return v
    
    @validator("count")
    def count_positive(cls, v):
        if v < 0:
            raise ValueError("Count must be non-negative")
        return v

# In node
def validated_node(state: dict) -> dict:
    # Validate before processing
    validated = ValidatedState(**state)
    
    # Process
    result = process(validated)
    
    # Return dict
    return result.dict()
```

### State Persistence

**Checkpoint Management:**

```python
from langgraph.checkpoint.sqlite import SqliteSaver

# Create checkpointer
memory = SqliteSaver.from_conn_string(":memory:")

# Compile with persistence
app = workflow.compile(checkpointer=memory)

# State automatically saved at each step
config = {"configurable": {"thread_id": "user-123"}}

# First invocation
result1 = app.invoke({"input": "Hello"}, config)

# Continue from checkpoint
result2 = app.invoke({"input": "Continue"}, config)
# State from result1 is preserved
```

### State Access Patterns

**Reading State:**

```python
def node(state: State) -> dict:
    # Direct access
    value = state["key"]
    
    # Safe access with default
    value = state.get("key", "default")
    
    # Check existence
    if "key" in state:
        value = state["key"]
    
    # Destructuring
    input_val = state["input"]
    count = state.get("count", 0)
    
    return {"output": f"{input_val} (count: {count})"}
```

### State Debugging

**Inspecting State:**

```python
import json
import logging

logger = logging.getLogger(__name__)

def debug_node(state: State) -> dict:
    """Log state for debugging"""
    logger.debug(f"Current state: {json.dumps(state, indent=2)}")
    
    # Process
    result = process(state)
    
    logger.debug(f"State updates: {json.dumps(result, indent=2)}")
    
    return result

# Get state history
def get_state_history(app, config):
    """Retrieve all state snapshots"""
    history = []
    for state in app.get_state_history(config):
        history.append(state)
    return history
```

### Interview Talking Points

- State is shared memory flowing through graph
- TypedDict defines state schema
- Reducers control how state updates merge
- State should be treated as immutable
- Checkpointers automatically persist state
- Annotations enable custom merge logic
- Complex nested structures supported
- State validation prevents runtime errors

**One-liner:** "State carries data across graph steps."

---

## Execution & Control Flow

### Interview Learning Goals

Demonstrate how LangGraph executes graphs with persistent control and recovery.

### Invocation Methods

**Ways to Execute:**

```python
app = workflow.compile()

# 1. Synchronous invoke - run to completion
result = app.invoke({"input": "Hello"})

# 2. Asynchronous invoke
result = await app.ainvoke({"input": "Hello"})

# 3. Streaming - get intermediate results
for chunk in app.stream({"input": "Hello"}):
    print(chunk)

# 4. Async streaming
async for chunk in app.astream({"input": "Hello"}):
    print(chunk)
```

### Streaming Execution

**Real-Time Updates:**

```python
# Stream node outputs
for output in app.stream({"messages": ["Hello"]}):
    for key, value in output.items():
        print(f"Node '{key}': {value}")

# Example output:
# Node 'agent': {'messages': [AIMessage(content='...')]}
# Node 'tools': {'messages': [ToolMessage(content='...')]}
# Node 'agent': {'messages': [AIMessage(content='Final answer')]}
```

**Stream Modes:**

```python
# Mode 1: values - Full state after each node
for chunk in app.stream(input, stream_mode="values"):
    print(chunk)  # Complete state

# Mode 2: updates - Only node updates
for chunk in app.stream(input, stream_mode="updates"):
    print(chunk)  # Just what changed

# Mode 3: debug - All internal details
for chunk in app.stream(input, stream_mode="debug"):
    print(chunk)  # Full debug info
```

### Checkpointing

**Persistent Execution:**

```python
from langgraph.checkpoint.sqlite import SqliteSaver

# Setup persistence
memory = SqliteSaver.from_conn_string("checkpoints.db")
app = workflow.compile(checkpointer=memory)

# Execute with thread ID
config = {"configurable": {"thread_id": "conversation-123"}}

# First call - creates checkpoint
result1 = app.invoke({"input": "Hello"}, config)

# Second call - resumes from checkpoint
result2 = app.invoke({"input": "Continue"}, config)
# State from result1 is preserved
```

### Checkpoint Management

**Working with Checkpoints:**

```python
# Get current state
current_state = app.get_state(config)
print(current_state.values)  # Current state dict
print(current_state.next)  # Next nodes to execute

# Get state history
history = app.get_state_history(config)
for state in history:
    print(f"Step {state.metadata['step']}: {state.values}")

# Time-travel to previous state
past_config = {"configurable": {"thread_id": "conversation-123", "checkpoint_id": "checkpoint-5"}}
result = app.invoke({"input": "New input"}, past_config)
```

### Interrupts and Human-in-the-Loop

**Pausing Execution:**

```python
# Compile with interrupt points
app = workflow.compile(
    checkpointer=memory,
    interrupt_before=["human_review"],  # Pause before
    interrupt_after=["critical_decision"]  # Pause after
)

# First invocation - runs until interrupt
result = app.invoke({"input": "Process this"}, config)
print(result)  # {'__interrupt__': {...}}

# Check what's next
state = app.get_state(config)
print(state.next)  # ['human_review']

# Resume after human input
result = app.invoke({"human_feedback": "Approved"}, config)
```

**Human Feedback Pattern:**

```python
def human_review_workflow():
    workflow = StateGraph(State)
    
    workflow.add_node("process", process_node)
    workflow.add_node("human_review", human_node)
    workflow.add_node("finalize", finalize_node)
    
    workflow.add_edge("process", "human_review")
    workflow.add_edge("human_review", "finalize")
    
    memory = SqliteSaver.from_conn_string(":memory:")
    return workflow.compile(
        checkpointer=memory,
        interrupt_before=["human_review"]
    )

# Usage
app = human_review_workflow()
config = {"configurable": {"thread_id": "review-1"}}

# Start process
result = app.invoke({"document": "Draft content"}, config)

# Later: Human reviews and approves
result = app.invoke({"approved": True}, config)
```

### Retry Logic

**Error Recovery:**

```python
class State(TypedDict):
    input: str
    output: str
    retry_count: int
    error: Optional[str]

def node_with_retry(state: State) -> dict:
    try:
        result = risky_operation(state["input"])
        return {"output": result, "error": None}
    except Exception as e:
        return {
            "error": str(e),
            "retry_count": state.get("retry_count", 0) + 1
        }

def should_retry(state: State) -> str:
    if state.get("error") and state.get("retry_count", 0) < 3:
        return "retry"
    elif state.get("error"):
        return "failed"
    else:
        return "success"

# Build graph with retry
workflow.add_node("operation", node_with_retry)
workflow.add_conditional_edges(
    "operation",
    should_retry,
    {
        "retry": "operation",  # Loop back
        "failed": "error_handler",
        "success": END
    }
)
```

### Timeout Handling

**Time-Limited Execution:**

```python
import asyncio
from typing import Optional

async def execute_with_timeout(
    app,
    input_data: dict,
    config: dict,
    timeout: int = 30
) -> Optional[dict]:
    """Execute graph with timeout"""
    try:
        result = await asyncio.wait_for(
            app.ainvoke(input_data, config),
            timeout=timeout
        )
        return result
    except asyncio.TimeoutError:
        logger.error(f"Execution timed out after {timeout}s")
        return None

# Usage
result = await execute_with_timeout(
    app,
    {"input": "Process this"},
    config,
    timeout=60
)
```

### Parallel Execution

**Concurrent Node Processing:**

```python
# LangGraph automatically parallelizes independent nodes

def create_parallel_workflow():
    workflow = StateGraph(State)
    
    # These can run in parallel
    workflow.add_node("search_web", search_node)
    workflow.add_node("search_db", db_node)
    workflow.add_node("calculate", calc_node)
    
    # Merge results
    workflow.add_node("combine", combine_node)
    
    # All three search nodes can run concurrently
    workflow.add_edge("search_web", "combine")
    workflow.add_edge("search_db", "combine")
    workflow.add_edge("calculate", "combine")
    
    return workflow.compile()

# LangGraph handles parallelization automatically
```

### Configuration

**Runtime Configuration:**

```python
# Thread-specific config
config = {
    "configurable": {
        "thread_id": "user-123",
        "checkpoint_id": "step-5",  # Optional: specific checkpoint
        "model_name": "gpt-4",  # Custom config
        "temperature": 0.7
    }
}

# Access config in nodes
def configurable_node(state: State, config: dict) -> dict:
    """Node can access runtime config"""
    model_name = config.get("configurable", {}).get("model_name", "gpt-3.5")
    temperature = config.get("configurable", {}).get("temperature", 0.5)
    
    # Use config
    model = ChatOpenAI(model=model_name, temperature=temperature)
    response = model.invoke(state["input"])
    
    return {"output": response.content}
```

### Monitoring Execution

**Observability:**

```python
import logging
from datetime import datetime

logger = logging.getLogger(__name__)

def monitored_invoke(app, input_data, config):
    """Execute with monitoring"""
    start = datetime.now()
    
    try:
        logger.info(f"Starting execution", extra={
            "thread_id": config.get("configurable", {}).get("thread_id"),
            "input_keys": list(input_data.keys())
        })
        
        result = app.invoke(input_data, config)
        
        duration = (datetime.now() - start).total_seconds()
        logger.info(f"Execution completed in {duration}s", extra={
            "duration": duration,
            "output_keys": list(result.keys())
        })
        
        return result
        
    except Exception as e:
        logger.exception("Execution failed", extra={
            "error": str(e),
            "duration": (datetime.now() - start).total_seconds()
        })
        raise
```

### LangSmith Integration

**Tracing with LangSmith:**

```python
import os

# Enable tracing
os.environ["LANGCHAIN_TRACING_V2"] = "true"
os.environ["LANGCHAIN_API_KEY"] = "your-api-key"
os.environ["LANGCHAIN_PROJECT"] = "my-project"

# Execute - automatically traces
result = app.invoke({"input": "Hello"}, config)

# View traces at https://smith.langchain.com
```

### Interview Talking Points

- Multiple invocation methods: invoke, stream, async variants
- Streaming provides real-time intermediate updates
- Checkpointing enables persistence and resumability
- Human-in-the-loop via interrupts before/after nodes
- Automatic retry and error recovery patterns
- Parallel execution handled automatically
- Configuration passed at runtime
- LangSmith integration for observability

**One-liner:** "LangGraph executes graphs with persistent control and recovery."

---

## LangGraph vs LangChain Chains

### Interview Learning Goals

Articulate differences and choose appropriate abstraction.

### Fundamental Differences

**Architecture Comparison:**

```
LangChain Chains:                LangGraph:
Input                            Input
  ↓                                ↓
LLM Call                         Node1 (LLM)
  ↓                                ↓
Output Parser                    Node2 (Tool)
  ↓                                ↓
Output                           Node3 (Decision)
                                   ↓
(Linear, DAG only)              Output

                                (Cyclical, stateful)
```

### LangChain Chains

**When to Use Chains:**

```python
from langchain.chains import LLMChain
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate

# Simple, linear workflows
model = ChatOpenAI()
prompt = ChatPromptTemplate.from_template("Translate {text} to {language}")

chain = prompt | model

result = chain.invoke({"text": "Hello", "language": "Spanish"})
# Simple: Input → Transform → Output
```

**Chain Characteristics:**

- Linear or DAG (no cycles)
- Stateless by default
- Quick to build
- Less control over flow
- Good for simple tasks

### LangGraph Workflows

**When to Use LangGraph:**

```python
from langgraph.graph import StateGraph
from langgraph.prebuilt import create_react_agent

# Complex, stateful workflows
tools = [search_tool, calculator_tool]
model = ChatOpenAI()

# Agent can loop, branch, maintain state
agent = create_react_agent(model, tools)

result = agent.invoke({
    "messages": [("human", "What's 2+2? Then search for that number")]
})
# Complex: Loops, branching, tool use
```

**LangGraph Characteristics:**

- Cyclical workflows (loops)
- Stateful execution
- Full control over flow
- Human-in-the-loop support
- More complex to build
- Production-ready durability

### Feature Comparison

**Capability Matrix:**

|Feature|LangChain Chains|LangGraph|
|---|---|---|
|Cycles/Loops|✗|✓|
|Conditional Branching|Limited|✓|
|Persistent State|✗ (manual)|✓ (built-in)|
|Checkpointing|✗|✓|
|Human-in-the-Loop|✗|✓|
|Streaming|✓|✓|
|Async Support|✓|✓|
|Time Travel|✗|✓|
|Tool Loops|Complex|Native|
|Setup Complexity|Low|Medium|
|Control Level|High-level|Low-level|

### When Chains Are Better

**Use LangChain Chains For:**

```python
# 1. Simple transformations
text | translator | output

# 2. Quick prototypes
chain = prompt | model | parser

# 3. Single LLM calls
retrieval_qa = RetrievalQA.from_llm(llm, retriever)

# 4. No loops needed
summarization_chain = load_summarize_chain(llm)

# 5. Minimal state
simple_chain.invoke({"input": "text"})
```

### When LangGraph Is Better

**Use LangGraph For:**

```python
# 1. Agent tool loops
agent = create_react_agent(model, tools)
# Agent calls tool, evaluates, may call again

# 2. Multi-step reasoning
# Research → Analyze → Draft → Review → Finalize

# 3. Human-in-the-loop
# Process → Pause for approval → Continue

# 4. Error recovery
# Try → Fail → Retry with different approach

# 5. Complex branching
# Classify → Route to specialized agents → Merge
```

### Migration Path

**From Chains to LangGraph:**

```python
# Before: Simple chain
from langchain.chains import LLMChain

chain = LLMChain(llm=model, prompt=prompt)
result = chain.run("What is AI?")

# After: LangGraph (more control)
from langgraph.graph import StateGraph

class State(TypedDict):
    question: str
    answer: str

def llm_node(state: State) -> dict:
    response = model.invoke(prompt.format(**state))
    return {"answer": response.content}

workflow = StateGraph(State)
workflow.add_node("llm", llm_node)
workflow.set_entry_point("llm")
workflow.set_finish_point("llm")

app = workflow.compile()
result = app.invoke({"question": "What is AI?"})
```

### Hybrid Approach

**Using Both Together:**

```python
from langchain.chains import LLMChain
from langgraph.graph import StateGraph

# LangChain chain for specific task
summary_chain = load_summarize_chain(llm)

# Use chain within LangGraph node
def summarize_node(state: State) -> dict:
    # Use LangChain chain in LangGraph
    summary = summary_chain.run(state["documents"])
    return {"summary": summary}

workflow = StateGraph(State)
workflow.add_node("summarize", summarize_node)
workflow.add_node("analyze", analyze_node)
workflow.add_edge("summarize", "analyze")

app = workflow.compile()
```

### Performance Considerations

**Chains vs Graphs:**

```python
# Chains: Lower overhead for simple tasks
chain_start = time.time()
chain_result = chain.invoke(input)
chain_time = time.time() - chain_start
# ~100ms for simple task

# LangGraph: Higher overhead, but worth it for complexity
graph_start = time.time()
graph_result = app.invoke(input, config)
graph_time = time.time() - graph_start
# ~150ms for simple task
# But enables features chains can't do
```

### Code Complexity

**Simplicity vs Control:**

```python
# Chain: 5 lines
chain = prompt | model | parser
result = chain.invoke(input)

# Graph: 15+ lines
workflow = StateGraph(State)
workflow.add_node("node1", func1)
workflow.add_node("node2", func2)
workflow.add_edge("node1", "node2")
workflow.set_entry_point("node1")
workflow.set_finish_point("node2")
app = workflow.compile()
result = app.invoke(input)

# Trade-off: Simplicity vs capabilities
```

### Interview Talking Points

- Chains for simple, linear workflows
- LangGraph for complex, stateful agents
- Chains: easier setup, less control
- LangGraph: more setup, full control
- LangGraph enables loops, chains don't
- Use chains inside LangGraph nodes (hybrid)
- Performance overhead justified by capabilities
- Choose based on workflow complexity, not familiarity

**One-liner:** "Use LangGraph when workflows need loops and state beyond simple chains."

---

## When to Use LangGraph

### Interview Learning Goals

Determine project fit and justify LangGraph adoption.

### Ideal Use Cases

**LangGraph Excels At:**

1. **Multi-Step Agents**

```python
# Complex reasoning workflows
Research → Analyze → Plan → Execute → Review → Iterate

# Example: Code generation agent
Understand Task → Search Docs → Draft Code → Test → Fix → Deploy
```

2. **Tool Loops**

```python
# Agent-tool interaction cycles
Agent: "I need to search"
  → Tool: Search results
Agent: "Calculate from results"
  → Tool: Calculation
Agent: "Final answer"

# Continues until task complete
```

3. **Human-in-the-Loop**

```python
# Workflows requiring human approval
Draft Content → Human Review → [Approve/Reject] → Publish

# Customer support
AI Response → Low Confidence? → Human Agent → Continue
```

4. **Stateful Conversations**

```python
# Long-running conversations with memory
Session 1: "My name is John"
Session 2: "What's my name?" → "John"

# Checkpoints preserve context
```

5. **Complex Decision Trees**

```python
# Multi-path routing
Classify → [Support | Sales | Technical] → Specialized Handler
```

### Real-World Applications

**Production Use Cases:**

```python
# 1. Customer Support Agent
Classify Intent → Route to Handler → Execute Action → Follow-up

# 2. Research Assistant
Query → Search Multiple Sources → Synthesize → Fact-Check → Report

# 3. Code Review Agent
Analyze Code → Run Tests → Security Check → Performance Review → Report

# 4. Data Processing Pipeline
Extract → Transform → Validate → Human Review → Load

# 5. Content Generation
Topic → Research → Outline → Draft → Edit → Human Review → Publish
```

### When NOT to Use LangGraph

**Better Alternatives:**

```python
# 1. Simple LLM Calls
# Use: LangChain Chain
chain = prompt | model
# Not: LangGraph with single node

# 2. Static Workflows
# Use: Traditional orchestration (Airflow, Prefect)
# Not: LangGraph for data pipelines

# 3. No State Needed
# Use: Stateless functions
def process(input): return transform(input)
# Not: LangGraph state management

# 4. Pure Retrieval QA
# Use: LangChain RetrievalQA
qa = RetrievalQA.from_llm(llm, retriever)
# Not: LangGraph unless need loops

# 5. Batch Processing
# Use: Async batch processing
results = await asyncio.gather(*tasks)
# Not: LangGraph unless need control flow
```

### Decision Framework

**Evaluation Questions:**

```
1. Does workflow need cycles/loops?
   Yes → LangGraph
   No → Consider LangChain Chains

2. Is state persistence required?
   Yes → LangGraph
   No → Stateless functions may suffice

3. Human-in-the-loop needed?
   Yes → LangGraph (native support)
   No → Other options viable

4. Multi-step with branching?
   Yes → LangGraph
   No → Linear chains work

5. Error recovery important?
   Yes → LangGraph (checkpointing)
   No → Simple retry logic enough

If 2+ answers are "Yes" → LangGraph is strong fit
```

### Complexity vs Value

**Cost-Benefit Analysis:**

```python
# Low Complexity Task
Input → LLM → Output

LangChain Chain:
- Setup: 5 minutes
- Code: 5 lines
- Maintenance: Easy

LangGraph:
- Setup: 20 minutes
- Code: 20+ lines
- Maintenance: Moderate

Verdict: Chain wins

# High Complexity Task
Input → Agent Loop → Tools → Decisions → Human Review → Output

LangChain:
- Setup: Hard (manual state)
- Code: 100+ lines
- Maintenance: Hard

LangGraph:
- Setup: 30 minutes
- Code: 50 lines
- Maintenance: Moderate

Verdict: LangGraph wins
```

### Team Considerations

**Skill Requirements:**

```python
# LangGraph requires:
✓ Python proficiency
✓ Understanding of graphs/state machines
✓ Async programming knowledge
✓ LangChain familiarity (helpful)
✓ Debugging complex workflows

# Consider team capabilities when choosing
```

### Scale Considerations

**Production Factors:**

```python
# LangGraph at Scale:

Advantages:
✓ Built-in checkpointing (durability)
✓ Streaming (responsiveness)
✓ Error recovery (reliability)
✓ Monitoring hooks (observability)

Challenges:
⚠ Checkpoint storage management
⚠ Graph complexity grows
⚠ Debugging distributed state
⚠ Performance tuning

# Use when scale benefits justify complexity
```

### Migration Checklist

**Adopting LangGraph:**

```
Before Starting:
☐ Current approach inadequate?
☐ Complexity justified?
☐ Team has required skills?
☐ Observability plan in place?
☐ Testing strategy defined?

During Development:
☐ Start simple, add complexity gradually
☐ Test nodes independently
☐ Monitor checkpoint storage
☐ Use LangSmith for debugging
☐ Document graph structure

Production Ready:
☐ Error handling comprehensive
☐ Checkpointing configured
☐ Monitoring/alerting set up
☐ Performance tested
☐ Rollback plan exists
```

### Interview Talking Points

- Use for multi-step agents with tool loops
- Ideal for human-in-the-loop workflows
- Overkill for simple LLM calls
- Requires state persistence and complexity justification
- Team skill level matters
- Production benefits justify learning curve
- Start simple, grow complexity as needed
- Alternative tools for static pipelines

**One-liner:** "LangGraph fits complex, stateful agent systems."

---

## Best Practices & Pitfalls

### Interview Learning Goals

Apply production-ready patterns and avoid common mistakes.

### Best Practices

#### 1. Modular Node Design

**Keep Nodes Focused:**

```python
# Bad: Monolithic node
def giant_node(state):
    # 100 lines of code
    # Multiple responsibilities
    # Hard to test
    # Hard to debug
    pass

# Good: Focused nodes
def classify(state):
    """Single responsibility: classify intent"""
    return {"intent": classifier(state["input"])}

def route(state):
    """Single responsibility: determine route"""
    return {"next_action": router(state["intent"])}

def execute(state):
    """Single responsibility: execute action"""
    return {"result": executor(state["next_action"])}
```

#### 2. Small State

**Minimize State Size:**

```python
# Bad: Bloated state
class BadState(TypedDict):
    full_conversation_history: list  # 1000s of messages
    all_search_results: list  # Megabytes of data
    complete_database_dump: dict
    every_intermediate_step: list

# Good: Essential state only
class GoodState(TypedDict):
    current_query: str
    relevant_context: str  # Summarized
    answer: str
    metadata: dict  # Minimal tracking

# Store large data externally if needed
```

#### 3. Comprehensive Logging

**Debug-Friendly Logging:**

```python
import logging
import json

logger = logging.getLogger(__name__)

def well_logged_node(state: State) -> dict:
    """Node with good logging"""
    
    # Log entry
    logger.info(
        f"Entering node",
        extra={
            "node": "well_logged_node",
            "state_keys": list(state.keys()),
            "thread_id": state.get("thread_id")
        }
    )
    
    try:
        # Process
        result = process(state)
        
        # Log success
        logger.info(
            "Node completed successfully",
            extra={"output_keys": list(result.keys())}
        )
        
        return result
        
    except Exception as e:
        # Log error
        logger.exception(
            "Node failed",
            extra={
                "error_type": type(e).__name__,
                "error_msg": str(e),
                "state": json.dumps(state, default=str)
            }
        )
        raise
```

#### 4. Thorough Testing

**Test at Multiple Levels:**

```python
# Unit test: Individual nodes
def test_classify_node():
    state = {"input": "hello"}
    result = classify_node(state)
    assert "intent" in result
    assert result["intent"] in ["greeting", "question", "command"]

# Integration test: Node sequences
def test_classify_and_route():
    state = {"input": "What's the weather?"}
    state = classify_node(state)
    state = {**state, **route_node(state)}
    assert state["next_action"] == "weather_query"

# End-to-end test: Full graph
def test_complete_workflow():
    app = create_app()
    config = {"configurable": {"thread_id": "test-1"}}
    
    result = app.invoke({"input": "Test query"}, config)
    
    assert "answer" in result
    assert result["answer"] is not None

# Property test: State invariants
def test_state_consistency():
    """Ensure state remains valid"""
    state = {"count": 0}
    for i in range(10):
        state = {**state, **increment_node(state)}
        assert state["count"] == i + 1
        assert state["count"] >= 0  # Invariant
```

#### 5. Error Boundaries

**Graceful Degradation:**

```python
def error_safe_node(state: State) -> dict:
    """Node with error boundary"""
    try:
        result = risky_operation(state)
        return {
            "result": result,
            "status": "success",
            "error": None
        }
    except SpecificError as e:
        # Handle specific errors
        logger.warning(f"Specific error: {e}")
        return {
            "result": fallback_value(),
            "status": "degraded",
            "error": str(e)
        }
    except Exception as e:
        # Catch-all
        logger.exception("Unexpected error")
        return {
            "result": None,
            "status": "failed",
            "error": "Internal error"
        }

# Router can handle degraded state
def error_aware_router(state: State) -> str:
    if state["status"] == "success":
        return "continue"
    elif state["status"] == "degraded":
        return "retry_with_fallback"
    else:
        return "error_handler"
```

#### 6. Configuration Management

**Externalize Configuration:**

```python
# config.py
from pydantic_settings import BaseSettings

class AppConfig(BaseSettings):
    # Model settings
    MODEL_NAME: str = "gpt-4"
    TEMPERATURE: float = 0.7
    MAX_TOKENS: int = 1000
    
    # Application settings
    MAX_RETRIES: int = 3
    TIMEOUT_SECONDS: int = 30
    
    # Storage
    CHECKPOINT_DB: str = "sqlite:///checkpoints.db"
    
    class Config:
        env_file = ".env"

config = AppConfig()

# Use in nodes
def configurable_node(state: State) -> dict:
    model = ChatOpenAI(
        model=config.MODEL_NAME,
        temperature=config.TEMPERATURE
    )
    # ...
```

### Common Pitfalls

#### Pitfall 1: State Mutation

**Problem:**

```python
# Bad: Mutating state
def bad_node(state: State) -> dict:
    state["messages"].append("new")  # Mutates!
    state["count"] += 1  # Mutates!
    return {}  # Doesn't return updates
```

**Solution:**

```python
# Good: Immutable updates
def good_node(state: State) -> dict:
    return {
        "messages": state["messages"] + ["new"],
        "count": state["count"] + 1
    }
```

#### Pitfall 2: Infinite Loops

**Problem:**

```python
# Bad: No exit condition
def loop_router(state: State) -> str:
    return "loop_node"  # Always loops!

workflow.add_conditional_edges(
    "loop_node",
    loop_router,
    {"loop_node": "loop_node"}
)
```

**Solution:**

```python
# Good: Clear termination
def safe_router(state: State) -> str:
    if state["iterations"] >= MAX_ITERATIONS:
        return "end"
    if state["goal_achieved"]:
        return "end"
    return "continue"

workflow.add_conditional_edges(
    "loop_node",
    safe_router,
    {
        "continue": "loop_node",
        "end": END
    }
)
```

#### Pitfall 3: Missing Error Handling

**Problem:**

```python
# Bad: No error handling
def fragile_node(state: State) -> dict:
    result = api_call(state["input"])  # Can fail!
    return {"result": result}
```

**Solution:**

```python
# Good: Robust error handling
def robust_node(state: State) -> dict:
    try:
        result = api_call(state["input"])
        return {"result": result, "error": None}
    except APIError as e:
        return {"result": None, "error": str(e)}
```

#### Pitfall 4: Ignoring Checkpointing

**Problem:**

```python
# Bad: No persistence
app = workflow.compile()  # State lost on restart
```

**Solution:**

```python
# Good: Enable checkpointing
from langgraph.checkpoint.sqlite import SqliteSaver

memory = SqliteSaver.from_conn_string("checkpoints.db")
app = workflow.compile(checkpointer=memory)
```

#### Pitfall 5: Over-Complex Graphs

**Problem:**

```python
# Bad: 20+ nodes, complex routing
workflow.add_node("node1", ...)
workflow.add_node("node2", ...)
# ... 18 more nodes
workflow.add_conditional_edges(...)  # Complex routing
```

**Solution:**

```python
# Good: Modular sub-graphs
def create_subgraph_1():
    sub = StateGraph(SubState)
    # 3-4 related nodes
    return sub.compile()

def create_subgraph_2():
    sub = StateGraph(SubState)
    # 3-4 related nodes
    return sub.compile()

# Main graph uses sub-graphs
main_workflow = StateGraph(MainState)
main_workflow.add_node("phase1", create_subgraph_1())
main_workflow.add_node("phase2", create_subgraph_2())
```

#### Pitfall 6: Poor State Design

**Problem:**

```python
# Bad: Flat state with everything
class BadState(TypedDict):
    user_input: str
    intent: str
    tool_result1: str
    tool_result2: str
    temp_var1: str
    temp_var2: str
    # 20 more fields...
```

**Solution:**

```python
# Good: Structured state
class GoodState(TypedDict):
    input: UserInput  # Structured
    context: Context  # Grouped related data
    results: Results  # Clear purpose
    metadata: Metadata  # Tracking info
```

#### Pitfall 7: Neglecting Observability

**Problem:**

```python
# Bad: No monitoring
result = app.invoke(input, config)
# Can't debug issues
```

**Solution:**

```python
# Good: Full observability
import os

# Enable LangSmith
os.environ["LANGCHAIN_TRACING_V2"] = "true"
os.environ["LANGCHAIN_PROJECT"] = "my-project"

# Add logging
logger.info(f"Executing workflow", extra={"config": config})

result = app.invoke(input, config)

# Monitor execution
state_history = app.get_state_history(config)
for state in state_history:
    logger.debug(f"Step: {state.metadata}")
```

### Production Checklist

**Before Deploying:**

```
Code Quality:
☐ Nodes are focused and testable
☐ Error handling comprehensive
☐ Logging at appropriate levels
☐ Configuration externalized
☐ Tests cover critical paths

Architecture:
☐ State size minimized
☐ Graph complexity manageable
☐ Sub-graphs used for modularity
☐ Clear termination conditions
☐ Timeout handling implemented

Operations:
☐ Checkpointing enabled
☐ Monitoring/alerting configured
☐ LangSmith tracing active
☐ Performance benchmarked
☐ Rollback plan documented

Documentation:
☐ Graph structure documented
☐ State schema defined
☐ Node responsibilities clear
☐ Error handling documented
☐ Configuration options listed
```

### Performance Tips

**Optimization Strategies:**

```python
# 1. Minimize state size
def compact_state(state: State) -> dict:
    """Keep only essential data"""
    return {
        "query": state["query"],
        "answer": state["answer"],
        # Remove intermediate_data, debug_info, etc.
    }

# 2. Use async for I/O
async def fast_node(state: State) -> dict:
    results = await asyncio.gather(
        api_call_1(state),
        api_call_2(state),
        api_call_3(state)
    )
    return {"results": results}

# 3. Cache expensive operations
from functools import lru_cache

@lru_cache(maxsize=100)
def expensive_lookup(key: str) -> str:
    # Cached for repeated calls
    return database.query(key)

# 4. Batch operations where possible
def batched_node(state: State) -> dict:
    # Process multiple items together
    items = state["pending_items"]
    results = batch_process(items)  # More efficient
    return {"results": results}
```

### Debugging Strategies

**When Things Go Wrong:**

```python
# 1. Enable debug streaming
for chunk in app.stream(input, stream_mode="debug"):
    print(json.dumps(chunk, indent=2))

# 2. Inspect state at each step
for state in app.get_state_history(config):
    print(f"After {state.metadata['step']}: {state.values}")

# 3. Add debug nodes
def debug_node(state: State) -> dict:
    """Print current state"""
    print(f"Current state: {json.dumps(state, indent=2)}")
    return {}

workflow.add_node("debug", debug_node)
workflow.add_edge("problematic_node", "debug")

# 4. Use LangSmith
# View full trace at smith.langchain.com

# 5. Test nodes in isolation
result = problematic_node(test_state)
assert result == expected
```

### Security Considerations

**Production Safety:**

```python
# 1. Validate input
from pydantic import BaseModel, validator

class SafeInput(BaseModel):
    query: str
    
    @validator("query")
    def no_injection(cls, v):
        if any(bad in v.lower() for bad in ["drop", "delete", "exec"]):
            raise ValueError("Suspicious input")
        return v

# 2. Rate limiting
from ratelimit import limits, sleep_and_retry

@sleep_and_retry
@limits(calls=10, period=60)
def rate_limited_node(state: State) -> dict:
    # Max 10 calls per minute
    pass

# 3. Timeout protection
import signal

def timeout_handler(signum, frame):
    raise TimeoutError("Node exceeded time limit")

def safe_node(state: State) -> dict:
    signal.signal(signal.SIGALRM, timeout_handler)
    signal.alarm(30)  # 30 second limit
    try:
        result = potentially_slow_operation(state)
        signal.alarm(0)  # Cancel alarm
        return result
    except TimeoutError:
        return {"error": "timeout"}

# 4. Sanitize output
def sanitize_output(state: State) -> dict:
    output = state["raw_output"]
    # Remove sensitive data
    cleaned = remove_pii(output)
    return {"output": cleaned}
```

### Interview Talking Points

- Keep nodes modular and focused
- Minimize state size for performance
- Comprehensive logging essential for debugging
- Test at unit, integration, and e2e levels
- Always enable checkpointing in production
- Avoid infinite loops with clear exit conditions
- Use error boundaries for graceful degradation
- Monitor with LangSmith or similar tools
- Security: validate input, rate limit, timeout
- Start simple, add complexity gradually

**One-liner:** "Best practices keep graphs debuggable and robust."

---

## Quick Reference Card

### Essential Commands

```python
# Create graph
from langgraph.graph import StateGraph, END

workflow = StateGraph(StateSchema)
workflow.add_node("name", function)
workflow.add_edge("from", "to")
workflow.add_conditional_edges("from", router, mapping)
workflow.set_entry_point("start")
app = workflow.compile()

# Execute
result = app.invoke(input, config)
for chunk in app.stream(input): print(chunk)

# With persistence
from langgraph.checkpoint.sqlite import SqliteSaver
memory = SqliteSaver.from_conn_string("db.sqlite")
app = workflow.compile(checkpointer=memory)
```

### State Definition

```python
from typing import TypedDict, Annotated
from operator import add

class State(TypedDict):
    field: str  # Replaced on update
    list_field: Annotated[list, add]  # Appended
```

### Node Template

```python
def node(state: State) -> dict:
    """Process state"""
    # Read from state
    input_val = state["key"]
    
    # Process
    result = process(input_val)
    
    # Return updates only
    return {"output": result}
```

### Router Template

```python
def router(state: State) -> str:
    """Determine next node"""
    if condition(state):
        return "path_a"
    return "path_b"

workflow.add_conditional_edges(
    "decision_node",
    router,
    {"path_a": "node_a", "path_b": "node_b"}
)
```

### Common Patterns

```python
# Agent-tool loop
workflow.add_node("agent", agent_fn)
workflow.add_node("tools", tools_fn)
workflow.add_edge("agent", "tools")
workflow.add_conditional_edges(
    "tools",
    should_continue,
    {"continue": "agent", "end": END}
)

# Human-in-the-loop
app = workflow.compile(
    checkpointer=memory,
    interrupt_before=["human_review"]
)

# Error retry
def retry_router(state):
    if state["error"] and state["retries"] < 3:
        return "retry"
    return "continue"
```

### Key Imports

```python
from langgraph.graph import StateGraph, END, MessageGraph
from langgraph.checkpoint.memory import MemorySaver
from langgraph.checkpoint.sqlite import SqliteSaver
from langgraph.prebuilt import create_react_agent, ToolNode
from typing import TypedDict, Annotated
from operator import add
```

---

## Interview Preparation Checklist

```
Core Concepts:
☐ Explain graph-based agent architecture
☐ Describe state management and reducers
☐ Differentiate nodes, edges, routing
☐ Explain checkpointing and persistence
☐ Contrast with LangChain chains

Practical Skills:
☐ Build simple agent from scratch
☐ Implement conditional routing
☐ Add human-in-the-loop
☐ Handle errors and retries
☐ Test nodes independently

Architecture:
☐ Design modular graph structure
☐ Choose appropriate state schema
☐ Implement sub-graphs
☐ Balance complexity vs maintainability

Production:
☐ Enable checkpointing
☐ Add comprehensive logging
☐ Implement error boundaries
☐ Configure observability
☐ Security considerations

Comparison Questions:
☐ When to use LangGraph vs Chains
☐ Advantages over other frameworks
☐ Limitations and trade-offs
☐ Real-world use cases
```

---

## Conclusion

This comprehensive LangGraph doctrine covers all essential aspects for interview preparation:

**Key Takeaways:**

1. **Architecture** - Graph-based, stateful agent workflows
2. **Flexibility** - Loops, branching, human-in-the-loop native
3. **Durability** - Built-in checkpointing and persistence
4. **Production-Ready** - Designed for reliability at scale
5. **Integration** - Works with LangChain ecosystem
6. **Control** - Low-level primitives for full control

**When to Use:**

- Multi-step agents with tool loops
- Human-in-the-loop workflows
- Stateful conversations
- Complex decision trees
- Error recovery requirements

**When NOT to Use:**

- Simple LLM calls
- Static linear workflows
- No state needed
- Pure retrieval QA

**Best Practices:**

- Keep nodes focused and testable
- Minimize state size
- Comprehensive logging
- Error boundaries everywhere
- Enable checkpointing in production

**Study Approach:**

1. Understand core concepts (graphs, nodes, edges, state)
2. Build simple examples from scratch
3. Study real-world patterns (agent loops, HITL)
4. Practice explaining trade-offs
5. Review common pitfalls
6. Stay current with LangGraph updates

Good luck with your interview! 🚀