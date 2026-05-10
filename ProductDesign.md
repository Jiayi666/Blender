# Blender Product Design

## What Is Blender

The name blender comes from the kitcken tool for blending ingredients together for better digestion. The tool is like a blender of knowledge that helps to spoon-feeding knowledge to users the way they like. This is a second brain that grows with interactions.

Everyone has different prefernce of learning new knowledge, and set their blender differently. And this is where the tool shines. It is stateful and able to learn from your previous conversations to personalize its knowlege feeding format.

## Purpose

### Personal Doc Management

This should be a tool that help me to do house clean up for my personal documents, especially the ones less structured, like weekly reflections, personal productivity reviews etc.

### Thinking Chain Skills Grow With Learns

Another thing is I want to use the "weekly reflection" and other "learnings" to update my "thinking chain". For example, I may learned that when planning for a new task I should firstly consider about "why we need to solve this", then "what are the requirements", then "what are the options", then "what are the trade-offs" etc. I want to maintain skills that is basically a template that help me to generate a clear chain of decision making, in my own style, with updated way of thinking.

### Spoon Feeding Knowledge Grow With Conversation

Everyone learns knowledge differently, I want a skill that can be used for generating debrief for docs, codebase, and new topics. The skill should be continuously updated based on previous usage. My expectation is that

1. I use the skill to generate "feeds" (like instagram feed)
2. I discuss with the agent about its feed including follow up questions, clarifications, agent does more research based on my question
3. After the discussion concludes, the agent analyze the conversation and update the skill so next time it is doing a better job "forecasting my questions" and has a better chance of one-shot the debrief I liked

### Obfuscate Sensitive Data & Absolutely No Code

Because this will be updated in work, the tool should obfuscate specific work related things to general engineering, career items that can be published to public network, and it should never include any code snippet in this directory.

- Help me remeber what I learned (engieering instincts, architectural best practices, career growth etc.)
- Distill how I learn from conversations to optimize "how the agent should present new topics so I can digest asap", and "how the agent should 
- Help me do the house cleaning of organizing my things, formating ideas, documenting learns etc.

## Design

### Blender Tool State Management

As described above, the tool is stateful and that is how it "learns from previous conversation". And inspired by the [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) the cheapest state storage for an agent is the local file system.

Similar as the LLM wiki, the blender tool should separate its files into "skill files", "index files" (including a global index file for each topic, and a compact description of each raw file, the global index should points to the compact file then to the raw file if necessary), and the "raw files".

The raw (and compacted raw) files should be categorized (grouped in sub-directories) based on doc types like "new topics conversation", "project plan conversation", "design brainstorm", "knowledge docs" etc.

The index file should be arranged by use case and only include pointers to compact raw files related with the use case. Here the use case is generally the problems the tools is trying to solve (project design, project planning, digest new knowledge etc.)

### Skills

- /design: Interactively brainstorm with me to design the solution of a problem. Follow my think-chain to probe me through the whole process of "why it is a problem", "what are the requirements of the problems", "what could be the options (fundamental or adhoc)", and "what are the pros and cons"
- /plan-project: Interactively brainstorm with me to plan a project. Follow my think-chain (we can have different think chain for different topics) to work with me through topics like "how can we parallelize", "how can we test each part in isolation", "what are the integration points", "what are the internal dependencies" etc.
- /spoon-feed: With an input material (a doc), generate a customized "feed" (an abstract, or a learning guide that exploit the core of the input material. And allow me to ask follow up questions where the agent can do more research to answer
- /archive: Can be called AFTER any of the above skills to archive the conversation to a new raw material encoded in the tool (also create the compact raw doc and add to relavant index doc). The agent should analyze the conversation to learn what are my follow up questions, where I changed from the initial output from the agent, to update the initial skills (/design, /plan-project, /spoon-feed etc.) so it has better chance of not requiring me to ask those follow ups

## Challenges

1. State management: This is a stateful system, it is challenging to define "WHEN the agent should read and write to the state"
2. DB search efficiency: This is similar as the state management challenge, it is hard to define what data the agent need from the "context database" (raw or slightly compacted conversations, raw docs, papers etc.). Basically it would be similar as a RAG that provide a search interface for the agent so it can pull only relavant context. It could be start with a simple index file, or a JSON formated file (can do jq filter), or even more complicated.
