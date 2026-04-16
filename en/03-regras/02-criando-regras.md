# Creating rules — step by step

> Learn to create rules that make the agent follow your project standards automatically.

---

## Method 1: From Cursor (recommended for beginners)

Cursor has a guided command to create rules:

1. Open the Command Palette (`Cmd+Shift+P` on Mac / `Ctrl+Shift+P` on Windows)
2. Type **“Cursor: New Rule”**
3. Choose the rule type
4. Give it a name
5. Cursor creates the `.mdc` file in the right folder

---

## Method 2: Manually

### Step 1: Create the folder (if it does not exist)

```
mkdir -p .cursor/rules
```

### Step 2: Create the `.mdc` file

Create a file with the `.mdc` extension inside `.cursor/rules/`.

### Step 3: Add frontmatter

```yaml
---
description: General code standards for the project
alwaysApply: true
---
```

### Step 4: Write the instructions

```markdown
# Project standards

## Language and framework

- Vue 3 with Composition API (`<script setup>`)
- TypeScript by default
- External SCSS (never inline CSS)

## Naming

- Components: PascalCase (e.g. `ProductCard.vue`)
- Composables: camelCase with `use` prefix (e.g. `useProducts.ts`)
- Test files: same name + `.spec.ts` (e.g. `ProductCard.spec.ts`)

## CSS

- BEM methodology for classes
- Use only project custom Tailwind classes
- Never use default Tailwind classes

## i18n

- All user-visible strings must use i18n
- Never hardcoded text in templates
```

---

## Method 3: Ask the agent to create them

You can use the agent to create rules — a great use case:

```
Analyze existing components in this project and create a rule
at .cursor/rules/components.mdc documenting the patterns you find.

The rule should have alwaysApply: true and cover:
- Component structure (script setup, template, style)
- CSS patterns
- Naming patterns
- i18n patterns
- What NOT to do

Include real examples from the project.
```

That is powerful because the agent will **analyze real code** and extract patterns that already exist.

---

## Useful rule examples

### General project rule

```yaml
---
description: General project conventions
alwaysApply: true
---

# Project conventions

## Stack
- Vue 3 + Composition API + TypeScript
- Vite as bundler
- Vitest for unit tests
- SCSS for styles

## Commands
- `npm run dev` — local development
- `npm run build` — production build
- `npm run test` — run tests
- `npm run lint` — run linter

## General rules
- Never commit without running tests
- Always type props and emits
- Components over 200 lines should be split
```

### Rule for Vue components

```yaml
---
description: Standards for Vue components
globs: ["**/*.vue"]
---

# Vue components

## Required structure

The component must follow this order:
1. `<script setup lang="ts">` (first)
2. `<template>` (second)
3. `<style>` referencing external SCSS (third)

## Example

<script setup lang="ts">
interface Props {
  title: string
  description?: string
}

const props = withDefaults(defineProps<Props>(), {
  description: ''
})

const emit = defineEmits<{
  close: []
}>()
</script>

<template>
  <div class="card">
    <h2 class="card__title">{{ title }}</h2>
    <p class="card__description">{{ description }}</p>
    <button class="card__close" @click="emit('close')">
      {{ $t('common.close') }}
    </button>
  </div>
</template>

<style lang="scss" src="./Card.scss" />
```

### Rule for tests

```yaml
---
description: Standards for unit tests
globs: ["**/*.spec.ts", "**/*.test.ts"]
---

# Unit tests

## Framework
- Vitest + @vue/test-utils

## Structure
- describe() groups by component/function
- it() with a clear description of expected behavior
- Arrange → Act → Assert

## Naming
- Describe behavior, not implementation
- GOOD: "should show error message when email is invalid"
- BAD: "should call setError with string"

## Example

import { mount } from '@vue/test-utils'
import { describe, it, expect } from 'vitest'
import ProductCard from './ProductCard.vue'

describe('ProductCard', () => {
  it('should display the product name', () => {
    const wrapper = mount(ProductCard, {
      props: { name: 'Test Product', price: 99.90 }
    })

    expect(wrapper.text()).toContain('Test Product')
  })
})
```

---

## How to know if your rules work

### Quick test

1. Open a new session
2. Ask for something that should be covered by the rule
3. Check whether the agent followed the pattern without you asking

**Example:**

```
Create a simple button component.
```

If the Vue component rule works, the agent should automatically:

- Use `<script setup lang="ts">`
- Follow BEM in CSS
- Use i18n for strings
- Create external SCSS

If not, review the rule — maybe `alwaysApply: false` or the description is unclear.

---

## Common mistakes when creating rules

| Mistake           | Problem                         | Fix                             |
| ----------------- | ------------------------------- | ------------------------------- |
| Rule too vague    | Agent does not know what to do  | Be specific, include examples   |
| Too many rules    | Pollutes context, hurts quality | Keep only essentials            |
| Conflicting rules | Agent gets confused             | Review and unify                |
| No examples       | Agent misinterprets             | Always include code examples    |
| Wrong frontmatter | Rule does not load              | Check YAML and `.mdc` extension |

---

## Summary

1. Rules live in `.cursor/rules/*.mdc`
2. Start with one general rule (`alwaysApply: true`)
3. Add specific rules as needed (`globs`)
4. Include code examples — the agent learns by example
5. Test by creating something new and checking the pattern
6. Update as the project evolves

---

> **Next:** [04 — Skills](../04-skills/01-o-que-sao-skills.md) — automate workflows with skills
