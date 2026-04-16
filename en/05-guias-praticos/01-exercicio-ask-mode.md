# Exercise 1: Ask Mode in practice

> **Goal:** Learn to explore a codebase without changing anything.
> **Mode:** Ask Mode
> **Estimated time:** 15 minutes

---

## Scenario

You just joined a new project. You need to understand how it works before making any changes. We will use Ask Mode to research.

---

## Setup

1. Open Cursor in an existing project (any project)
2. Switch to **Ask Mode** in the mode selector
3. Open the chat

---

## Exercise 1.1 — Project overview

### Prompt to copy and paste:

```
Give me an overview of this project:
1. Which framework and language are used?
2. What is the main folder structure?
3. What are the build, dev, and test commands?
4. Are there special configurations (linters, formatters, etc.)?
```

### What to watch for:

- The agent will read files like `package.json`, `tsconfig.json`, project root
- It **will not change anything** — only read and answer
- The answer should be an organized summary of the project

### Checkpoint:

> Does the answer match what you know about the project? If yes, the agent understood the context.

---

## Exercise 1.2 — Understand a specific flow

Pick a feature in the project and ask the agent to explain how it works.

### Prompt to copy and paste:

```
Explain how the [FEATURE] flow works in this project.

I want to understand:
1. Which components/files are involved?
2. How does data flow (from API to UI)?
3. Is any global state (store) involved?
4. What are the entry points (routes, events, etc.)?

Reference specific files and lines.
```

> Replace `[FEATURE]` with something from your project. Examples:
>
> - "product listing"
> - "user authentication"
> - "contact form submission"

### What to watch for:

- The agent should search and read relevant files
- The answer should reference real file paths
- If the agent asks for more context, provide it with `@file`

---

## Exercise 1.3 — Research before implementing

Imagine you need to add a feature. Use Ask Mode to **research first**.

### Prompt to copy and paste:

```
I need to add [NEW FEATURE] to the project.

Before implementing, help me understand:
1. Is there something similar already implemented I can use as reference?
2. Which files would I need to create or change?
3. What patterns in the project should I follow?
4. What edge cases should I consider?
5. Are there dependencies I would need to add?

Do NOT implement anything — only research and answer.
```

> Replace `[NEW FEATURE]` with something simple. Examples:
>
> - "a search filter on the listing"
> - "an export to CSV button"
> - "email validation on the form"

### What to watch for:

- The agent researches but **does not generate implementation code**
- It should find existing patterns to mirror
- The answer should give you confidence to move on to planning

---

## Exercise 1.4 — Compare approaches

### Prompt to copy and paste:

```
I need to implement [PROBLEM].
What approaches would make sense in this project?

Compare at least two options considering:
- Pros and cons of each
- Which aligns best with existing patterns
- Implementation complexity
- Maintainability

Recommend one option and justify it.
```

### What to watch for:

- The agent should analyze the real project, not give generic advice
- The recommendation should consider what already exists in the codebase
- You should leave with a clear decision

---

## What we learned

After these exercises, you should notice that:

1. **Ask Mode prevents rushed decisions** — you cannot generate code even if you want to
2. **Research first is fast** — a few minutes of research save hours of refactoring
3. **The agent reads the real codebase** — answers are based on your project, not generic examples
4. **You leave knowing what to do** — and that clarity makes implementation faster

---

## Next step

Now that you know how to research, we will **plan**.

> **Next:** [02 — Plan Mode exercise](./02-exercicio-plan-mode.md)
