# Orchestrating in practice — step by step

> Design an intentional flow: **skill** defines the process, **agent** implements, **sub-agent** supports when it helps.

---

## When to design an orchestration flow

Do this when:

- The task has **several stages** and you have already repeated similar prompts
- You need to **scan a lot of code** before touching files
- Multiple people should reach the **same outcome**
- You want **less noise** in the main conversation’s context

---

## Step by step

### 1. Write the end state in one line

Describe what must exist when you are done (files, PR, tests green). That becomes the success criterion for the **main agent**.

**Example:** “New `/reports` route with page, smoke test, and menu entry.”

---

### 2. Split “standard” from “process”

- **Standard** (language, folders, tests) → should already live in **rules**.
- **Process** (file order, checklist, release steps) → good candidate for a **skill**.

If the process repeats in more than three steps, create or update `.cursor/skills/<name>/SKILL.md`.

---

### 3. Author the skill for all three roles

In `SKILL.md`, make explicit:

1. **When to use** — triggers so the main agent loads the skill.
2. **Ordered steps** — what to do in sequence.
3. **Validation** — checkboxes the agent can follow before finishing.

That way the **agent** does not improvise order; it **follows the script**.

Minimal structure:

```markdown
# Skill name

> One line: what it delivers and when to use it.

## Trigger

- Requests like: "..."
- When this exists: ...

## Steps

### 1. ...

### 2. ...

## Validation

- [ ] ...
```

---

### 4. Decide if you need a sub-agent

Before editing, ask: “Do I need a **wide map** of the repo without loading everything into the main chat?”

- **Yes** — use a **read-only explore** sub-agent: a crisp brief of what to discover (key folders, patterns, similar files).
- **No** — go straight to the **main agent** with the skill.

If the same specialist role should be **reused** across sessions (verifier, debugger, security review), add a **custom** sub-agent under **`.cursor/agents/`** and commit that folder so everyone gets the same definitions. Full field reference: [Cursor — Subagents](https://cursor.com/docs/subagents).

#### How to create a custom sub-agent (file format)

Each custom sub-agent is **one Markdown file** (for example `.cursor/agents/security-auditor.md`). **YAML frontmatter** at the top tells Cursor the `name`, when to delegate (`description`), and optional behavior (`model`, `readonly`, `is_background`). **Everything after the second `---`** is the prompt the sub-agent runs with (same idea as the [official “File format” section](https://cursor.com/docs/subagents)).

Example (adapt the filename, `name`, and body to your own specialist):

````text
---
name: security-auditor
description: Security specialist. Use when implementing auth, payments, or handling sensitive data.
model: inherit
readonly: true
---

You are a security expert auditing code for vulnerabilities.

When invoked:
1. Identify security-sensitive code paths
2. Check for common vulnerabilities (injection, XSS, auth bypass)
3. Verify secrets are not hardcoded
4. Review input validation and sanitization

Report findings by severity:
- Critical (must fix before deploy)
- High (fix soon)
- Medium (address when possible)
````

- **`name`** — identifier; invoke explicitly with `/security-auditor` in the prompt (see *Using subagents* in the [Cursor Subagents doc](https://cursor.com/docs/subagents)).
- **`description`** — short text Agent uses to decide **when** to delegate; make it specific.
- **`model`** — often `inherit` or `fast`; see the doc for other options.
- **`readonly: true`** — sub-agent runs read-only (no edits / state-changing shell), good for audits and exploration-only roles.

**Good sub-agent prompt:**

```
Explore where routes and pages are registered in this project.
Summarize: main files, one existing example, naming conventions.
Do not propose changes yet.
```

**Afterward:** paste the summary into the **main agent** and ask for implementation **following skill** X.

---

### 5. Run with the main agent

In the main session:

1. Mention the **skill** if it is not picked up automatically.
2. Attach **minimal context** (open files, targeted `@file` references).
3. Ask the agent to **point to** where each skill step was applied (easier review).

**Example prompt:**

```
Use the `create-page` skill (in .cursor/skills/create-page/SKILL.md).
Implement the reports page using the exploration summary below.
[...paste sub-agent summary...]
```

---

### 6. Review as the human orchestrator

Quick checklist:

- [ ] Rules respected (lint, style, i18n)?
- [ ] Every skill step covered?
- [ ] No contradictions between skill and rules (if there are, fix the skill)?

---

## Full example (story)

**Scenario:** add an endpoint and a client in an internal SDK.

1. **Sub-agent:** locate where other SDK endpoints are defined and how tests are named.
2. **Skill `add-sdk-endpoint`:** steps — contract, implementation, test, package README example.
3. **Main agent:** implements using summary + skill; opens PR.

When the repo changes, update the **skill** (and **rules** if the standard changed).

---

## Organizing skills for orchestration

Avoid one mega-skill that does everything. Prefer:

```
.cursor/skills/
├── explore-feature-area/   ← exploration-friendly
├── add-sdk-endpoint/       ← closed process
└── release-internal-pkg/   ← another process
```

**Small, composable** skills are easier for the main agent to chain in the right order.

---

## Testing the flow

1. Start a fresh conversation (cleaner context).
2. Repeat only the **short request** plus the skill reference.
3. Confirm the agent loaded the skill and steps match the PR.
4. Optional: run again **without** a sub-agent in phase one and compare output quality.

---

## Summary

1. Define **end state** and what is **standard** (rule) vs **process** (skill).
2. Keep `SKILL.md` with triggers, steps, and validation.
3. Use **sub-agent** for exploration/summary; **main agent** for edits.
4. Iterate skills when the team’s real flow changes.

---

> **Next:** [03 — PDF orchestration example](./03-pdf-orchestration-example.md) — skill + three sub-agents for a large PDF digest · [05 — Hands-on guides](../05-guias-praticos/01-exercicio-ask-mode.md) — practice modes and flows on a real project
