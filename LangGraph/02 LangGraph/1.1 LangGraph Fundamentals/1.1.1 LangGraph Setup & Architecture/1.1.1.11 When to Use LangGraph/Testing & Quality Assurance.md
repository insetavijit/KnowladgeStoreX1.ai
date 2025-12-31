# Testing & Quality Assurance

## 1. Core Definition
**Testing & Quality Assurance** in LangGraph involves validating both the individual components (nodes) and the orchestrated behavior (edges/routing). Explicit graphs are significantly easier to test than unstructured "agentic loops" because the logic is broken into discrete, testable units.

## 2. Key Technical Details
*   **Unit Testing Nodes**: Since every Node is just a Python function `State -> State`, they can be unit tested with standard tools (pytest) by mocking the input state and asserting the output update.
*   **Integration Testing**: You can test the graph's connectivity by mocking the LLM responses (using `langchain-core.tracers` or simple mocks) and asserting that the graph routes to the expected node.
*   **Determinism**: By fixing the seed or mocking the LLM, you can ensure the graph structure behaves deterministically (e.g., "If score is low, ALWAYS go to revision").
*   **LangGraph Studio**: A visual debugger that allows you to replay past traces, modify state, and step through execution—a massive boost for QA compared to print debugging.

## 3. Mental Model
*   **Visual**: A circuit board tester. You probe specific points (Nodes) to ensure the voltage (State) is correct, rather than just plugging it in and hoping it works.
*   **Analogy**: Testing a car. You test the brakes (Node A), the engine (Node B), and the steering (Edges) separately on a rig before driving on the road.

## 4. Code Example (Unit Testing)
```python
# testing_nodes.py
def test_routing_logic():
    # Setup state
    state = {"score": 0.4}
    
    # Test the function directly (no graph overhead needed for unit test)
    next_node = routing_function(state)
    
    assert next_node == "revise"

def test_graph_flow():
    # Mock the LLM to return a specific "Low Score"
    with mock.patch("model.invoke", return_value="Low Score"):
        final_state = app.invoke(inputs)
        # Assert we visited the revision node
        assert "revision_notes" in final_state
```

## 5. One-Line Recall
LangGraph's modular architecture makes "agent behavior" testable by decomposing it into standard input/output functions.
