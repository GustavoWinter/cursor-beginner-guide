# Exercicio 4: Regras na Pratica — Antes e Depois

> **Objetivo:** Ver a diferenca concreta que regras fazem no output do agente.
> **Modo:** Agent Mode
> **Tempo estimado:** 20 minutos

---

## O Cenario

Vamos pedir a mesma coisa ao agente **duas vezes**: primeiro sem regras, depois com regras. A diferenca vai ser clara.

---

## Parte A — SEM Regras

### Preparacao

1. Temporariamente renomeie a pasta `.cursor/rules` para `.cursor/rules-backup` (para desativar as regras)
2. Abra uma **nova sessao** em Agent Mode

### Prompt para copiar e colar:

```
Crie um componente Vue simples chamado AlertBanner que:
- Recebe um tipo (sucesso, erro, aviso)
- Recebe uma mensagem
- Tem um botao de fechar
- Emite um evento quando fechado
```

### O que observar e anotar:

Olhe o resultado e anote:


| Criterio                                      | O que o agente fez? |
| --------------------------------------------- | ------------------- |
| Usou Composition API ou Options API?          |                     |
| Usou TypeScript?                              |                     |
| Onde colocou o CSS? (inline, scoped, externo) |                     |
| Usou alguma metodologia CSS? (BEM, etc)       |                     |
| Textos estao hardcoded ou com i18n?           |                     |
| Criou arquivo de teste?                       |                     |
| Em qual pasta criou o componente?             |                     |
| Tipou as props?                               |                     |


**Nao aceite as mudancas. Apenas anote.**

---

## Parte B — COM Regras

### Preparacao

1. Restaure a pasta `.cursor/rules` (renomeie de volta)
2. Se voce nao tem regras ainda, crie uma regra basica. Abra uma nova sessao em Agent Mode:

```
Crie um arquivo .cursor/rules/components.mdc com o seguinte conteudo:

---
description: Padroes para criacao de componentes Vue
alwaysApply: true
---

# Padroes de Componentes Vue

## Obrigatorio
- Usar `<script setup lang="ts">`
- Tipar todas as props com interface TypeScript
- Tipar todos os emits
- CSS em arquivo SCSS externo (nunca inline, nunca scoped)
- Metodologia BEM para classes CSS
- Textos visiveis ao usuario via i18n (nunca hardcoded)

## Estrutura do arquivo .vue
1. `<script setup lang="ts">` (primeiro)
2. `<template>` (segundo)  
3. `<style lang="scss" src="./NomeDoComponente.scss" />` (terceiro)

## Nomenclatura
- Arquivo: PascalCase (ex: AlertBanner.vue)
- Classe CSS raiz: kebab-case (ex: .alert-banner)
- Elementos BEM: classe-raiz__elemento (ex: .alert-banner__title)
- Modificadores BEM: classe-raiz--modificador (ex: .alert-banner--error)

## Exemplo

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
```

1. Abra uma **nova sessao** (importante! contexto limpo)

### Mesmo prompt:

```
Crie um componente Vue simples chamado AlertBanner que:

- Recebe um tipo (sucesso, erro, aviso)
- Recebe uma mensagem
- Tem um botao de fechar
- Emite um evento quando fechado
```

### O que observar e anotar:

Anote da mesma forma:


| Criterio                        | Sem regra (Parte A) | Com regra (Parte B) |
| ------------------------------- | ------------------- | ------------------- |
| Composition API ou Options API? |                     |                     |
| Usou TypeScript?                |                     |                     |
| CSS inline, scoped ou externo?  |                     |                     |
| Metodologia CSS (BEM)?          |                     |                     |
| i18n para textos?               |                     |                     |
| Criou teste?                    |                     |                     |
| Pasta do componente?            |                     |                     |
| Props tipadas?                  |                     |                     |


---

## Parte C — Comparacao

### A diferenca deve ser visivel:

**Sem regras:**

- O agente faz **escolhas arbitrarias**
- Pode usar Options API ou Composition API
- CSS provavelmente fica inline ou scoped
- Textos ficam hardcoded
- Sem padrao de nomenclatura consistente

**Com regras:**

- O agente segue **exatamente** o que a regra define
- Composition API com script setup sempre
- SCSS externo com BEM sempre
- Textos com i18n sempre
- Nomenclatura consistente

### A licao principal:

> Regras transformam resultados imprevisíveis em resultados consistentes.
> O mesmo prompt gera codigo completamente diferente dependendo das regras.

---

## Exercicio Bonus — Regra Contextual

Crie uma regra que so carrega para arquivos de teste:

### Prompt:

```
Crie um arquivo .cursor/rules/tests.mdc com o conteudo:

---
description: Padroes para testes unitarios
globs: ["**/*.spec.ts", "**/*.test.ts"]
---

# Padroes de Testes

## Framework

- Vitest + @vue/test-utils

## Estrutura

- describe() para agrupar por componente
- it() com descricao em portugues do comportamento
- Padrao Arrange → Act → Assert

## Obrigatorio

- Testar renderizacao com props padrao
- Testar cada prop que altera visualmente o componente
- Testar eventos emitidos
- Testar estados de loading/erro quando aplicavel

## Nomenclatura

- Arquivo: [NomeDoComponente].spec.ts
- Describe: nome do componente
- It: "deve [comportamento esperado]"

```

Depois, abra uma nova sessao e peca:

```

Crie testes unitarios para o componente AlertBanner.

```

### O que observar:

- A regra de testes foi carregada automaticamente (por causa do `globs`)
- Os testes seguem o padrao definido
- Os `it()` estao em portugues conforme a regra

---

## Resumo do que Aprendemos

1. **Sem regras** — o agente improvisa e o resultado varia
2. **Com regras** — o agente segue padroes e o resultado e consistente
3. **Regras always-on** — carregam em toda interacao
4. **Regras com globs** — carregam apenas para tipos de arquivo especificos
5. **Investir em regras** — e investir em qualidade a longo prazo

---

> **Proximo:** [05 - Exercicio Skills](./05-exercicio-skills.md) — automatizando tarefas com skills

