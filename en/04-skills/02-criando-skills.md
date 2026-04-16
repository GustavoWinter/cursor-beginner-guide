# Creating skills — step by step

> Learn to turn repetitive tasks into automated workflows.

---

## When to create a skill

Create a skill when:

- You do the **same thing more than twice**
- The process has **more than three steps**
- **Other people** on the team need to do the **same task**
- You want **consistent** results

---

## Step by step

### 1. Create the folder structure

```
mkdir -p .cursor/skills/skill-name
```

### 2. Create the SKILL.md file

The file must be named `SKILL.md` (capital letters) inside the skill folder.

```
.cursor/
└── skills/
    └── skill-name/
        └── SKILL.md
```

### 3. Write the skill

Recommended structure:

```markdown
# Skill name

> One-line description: what it does and when to use it.

## Trigger
Use this skill when:
- The user asks to [action]
- The user mentions [keyword]

## Prerequisites
- What must exist before starting

## Steps

### 1. Step name
Detailed instructions.

### 2. Step name
Detailed instructions.

## Validation
How to verify everything worked.

## Example
Sample prompt and expected result.
```

---

## Full example: create page skill

Create a skill for adding a new page to the project:

```
mkdir -p .cursor/skills/create-page
```

Contents of `SKILL.md`:

```markdown
# Create new page

> Creates a new page with route, component, and i18n.
> Use when the user asks to create a page, screen, or view.

## Trigger
- "Create a new page"
- "Add a screen for..."
- "I need a new view for..."

## Prerequisites
- Page name
- Desired route (e.g. /products, /settings)

## Steps

### 1. Create the page component
- Location: `src/pages/[PageName]/[PageName].vue`
- Use `<script setup lang="ts">`
- Basic structure with title and content slot

### 2. Create styles file
- Location: `src/pages/[PageName]/[PageName].scss`
- Root class with BEM
- Basic layout styles

### 3. Register the route
- File: `src/router/index.ts`
- Add route with lazy loading
- Include meta title

Example:
{
  path: '/page-name',
  name: 'PageName',
  component: () => import('@/pages/PageName/PageName.vue'),
  meta: { title: 'Page Title' }
}

### 4. Create i18n file
- Location: `src/i18n/pages/page-name.json`
- Include at least the page title

### 5. Create basic test
- Location: `src/pages/[PageName]/__tests__/[PageName].spec.ts`
- Test that the page renders without error
- Test that the title appears

## Validation
- [ ] Component created with default structure
- [ ] SCSS created with BEM
- [ ] Route registered with lazy loading
- [ ] i18n file created
- [ ] Basic test created and passing
- [ ] Page reachable in the browser at the route

## Example usage

User prompt:
> Create a new user settings page at /settings

Expected result:
- src/pages/UserSettings/UserSettings.vue
- src/pages/UserSettings/UserSettings.scss
- src/pages/UserSettings/__tests__/UserSettings.spec.ts
- src/i18n/pages/user-settings.json
- Route /settings added in src/router/index.ts
```

---

## Asking the agent to create the skill

You can ask the agent to create skills based on what it sees in the project:

```
Analyze how existing pages are structured in this project.
Based on that, create a skill at .cursor/skills/create-page/SKILL.md
documenting the full process to create a new page.

The skill should include:
- All files that must be created
- The correct order of steps
- Examples based on what already exists
- A validation checklist
```

---

## Organizing skills

As you add more skills, keep them organized:

```
.cursor/
└── skills/
    ├── create-vue-component/    ← creation
    │   └── SKILL.md
    ├── create-page/             ← creation
    │   └── SKILL.md
    ├── code-review/             ← quality
    │   └── SKILL.md
    ├── pre-commit-check/        ← quality
    │   └── SKILL.md
    └── deploy/                  ← operations
        └── SKILL.md
```

---

## Skills with reference files

Skills can include extra files in the same folder for the agent to use as reference:

```
.cursor/
└── skills/
    └── create-vue-component/
        ├── SKILL.md
        ├── template.vue         ← reference template
        └── template.scss        ← reference SCSS template
```

In `SKILL.md`, you can reference:

```markdown
### 1. Create the component
Use `template.vue` as a base and adapt for your case.
```

---

## Testing your skill

1. Open a new session in Cursor
2. Make a request that should trigger the skill
3. Check whether the agent:
   - Detected and loaded the skill
   - Followed the steps in order
   - Created all listed files
   - The result follows your standards

If the skill was not detected, check:
- Is the file named `SKILL.md` (capital letters)?
- Is the description clear about when to use it?
- Is the folder under `.cursor/skills/`?

---

## Summary

1. Create the folder under `.cursor/skills/skill-name/`
2. Create `SKILL.md` with clear, ordered steps
3. Include examples and a validation checklist
4. Test in a new session
5. Iterate as you use it

---

> **Next:** [05 — Hands-on guides](../05-guias-praticos/01-exercicio-ask-mode.md) — time to practice!
