# Exercise 4: Rules in practice — before and after

> **Goal:** See the concrete difference rules make in the agent’s output.
> **Mode:** Agent Mode
> **Estimated time:** 20 minutes

---

## Scenario

We will ask the agent for the **same thing twice**: first without rules, then with rules. The difference should be obvious.

---

## Part A — WITHOUT rules

### Setup

1. Temporarily rename `.cursor/rules` to `.cursor/rules-backup` (to disable rules)
2. Open a **new session** in Agent Mode

### Prompt to copy and paste:

```
Create a simple Vue component called AlertBanner that:
- Receives a type (success, error, warning)
- Receives a message
- Has a close button
- Emits an event when closed
```

### What to observe and note:

Look at the result and note:

| Criterion                                | What did the agent do? |
| ---------------------------------------- | ---------------------- |
| Composition API or Options API?          |                        |
| TypeScript?                              |                        |
| Where is CSS? (inline, scoped, external) |                        |
| Any CSS methodology? (BEM, etc.)         |                        |
| Hardcoded strings or i18n?               |                        |
| Test file created?                       |                        |
| Which folder for the component?          |                        |
| Typed props?                             |                        |

**Do not accept the changes. Only take notes.**

---

## Part B — WITH rules

### Setup

1. Restore `.cursor/rules` (rename back)
2. If you have no rules yet, create a basic one. Open a new session in Agent Mode:

````
Create a file .cursor/rules/components.mdc with the following content:

---
description: Standards for creating Vue components
alwaysApply: true
---

# Vue component standards

## Required
- Use `<script setup lang="ts">`
- Type all props with a TypeScript interface
- Type all emits
- CSS in an external SCSS file (never inline, never scoped)
- BEM methodology for CSS classes
- User-visible strings via i18n (never hardcoded)

## .vue file structure
1. `<script setup lang="ts">` (first)
2. `<template>` (second)
3. `<style lang="scss" src="./ComponentName.scss" />` (third)

## Naming
- File: PascalCase (e.g. AlertBanner.vue)
- Root CSS class: kebab-case (e.g. .alert-banner)
- BEM elements: block__element (e.g. .alert-banner__title)
- BEM modifiers: block--modifier (e.g. .alert-banner--error)

## Example

```vue
<script setup lang="ts">
interface Props {
  title: string
  variant?: 'primary' | 'secondary'
}

withDefaults(defineProps<Props>(), {
  variant: 'primary'
})

const emit = defineEmits<{
  close: []
}>()
</script>
````

3. Open a **new session** (important — clean context)

### Same prompt:

```
Create a simple Vue component called AlertBanner that:
- Receives a type (success, error, warning)
- Receives a message
- Has a close button
- Emits an event when closed
```

### What to observe and note:

Note the same criteria:

| Criterion                        | Without rules (Part A) | With rules (Part B) |
| -------------------------------- | ---------------------- | ------------------- |
| Composition API or Options API?  |                        |                     |
| TypeScript?                      |                        |                     |
| CSS inline, scoped, or external? |                        |                     |
| CSS methodology (BEM)?           |                        |                     |
| i18n for strings?                |                        |                     |
| Test created?                    |                        |                     |
| Component folder?                |                        |                     |
| Typed props?                     |                        |                     |

---

## Part C — Comparison

### The difference should be clear:

**Without rules:**

- The agent makes **arbitrary** choices
- May use Options API or Composition API
- CSS is often inline or scoped
- Strings are often hardcoded
- No consistent naming pattern

**With rules:**

- The agent follows **exactly** what the rule defines
- Composition API with script setup always
- External SCSS with BEM always
- Strings with i18n always
- Consistent naming

### Main lesson:

> Rules turn unpredictable results into consistent results.
> The same prompt can produce completely different code depending on the rules.

---

## Bonus exercise — contextual rule

Create a rule that only loads for test files:

### Prompt:

```
Create a file .cursor/rules/tests.mdc with this content:

---
description: Standards for unit tests
globs: ["**/*.spec.ts", "**/*.test.ts"]
---

# Test standards

## Framework
- Vitest + @vue/test-utils

## Structure
- describe() groups by component
- it() with English description of behavior
- Arrange → Act → Assert pattern

## Required
- Test rendering with default props
- Test each prop that changes appearance
- Test emitted events
- Test loading/error states when applicable

## Naming
- File: [ComponentName].spec.ts
- describe: component name
- it: "should [expected behavior]"
```

Then open a new session and ask:

```
Create unit tests for the AlertBanner component.
```

### What to observe:

- The test rule loads automatically (because of `globs`)
- Tests follow the defined pattern
- `it()` descriptions are in English as defined by the rule

---

## What we learned

1. **Without rules** — the agent improvises and results vary
2. **With rules** — the agent follows patterns and results are consistent
3. **Always-on rules** — load on every interaction
4. **Rules with globs** — load only for specific file types
5. **Investing in rules** — investing in long-term quality

---

> **Next:** [05 — Skills exercise](./05-exercicio-skills.md) — automate tasks with skills
