# Chain Basics

**Core Definition:** A sequence of calls (Runnables) where the output of step A becomes the input of step B.

## The Mental Model
A **Pipeline**. Data flows in one direction.
`Input -> Step 1 -> Step 2 -> Output`

## Syntax (LCEL)
LangChain Expression Language (LCEL) uses the pipe `|` operator.

```python
chain = prompt | model | parser
```

## Characteristics
1.  **Stateless:** The chain doesn't "remember" anything between runs.
2.  **Implicit Context:** Data is passed via dictionary merging or direct string passing.
3.  **Linear:** No loops. You cannot go back to `Step 1`.

## Quick Summary

**1-Line Recall:** **Chains are linear, stateless pipelines of components suited for simple "Input-Process-Output" tasks.**
