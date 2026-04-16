# Rules — teaching the agent your standards

> Without rules, you repeat the same instructions every session.
> With rules, the agent **always** knows how your project works.

---

## What are rules?

Rules are **persistent instructions** the agent loads automatically. Instead of repeating “use BEM for CSS” or “follow the composables pattern” every chat, you write it once as a rule and the agent always follows it.

Think of rules as your project’s **developer handbook** — written for the AI to read.

---

## Why rules matter

### Without rules

You open a new session and write:

```
Create a product card component.
Use BEM for CSS.
Use Composition API with script setup.
Use our custom Tailwind classes.
Put strings in i18n files.
Use external SCSS, not inline.
Follow the pattern of other components in the project.
```

Next session, you repeat all of that. If you forget something, the agent generates off-pattern code.

### With rules

You open a new session and write:

```
Create a product card component.
```

The agent already knows the patterns because the rules were loaded automatically.

---

## Types of rules in Cursor

Rules live in `.cursor/rules/` in your project. There are several types:

### 1. Always apply

Loaded on **every** interaction, regardless of context.

**When to use:** Patterns that apply to any task in the project.

**Examples:**

- Code conventions (BEM, Composition API, etc.)
- Folder structure
- Naming patterns

```yaml
---
description: General development standards
alwaysApply: true
---
```

### 2. Auto attached

Loaded only when the agent works with **files that match a pattern**.

**When to use:** Rules specific to certain file types.

**Examples:**

- Vue rules when working with `.vue`
- Test rules when working with `.spec.ts`
- Style rules when working with `.scss`

```yaml
---
description: Standards for Vue components
globs: ["**/*.vue"]
---
```

### 3. Agent requested (on demand)

The agent **decides** whether to load a rule based on its description. It reads the description and, if it seems relevant, loads the full content.

**When to use:** Specialized rules that are not always needed.

**Examples:**

- How to deploy
- How to create a new page
- How to change pricing

```yaml
---
description: How to create new pages in the CMS
---
```

### 4. Manual (only when you ask)

Loaded only when you explicitly reference them with `@`.

**When to use:** Very specific or rarely used rules.

---

## Where rules live

```
your-project/
├── .cursor/
│   └── rules/
│       ├── general.mdc            ← always apply
│       ├── components/
│       │   └── vue.mdc            ← auto attached for .vue
│       ├── tests/
│       │   └── unit.mdc           ← auto attached for .spec.ts
│       └── deploy/
│           └── deploy.mdc         ← agent requested
```

Rules use the `.mdc` extension (Markdown with configuration frontmatter).

---

## Anatomy of a rule

An `.mdc` rule has two parts:

### 1. Frontmatter (configuration)

```yaml
---
description: Short description of what this rule does
alwaysApply: true          # or false
globs: ["**/*.vue"]        # optional — file pattern
---
```

### 2. Content (instructions in Markdown)

```markdown
# Vue component standards

## Required
- Use `<script setup lang="ts">`
- External CSS in a separate `.scss` file
- Strings via i18n, never hardcoded
- CSS classes following BEM

## Forbidden
- Do not use Options API
- Do not use inline CSS
- Do not use default Tailwind classes (only project custom ones)
```

---

## Rules vs. repeating in the prompt


| Aspect | Repeat in prompt | Use a rule |
| ------ | ---------------- | ---------- |
| Consistency | Depends on you remembering | Automatic |
| Maintenance | Spread across N sessions | Centralized in one file |
| Team | Everyone repeats differently | Everyone follows the same rule |
| Context | Uses space every time | Loaded intelligently |


---

## Important tips

1. **Start simple** — one general rule with the most important standards
2. **Do not overdo it** — too many rules pollute context (remember the context chapter)
3. **Be specific** — *“use BEM”* is better than *“write well-organized CSS”*
4. **Include examples** — the agent learns better from concrete examples
5. **Update as you learn** — rules should evolve with the project

---

## Summary


| Concept | Detail |
| ------- | ------ |
| **What they are** | Persistent instructions for the agent |
| **Where they live** | `.cursor/rules/*.mdc` |
| **Types** | Always apply, auto attached, agent requested, manual |
| **Benefit** | You do not repeat standards every session |
| **Caution** | Too many rules pollute context — keep them lean |


---

> **Next:** [02 — Creating rules](./02-criando-regras.md) — step-by-step tutorial for your first rules
