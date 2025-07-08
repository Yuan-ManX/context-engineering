# Context Engineering

Context Engineering - The art of providing all the context for the task to be plausibly solvable by the LLM. To understand context engineering, we must first expand our definition of "context." It isn't just the single prompt you send to an LLM. Think of it as everything the model sees before it generates a response. 

<p align="center">
  <img src="Context-Engineering.png" alt="Context-Engineering" style="display:block; margin:auto; width:650px;" />
</p>


**Instructions / System Prompt**: An initial set of instructions that define the behavior of the model during a conversation, can/should include examples, rules ….

**User Prompt**: Immediate task or question from the user.

**State / History (short-term Memory)**: The current conversation, including user and model responses that have led to this moment.

**Long-Term Memory**: Persistent knowledge base, gathered across many prior conversations, containing learned user preferences, summaries of past projects, or facts it has been told to remember for future use.

**Retrieved Information (RAG)**: External, up-to-date knowledge, relevant information from documents, databases, or APIs to answer specific questions.

**Available Tools**: Definitions of all the functions or built-in tools it can call (e.g., check_inventory, send_email).

**Structured Output**: Definitions on the format of the model's response, e.g. a JSON object.
