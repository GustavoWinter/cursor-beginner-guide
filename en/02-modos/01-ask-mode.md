# Ask Mode — research and understand

> Cursor’s most underrated mode.
> Here you turn the agent into a **researcher** that can only read and talk.

---

## What is Ask Mode?

Ask Mode is **read-only**. The agent can:

- Read project files
- Search the codebase
- Answer questions
- Analyze code

The agent **cannot**:

- Create or edit files
- Run terminal commands
- Make commits
- Change anything in the project

---

## Why that is powerful

It sounds limiting, but it is the opposite. By removing the ability to act, you force the agent to **think** instead of rushing to execute.

Without Ask Mode, the default behavior is:

1. You ask something
2. The agent immediately starts generating code
3. You get 200 lines that may or may not be correct

With Ask Mode:

1. You ask something
2. The agent researches, analyzes, and **explains**
3. You understand the problem before touching any code

---

## How to enable Ask Mode

In Cursor, in the chat field, you will see a mode selector. Click it and choose **“Ask.”**

You can also use a keyboard shortcut or type directly in the field.

---

## When to use Ask Mode


| Situation | Example prompt |
| --------- | -------------- |
| **Understand existing code** | *“How does authentication work in this project?”* |
| **Investigate a bug** | *“What might cause this error? @file-with-error.ts”* |
| **Compare approaches** | *“What are the pros and cons of Pinia vs composables here?”* |
| **Learn project patterns** | *“What component patterns does this project use? Show examples.”* |
| **Prepare a change** | *“If I need to add a new field to the form, which files should I change?”* |
| **Review a concept** | *“Explain how Vue Router is used in this project.”* |


---

## Example prompts for Ask Mode

### Explore the codebase

```
Give me an overview of this project’s structure.
What are the main folders and what does each contain?
```

### Investigate how something works

```
How do product data reach the listing component?
Trace the path from the API to the template.
Reference the files involved.
```

### Prepare an implementation

```
I need to add CPF validation to the registration form.

1. Where is the current form? Which components are involved?
2. Is there similar validation elsewhere I can mirror?
3. Which files would I need to change?
4. Is there an existing validation utility?
```

### Understand an error

```
I am getting this error:

[paste error here]

Analyze the error, look at the relevant project files,
and explain what might be causing it.
Do not fix it — only explain.
```

---

## Good practices in Ask Mode

1. **Be specific** — Instead of *“how does auth work?”*, ask *“how is the JWT validated in the auth middleware?”*
2. **Reference files** — Use `@` to point to specific files. That reduces ambiguity and focuses the agent.
3. **Ask for references** — End with *“show me the relevant files and lines”* for concrete answers.
4. **Do not rush** — The goal here is to understand, not to solve. Ask as many questions as you need.
5. **Sanity-check** — Before leaving Ask Mode, ask yourself: *“Do I understand the problem well enough to explain it to someone else?”*

---

## What Ask Mode does NOT do

- It does not generate code for you to copy-paste (that is Agent Mode)
- It does not execute changes (it cannot)
- It does not replace reading code yourself (but it speeds things up a lot)

---

## Summary


| Aspect | Detail |
| ------ | ------ |
| **Capability** | Read and chat only |
| **When to use** | Before implementing anything |
| **Goal** | Understand the problem and the system |
| **Outcome** | You leave knowing exactly what to do |
| **Common mistake** | Jumping straight to Agent Mode without research |


---

> **Next:** [02 — Plan Mode](./02-plan-mode.md) — design the solution before implementing
