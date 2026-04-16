# The Right Mental Model

> Before you open Cursor, you need to adjust how you **think** about AI.
> That mindset shift is the difference between frustration and productivity.

---

## Using AI vs. working with AI

Most developers say they “use AI to code faster.” But if you ask _how_, exactly, few can explain the real flow: what they delegate, what they keep, and how they choose between the two.

That distinction matters. There is a gap between:

- **Using AI** — accepting autocomplete suggestions and hoping it works
- **Working with AI** — directing the work, reviewing critically, and deciding what the agent may or may not do

Working with AI is an active role. You are the tech lead; the agent is the executor.

---

## The agent as a junior developer

The most useful mental model for Cursor:

> **Think of the agent as an enthusiastic junior developer, extremely well read, and often wrong with confidence.**

### What the agent does well

| Strength            | Example                                              |
| ------------------- | ---------------------------------------------------- |
| **Speed**           | Generates hundreds of lines in seconds               |
| **No ego**          | Rewrites the same code six times without complaining |
| **Broad knowledge** | Knows many languages, frameworks, and patterns       |
| **Tireless**        | Does not get tired, distracted, or need coffee       |

### What the agent does not do well

| Weakness                  | Example                                                         |
| ------------------------- | --------------------------------------------------------------- |
| **No judgment**           | Does not know whether that endpoint is critical to the business |
| **No historical context** | Does not know why you chose that architecture three months ago  |
| **Overconfidence**        | Writes technically correct but contextually wrong code          |
| **No system view**        | Can break an integration it does not even know exists           |

### In practice

Imagine you ask the agent: _“Create a payment endpoint.”_

It will generate a working endpoint. But it does not know that:

- Your system uses a specific payment gateway
- There is an async processing queue
- Security requires a specific logging standard
- There is an undocumented business rule about installments

The code will compile. Tests may pass. It still will not be production-ready.

**That is the gap you must fill.**

---

## Your role: director of the work

If the agent is the junior dev, you are the **tech lead**. Your job is not to write every line of code — it is to make sure the final result is correct.

That means:

1. **Define what needs to be done** — clearly enough for the agent to execute
2. **Provide context** — the agent only knows what you tell it
3. **Review the output** — never accept code without reading it
4. **Correct course** — when the agent is wrong, redirect with clear instructions

### Practical analogy

| Situation                      | Without the mental model | With the mental model                        |
| ------------------------------ | ------------------------ | -------------------------------------------- |
| Agent generates wrong code     | “AI does not work”       | “I did not give enough context”              |
| Agent ignores project patterns | “AI is dumb”             | “I need a rule for this”                     |
| Result is good on first try    | “AI is magic”            | “The prompt was very specific”               |
| Quality drops over the session | “AI got tired?”          | “Context got noisy — time for a new session” |

---

## Summary

- The agent is a powerful tool, but **it has no judgment**
- You need to be the **director of the work**, not just a consumer of suggestions
- Output quality depends directly on the quality of the **input you provide**
- When the result is bad, the first question should be: _“What could I have done differently?”_

---

> **Next:** [02 — What is context](./02-contexto.md) — the most important concept for working with AI
