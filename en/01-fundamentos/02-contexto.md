# Context: The most important concept

> Everything the agent knows comes from **context**. If you understand that, you understand most of how to work with AI.

---

## What is context?

Context is **all information the agent receives** before generating a response. That includes:

- Your prompt (what you typed)
- Conversation history (everything said in this session)
- Files you referenced with `@`
- Project rules (`.cursor/rules/`)
- Loaded skills
- Enabled MCP tools
- System information (OS, terminal, folder structure)

All of that together forms the **context window** — the agent’s “field of view.”

---

## Why context matters

### 1. Context is expensive

Every token (chunk of text) in the context costs money. More importantly: **the entire history is resent on every new message**. So a long conversation gets progressively more expensive.

### 2. More context is NOT always better

Research shows that response quality **degrades** when the context window goes beyond roughly ~50% capacity. The agent starts to “get lost” in too much information.

```
 0–50% context  →  Good quality
50–80% context  →  Quality starts to drop
80%+   context  →  “Dumb zone” — inconsistent answers
```

### 3. Bad context poisons everything

Worse than too much context is **wrong** context. Examples:

- Mixing two different tasks in one session
- Outdated comments in code
- Earlier failed attempts (the agent may repeat the same mistakes)
- Trying to “steer” after many wrong messages

---

## Four context management strategies

### 1. Persist outside the window

Store important information in files the agent can read when needed, instead of trying to keep everything in the chat.

**Where to store:**

- `.cursor/rules/` — rules the agent loads automatically
- `agents.md` or `AGENTS.md` — general project context
- `.cursor/skills/` — reusable workflows
- Plan files (`plans/`) — decisions and strategy

### 2. Be selective

Bring into context **only what is relevant for this step**. Do not load everything that “might be useful.”

**Practical examples in Cursor:**

- Use `@file.ts` to reference only relevant files
- Disable MCPs that are not needed for the current task
- Do not paste whole docs — cite only the relevant part

### 3. Summarize and compress

After a long debugging session, context is full of attempts, errors, and detours. Before continuing:

1. Ask the agent: *“Summarize what we found and what the fix is.”*
2. Read the summary and validate it
3. Open a **new session** with only the summary as the starting point

> AI is great at writing prompts for AI. Use that to your advantage.

### 4. Isolate context

Split work across separate sessions. Each session should have **one clear task**.


| Bad | Good |
| --- | ---- |
| One session for “refactor auth, add tests, and fix login bug” | Session 1: research the login bug |
| | Session 2: plan the refactor |
| | Session 3: implement the changes |


---

## Signs that context is polluted

Watch for these during a session:

- The agent **repeats errors** you already corrected
- Answers become **generic** instead of specific
- The agent **forgets** instructions you gave earlier
- The agent suggests things that **contradict** what you agreed on
- You feel you are “fighting” the agent

**When that happens:** stop, open a new session, and start clean.

---

## Context in Cursor — where things live

```
Always in context:
├── Always-on rules (.cursor/rules/ with alwaysApply: true)
├── System information (OS, terminal, git status)
└── System prompt of the active mode (Ask, Agent, Plan)

Added by you:
├── @file.ts — specific file
├── @folder/ — whole folder
├── Your prompt text
└── Current conversation history

Added on demand:
├── Skills (when referenced)
├── Contextual rules (when the agent detects relevance)
└── MCP tools (descriptions of enabled tools)
```

---

## Practical habits

1. **One task per session** — do not mix topics
2. **Watch context size** — if the chat is long, it is probably time for a new session
3. **If something feels wrong, trust that** — start a new session
4. **Ask for summaries** — before a new session, ask the agent to summarize current state
5. **Disable MCPs you are not using** — each MCP adds tokens to context

---

## Summary


| Concept | Meaning |
| ------- | ------- |
| Context is everything | The agent only knows what is in the context window |
| Less is more | Too much context degrades quality |
| Garbage in, garbage out | Bad context produces bad results |
| Persist outside | Use rules, skills, and files to store information |
| Isolate | One task, one session |


---

> **Next:** [03 — The Research → Plan → Implement workflow](./03-workflow.md)
