# Testing Node Functions

**Core Definition:** Verifying node logic in isolation before putting it into the graph.

## The Strategy: "Unit Test First"
Because nodes are just functions, you successfully test them with standard `pytest`.

## Mocking State
You don't need a real graph to test a node. Just pass a dictionary.

```python
# test_agent.py
from src.nodes.agent import agent_node
from src.state import AgentState

def test_agent_node():
    # 1. Arrange
    mock_state = {"messages": [("user", "Hello")], "count": 0}
    
    # 2. Act
    update = agent_node(mock_state)
    
    # 3. Assert
    assert "messages" in update
    assert len(update["messages"]) == 1
```

## Mocking Internals (LLMs)
If your node calls an LLM, use `unittest.mock` to prevent real API calls.

```python
@patch("src.nodes.agent.llm") # Patch the global LLM object
def test_agent_calls_llm(mock_llm):
    mock_llm.invoke.return_value = AIMessage(content="Hi")
    # ... run test ...
```

## Integration vs Unit
-   **Unit:** Test one node function with mocked inputs.
-   **Integration:** Compile the graph and run `graph.invoke()` to test how nodes interact.

## Quick Summary

**1-Line Recall:** **Test nodes as standard Python functions; manually construct the input `state` dict and assert on the returned `update` dict.**
