# Criando Regras — Passo a Passo

> Aprenda a criar regras que fazem o agente seguir os padroes do seu projeto automaticamente.

---

## Metodo 1: Pelo Cursor (recomendado para iniciantes)

O Cursor tem um comando para criar regras de forma guiada:

1. Abra a Command Palette (`Cmd+Shift+P` no Mac / `Ctrl+Shift+P` no Windows)
2. Digite **"Cursor: New Rule"**
3. Escolha o tipo de regra
4. De um nome
5. O Cursor cria o arquivo `.mdc` na pasta correta

---

## Metodo 2: Manualmente

### Passo 1: Crie a pasta (se nao existir)

```
mkdir -p .cursor/rules
```

### Passo 2: Crie o arquivo `.mdc`

Crie um arquivo com extensao `.mdc` dentro de `.cursor/rules/`.

### Passo 3: Adicione o frontmatter

```yaml
---
description: Padroes gerais de codigo do projeto
alwaysApply: true
---
```

### Passo 4: Escreva as instrucoes

```markdown
# Padroes do Projeto

## Linguagem e Framework

- Vue 3 com Composition API (`<script setup>`)
- TypeScript como padrao
- SCSS externo (nunca CSS inline)

## Nomenclatura

- Componentes: PascalCase (ex: `ProductCard.vue`)
- Composables: camelCase com prefixo `use` (ex: `useProducts.ts`)
- Arquivos de teste: mesmo nome + `.spec.ts` (ex: `ProductCard.spec.ts`)

## CSS

- Metodologia BEM para classes
- Usar apenas classes Tailwind customizadas do projeto
- Nunca usar classes Tailwind padrao

## i18n

- Todos os textos visiveis ao usuario devem usar i18n
- Nunca texto hardcoded no template
```

---

## Metodo 3: Pedir para o agente criar

Voce pode usar o proprio agente para criar regras. Este e um otimo caso de uso:

```
Analise os componentes existentes neste projeto e crie uma regra
em .cursor/rules/components.mdc que documente os padroes que
encontrar.

A regra deve ter alwaysApply: true e cobrir:
- Estrutura dos componentes (script setup, template, style)
- Padroes de CSS
- Padroes de nomenclatura
- Padroes de i18n
- O que NAO fazer

Inclua exemplos reais do projeto.
```

Isso e poderoso porque o agente vai **analisar o codigo real** e extrair os padroes que ja existem.

---

## Exemplos de Regras Uteis

### Regra geral do projeto

```yaml
---
description: Convencoes gerais do projeto
alwaysApply: true
---

# Convencoes do Projeto

## Stack
- Vue 3 + Composition API + TypeScript
- Vite como bundler
- Vitest para testes unitarios
- SCSS para estilos

## Comandos
- `npm run dev` — desenvolvimento local
- `npm run build` — build de producao
- `npm run test` — rodar testes
- `npm run lint` — verificar linting

## Regras gerais
- Nunca commitar sem rodar os testes
- Sempre tipar props e emits
- Componentes com mais de 200 linhas devem ser divididos
```

### Regra para componentes Vue

```yaml
---
description: Padroes para componentes Vue
globs: ["**/*.vue"]
---

# Componentes Vue

## Estrutura obrigatoria

O componente deve seguir esta ordem:
1. `<script setup lang="ts">` (primeiro)
2. `<template>` (segundo)
3. `<style>` com referencia a SCSS externo (terceiro)

## Exemplo

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

### Regra para testes

```yaml
---
description: Padroes para testes unitarios
globs: ["**/*.spec.ts", "**/*.test.ts"]
---

# Testes Unitarios

## Framework
- Vitest + @vue/test-utils

## Estrutura
- describe() para agrupar por componente/funcao
- it() com descricao clara do comportamento esperado
- Arrange → Act → Assert

## Nomenclatura
- Descrever comportamento, nao implementacao
- BOM: "deve exibir mensagem de erro quando email invalido"
- RUIM: "deve chamar setError com string"

## Exemplo

import { mount } from '@vue/test-utils'
import { describe, it, expect } from 'vitest'
import ProductCard from './ProductCard.vue'

describe('ProductCard', () => {
  it('deve exibir o nome do produto', () => {
    const wrapper = mount(ProductCard, {
      props: { name: 'Produto Teste', price: 99.90 }
    })

    expect(wrapper.text()).toContain('Produto Teste')
  })
})
```

---

## Como saber se suas regras estao funcionando

### Teste rapido

1. Abra uma nova sessao
2. Peca algo que deveria ser coberto pela regra
3. Verifique se o agente seguiu o padrao sem voce pedir

**Exemplo:**

```
Crie um componente simples de botao.
```

Se a regra de componentes Vue esta funcionando, o agente deve automaticamente:

- Usar `<script setup lang="ts">`
- Seguir BEM no CSS
- Usar i18n para textos
- Criar SCSS externo

Se ele nao seguiu, revise a regra — pode estar com `alwaysApply: false` ou a descricao pode nao ser clara.

---

## Erros comuns ao criar regras

| Erro                 | Problema                          | Solucao                          |
| -------------------- | --------------------------------- | -------------------------------- |
| Regra muito generica | Agente nao sabe o que fazer       | Seja especifico, inclua exemplos |
| Regras demais        | Polui contexto, degrada qualidade | Mantenha apenas o essencial      |
| Regras conflitantes  | Agente fica confuso               | Revise e unifique                |
| Sem exemplos         | Agente interpreta errado          | Sempre inclua exemplos de codigo |
| Frontmatter errado   | Regra nao carrega                 | Verifique YAML e extensao `.mdc` |

---

## Resumo

1. Regras ficam em `.cursor/rules/*.mdc`
2. Comece com uma regra geral (`alwaysApply: true`)
3. Adicione regras especificas conforme necessidade (`globs`)
4. Inclua exemplos de codigo — o agente aprende por exemplo
5. Teste criando algo novo e verificando se o padrao foi seguido
6. Atualize conforme o projeto evolui

---

> **Proximo:** [04 - Skills](../04-skills/01-o-que-sao-skills.md) — automatizando workflows com skills
