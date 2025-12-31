# Testing Strategies

## 1. Core Definition
**Testing Strategies** for graphs involve a layered approach: Unit Testing (individual nodes), Integration Testing (subgraphs), and End-to-End Testing (full flows). Unlike diverse software, testing agents involves handling non-determinism.

## 2. Key Technical Details
*   **Unit Tests**: Test nodes as pure Python functions. Mock the State input and assert the output dictionary. This verifies *logic* (e.g., "router returns 'retry' on error") without invoking LLMs.
*   **Mocking LLMs**: For integration tests, use mock LLMs that return fixed responses. This ensures your graph wiring is correct without paying for API calls or dealing with random text variations.
*   **Evals (LLM-as-a-Judge)**: For end-to-end quality, run the graph on a dataset of inputs and use another LLM to grade the final response (e.g., "Is this answer accurate?").
*   **Regression Testing**: Keep a set of "Golden Questions" where you know the correct answer. Run these on every PR to ensure the agent hasn't regressed.

## 3. Mental Model
*   **Visual**: The Pyramid of Testing.
    *   Top (Smallest): E2E User Simul (Real LLMs)
    *   Middle: Integration (Mocked LLMs)
    *   Base (Largest): Unit Tests (Pure Logic)
*   **Analogy**: Reviewing a play.
    *   Unit: Actors memorize lines alone.
    *   Integration: Actors rehearse scenes together (no audience).
    *   E2E: Full dress rehearsal.

## 4. Code Example (Unit Test)
```python
def test_router_logic():
    # Arrange
    state = {"messages": [AIMessage(content="", tool_calls=[1])]}
    
    # Act
    next_node = route_tools(state)
    
    # Assert
    assert next_node == "tools"
```

## 5. One-Line Recall
Test logic with mocks (deterministic) and test quality with evals (probabilistic); don't mix the two goals.
