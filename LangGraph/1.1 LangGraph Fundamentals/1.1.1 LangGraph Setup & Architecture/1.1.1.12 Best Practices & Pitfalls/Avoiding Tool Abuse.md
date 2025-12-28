# Avoiding Tool Abuse

## 1. Core Definition
**Avoiding Tool Abuse** refers to preventing the agent from calling tools unnecessarily, repetitively, or efficiently. LLMs sometimes "get stuck" calling search 10 times with the same query, or using a tool when they already know the answer.

## 2. Key Technical Details
*   **Tool Constraints**: Limit the number of times a specific tool can be called.
*   **Prompt Engineering**: Explicitly instruct the model in the system prompt: "Only use search if you strictly do not know the answer."
*   **Human-in-the-Loop**: For sensitive tools (Delete Database, Send Email), require human approval to prevent "hallucinated actions."
*   **Result Pruning**: If a tool returns massive JSON, trim it before feeding it back to the LLM to prevent it from getting confused by noise, which often triggers retry loops.

## 3. Mental Model
*   **Visual**: A distracted worker. Instead of doing the job, they keep checking the manual (Tool) over and over for the same page. You need to take the manual away or tell them to focus.
*   **Analogy**: A kid with a hammer. To a hammer, everything looks like a nail. An agent with a Search Tool will try to Search for "What is 2+2" unless you tell it to use its internal math skills.

## 4. One-Line Recall
Constrain tool usage via system prompts and loop limits to prevent agents from wasting money on redundant or unnecessary actions.
