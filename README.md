# Context Engineering

Context Engineering - The art of providing all the context for the task to be plausibly solvable by the LLM. To understand context engineering, we must first expand our definition of "context." It isn't just the single prompt you send to an LLM. Think of it as everything the model sees before it generates a response. 

Andrey Karpathy’s post about this is a great summary: People associate prompts with short task descriptions you'd give an LLM in your day-to-day use. When in every industrial-strength LLM app, context engineering is the delicate art and science of filling the context window with just the right information for the next step.

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


## Context Engineering for Agents

We group common strategies for agent context engineering into four buckets — write, select, compress, and isolate.

<p align="center">
  <img src="General categories of context engineering.png" alt="General categories of context engineering" style="display:block; margin:auto; width:930px;" />
</p>


**Write Context**: Writing context means saving it outside the context window to help an agent perform a task. **Scratchpads** - When humans solve tasks, we take notes and remember things for future, related tasks. Agents are also gaining these capabilities! Note-taking via a “scratchpad” is one approach to persist information while an agent is performing a task. The idea is to save information outside of the context window so that it’s available to the agent. **Memories** - Scratchpads help agents solve a task within a given session (or thread), but sometimes agents benefit from remembering things across many sessions! Reflexion introduced the idea of reflection following each agent turn and re-using these self-generated memories. Generative Agents created memories synthesized periodically from collections of past agent feedback.

**Select Context**: Selecting context means pulling it into the context window to help an agent perform a task. 

**Compressing Context**: Compressing context involves retaining only the tokens required to perform a task. **Context Summarization** - Agent interactions can span hundreds of turns and use token-heavy tool calls. Summarization is one common way to manage these challenges. If you’ve used Claude Code, you’ve seen this in action. Claude Code runs “auto-compact” after you exceed 95% of the context window and it will summarize the full trajectory of user-agent interactions. This type of compression across an agent trajectory can use various strategies such as recursive or hierarchical summarization. **Context Trimming** - Whereas summarization typically uses an LLM to distill the most relevant pieces of context, trimming can often filter or, as Drew Breunig points out, “prune” context. This can use hard-coded heuristics like removing older messages from a list. Drew also mentions Provence, a trained context pruner for Question-Answering.

**Isolating Context**: Isolating context involves splitting it up to help an agent perform a task. **Multi-agent** - One of the most popular ways to isolate context is to split it across sub-agents. A motivation for the OpenAI Swarm library was separation of concerns, where a team of agents can handle specific sub-tasks. Each agent has a specific set of tools, instructions, and its own context window.

