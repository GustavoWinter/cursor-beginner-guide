# Agent orchestration — overview

> **Agent** executes. **Sub-agent** delegates isolated work. **Skill** documents the process.
> Orchestration is choosing the right piece at the right time.

---

## What is agent orchestration?

**Orchestration** is how you combine the **main agent** (the conversation where you request changes), **sub-agents** (separate or background sessions that explore or run focused tasks in isolation), and **skills** (repo-backed playbooks the agent follows on demand) to get predictable outcomes without burning context or repeating huge prompts.

Think in three layers:

| Layer           | Short role                                                 |
| --------------- | ---------------------------------------------------------- |
| **Skill**       | *What to do* — reusable steps, versioned in the repo       |
| **Agent**       | *Who acts* in your project — tools, files, PRs           |
| **Sub-agent**   | *Who helps off-thread* — research, read-only, summaries   |

When these three ideas line up, you rely less on “prompt luck” and more on **design**.

---

## The three pillars

### 1. Skill — the playbook

Skills live under `.cursor/skills/` (in `SKILL.md`) and describe **steps**, **triggers**, and **validation**. The main agent loads a skill when your request matches the description or when you ask for it explicitly.

**In orchestration:** the skill is the **script**. It cuts ambiguity: the agent knows the order of actions and what “done” looks like.

> Details: [04 — Skills](../04-skills/01-o-que-sao-skills.md).

### 2. Agent (main) — the executor in the repo

The **main agent** is the interactive session (for example in Agent mode) with access to your workspace, loaded rules, terminal, codebase search, and edits. It applies **rules** whenever they apply and **skills** when the situation calls for it.

**In orchestration:** the main agent is the **conductor inside the repository** — the one that keeps work consistent with the rest of the codebase and your team’s conventions.

### 3. Sub-agent — delegation with its own context

**Sub-agents** run **separately** from the main thread: another context (or another focus), often **read-only** or single-purpose (explore the repo, scan patterns, produce a digest). Output comes back **compressed** for the main agent, which decides what to apply.

**In orchestration:** sub-agents are **divide and conquer** — wide exploration or long-running prep without stuffing the main chat with thousands of lines.

---

## When to use what?

| Need                                      | Typical choice                    |
| ----------------------------------------- | --------------------------------- |
| Repeatable process in the same project    | **Skill**                         |
| Implement, refactor, ship commits/PRs     | **Main agent**                    |
| Map a large codebase without editing      | **Explore-style sub-agent**       |
| Several parallel research tracks          | **Sub-agents** in parallel        |
| Global standards (style, stack)           | **Rules** (they complement all) |

Rules remain the foundation: they say **how** code should look. Skills say **what to do** for specific workflows. The main agent **applies** both. Sub-agents **inform** or prepare work without diluting the main session’s focus.

---

## Simple mental flow

```
Rule (always-on) → Skill (if applicable) → Main agent (edits)
                        ↑
            Sub-agent (optional: explore / summarize)
```

1. Make sure **rules** cover project essentials.
2. For work you repeat, maintain a **skill** with ordered steps and a checklist.
3. Use the **main agent** to implement following rules and skills.
4. Bring in a **sub-agent** when you need broad exploration or a summarized handoff before coding.

---

## Common mistakes

| Mistake                               | Effect                         | Fix                                      |
| ------------------------------------- | ------------------------------ | ---------------------------------------- |
| Giant prompt every time               | Drift, fatigue                 | Move to **skill** or **rule**            |
| Sub-agent for everything              | Overhead, loss of coherence    | Use only when **isolation** helps        |
| Overlapping skills                    | Conflicting instructions       | One skill per **clear purpose**          |
| Bypassing the main agent on refactors | PRs misaligned with the repo   | **Edits** should stay with the main view |

---

## Summary

| Concept        | One-line reminder                                           |
| -------------- | ----------------------------------------------------------- |
| **Skill**      | Versioned playbook; loaded on demand                      |
| **Agent**      | Executor in the workspace with rules, tools, live context   |
| **Sub-agent**  | Side helper with its own context; returns a digest          |
| **Orchestration** | Combining all three (plus rules) in the right order    |

---

> **Next:** [02 — Orchestrating in practice](./02-orquestrando-na-pratica.md) — step-by-step flow with skills, main agent, and sub-agents
