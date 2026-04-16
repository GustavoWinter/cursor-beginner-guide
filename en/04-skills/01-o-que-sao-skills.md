# Skills — reusable workflows

> Rules say **how** to do things. Skills say **what** to do.
> They are playbooks the agent runs on demand.

---

## What are skills?

Skills are **complete workflows** the agent can run when asked. While rules define patterns (“use BEM”, “use i18n”), skills define processes (“to create a Vue component, follow these seven steps”).

Think of skills as **recipes** — step-by-step instructions to complete a specific task consistently.

---

## Rules vs. skills


| Aspect | Rules | Skills |
| ------ | ----- | ------ |
| **What they do** | Define patterns and conventions | Define complete workflows |
| **When they load** | Automatically (always apply) or by context | On demand (when you ask) |
| **Analogy** | Style guide | Recipe |
| **Example** | “Use BEM for CSS” | “To create a component: 1) create .vue, 2) create .scss, 3) create .spec.ts…” |
| **Size** | Usually short and focused | Usually longer and detailed |
| **Where they live** | `.cursor/rules/` | `.cursor/skills/` |


---

## When to use skills


| Situation | Example skill |
| --------- | ------------- |
| Repetitive task | “Create Vue component” — same flow every time |
| Multi-step process | “From ticket to PR” — fetch card, implement, branch, open PR |
| Complex standard | “Code review” — validation checklist with many criteria |
| Onboarding | “Project setup” — steps for local environment |
| Deploy flow | “Deploy” — branch, changelog, tag, PR |


---

## Anatomy of a skill

Skills live under `.cursor/skills/` with this structure:

```
.cursor/
└── skills/
    └── skill-name/
        └── SKILL.md
```

### The SKILL.md file

```markdown
# Skill name

> Short description: when and why to use this skill.

## When to use
- Situation A
- Situation B

## Steps

### 1. First step
Detailed instructions...

### 2. Second step
Detailed instructions...

### 3. Third step
Detailed instructions...

## Example usage
A prompt the user can use to trigger this skill.

## Expected output
What the user should have at the end.
```

---

## How to use a skill

### Implicit

Cursor detects skills from the description in `SKILL.md`. When you ask for something that matches, the agent loads and follows the skill.

```
Create a Vue component to show order details.
```

If a skill “create-vue-component” says in its description to use it when creating new Vue components, the agent will load and follow it.

### Explicit

You can also reference directly:

```
Use the component creation skill to build a
notifications list component.
```

---

## Useful skill examples

### Skill: Create Vue component

```markdown
# Create Vue component

> Creates a full Vue component following project standards.
> Use when creating new Vue components.

## Steps

### 1. Create the .vue file
- Location: `src/components/[ComponentName].vue`
- Use `<script setup lang="ts">`
- Type all props and emits

### 2. Create the .scss file
- Location: `src/components/[ComponentName].scss`
- Follow BEM methodology
- Use only custom Tailwind classes

### 3. Create the i18n file
- Location: `src/i18n/[feature]/[component-name].json`
- Extract all visible strings

### 4. Create the test file
- Location: `src/components/__tests__/[ComponentName].spec.ts`
- Cover rendering, props, events

### 5. Register the component (if needed)
- Check whether it must be imported in an index or route
```

### Skill: Code review

```markdown
# Code review

> Performs code review following project standards.
> Use when reviewing PRs or code changes.

## Checklist

### Code quality
- [ ] Clear, descriptive names
- [ ] Single-responsibility functions
- [ ] No duplicated logic

### Project standards
- [ ] Composition API with script setup
- [ ] BEM for CSS
- [ ] i18n for strings
- [ ] External SCSS

### Security
- [ ] No hardcoded credentials
- [ ] Sanitized inputs
- [ ] No sensitive data in logs

### Tests
- [ ] Unit tests for new logic
- [ ] Existing tests passing
```

---

## Skills vs. repeating instructions


| Scenario | Without a skill | With a skill |
| -------- | ---------------- | ------------ |
| Create component first time | Write a 15-line prompt | Write a 15-line prompt |
| Create component fifth time | Write 15 lines again | “Create a component for X” |
| New teammate | Must learn patterns | Skill documents the process |
| Change the standard | Update every future session | Update SKILL.md once |


From the **second** time you do something, consider creating a skill.

---

## Good practices for skills

1. **One skill, one purpose** — do not mix “create component” with “deploy”
2. **Clear, ordered steps** — the agent follows in sequence
3. **Include examples** — the more concrete, the better the result
4. **Define expected output** — what should exist when the skill finishes
5. **Update often** — if the process changed, update the skill

---

## Summary


| Concept | Detail |
| ------- | ------ |
| **What they are** | Reusable workflows |
| **Where they live** | `.cursor/skills/skill-name/SKILL.md` |
| **When to use** | Repetitive tasks or multi-step processes |
| **Difference from rules** | Rules = patterns (how), skills = processes (what to do) |
| **Benefit** | Consistency and speed on repeated tasks |


---

> **Next:** [02 — Creating skills](./02-criando-skills.md) — tutorial for your first skills
