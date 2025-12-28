# Entrypoint & CLI

**Core Definition:** The "Main Door" to your application. How do you actually run the graph?

**The Problem:** You have a `graph` object, but you need a way to invoke it from the terminal or a script.

## The `invoke` Entrypoint

Create a `src/main.py` or script that handles the execution loop.

```python
# src/main.py
from src.graph import graph

def main():
    print("Agent Started. Type 'quit' to exit.")
    while True:
        user_input = input("User: ")
        if user_input.lower() in ["quit", "exit"]:
            break
            
        # Stream events
        for event in graph.stream({"messages": [("human", user_input)]}):
            for value in event.values():
                print("Agent:", value["messages"][-1].content)

if __name__ == "__main__":
    main()
```

## CLI Libraries

Don't parse `sys.argv` manually. Use **Click** or **Typer**.

```python
import typer
app = typer.Typer()

@app.command()
def chat(model: str = "gpt-4"):
    """Run the chat agent."""
    config = {"configurable": {"model": model}}
    # ... run graph with config ...

if __name__ == "__main__":
    app()
```

## Python Module Execution

Run your entrypoint as a module:
`python -m src.main`
(This ensures imports resolve correctly).

## Quick Summary

**1-Line Recall:** **Create a dedicated `main.py` entrypoint that handles the user loop or CLI arguments, separating "running" from "defining".**
