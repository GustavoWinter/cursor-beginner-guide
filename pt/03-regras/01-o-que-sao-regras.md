# Regras — Ensinando o Agente a Seguir Padroes

> Sem regras, voce repete as mesmas instrucoes a cada sessao.
> Com regras, o agente **sempre** sabe como o projeto funciona.

---

## O que sao regras?

Regras sao **instrucoes persistentes** que o agente carrega automaticamente. Em vez de repetir "use BEM para CSS" ou "siga o padrao de composables" em cada conversa, voce escreve isso uma vez como regra e o agente segue sempre.

Pense em regras como o **manual do desenvolvedor** do seu projeto — so que escrito para a IA ler.

---

## Por que regras importam?

### Sem regras

Voce abre uma nova sessao e escreve:

```
Crie um componente de card de produto.
Use BEM para CSS.
Use Composition API com script setup.
Use as classes do nosso Tailwind customizado.
Coloque textos em arquivos i18n.
Use SCSS externo, nao inline.
Siga o padrao dos outros componentes do projeto.
```

Na proxima sessao, voce tem que repetir tudo isso. E se esquecer algo, o agente gera codigo fora do padrao.

### Com regras

Voce abre uma nova sessao e escreve:

```
Crie um componente de card de produto.
```

O agente ja sabe todos os padroes porque as regras foram carregadas automaticamente.

---

## Tipos de regras no Cursor

As regras ficam na pasta `.cursor/rules/` do seu projeto. Existem diferentes tipos:

### 1. Always Apply (Sempre ativas)

Carregadas em **toda** interacao, independente do contexto.

**Quando usar:** Padroes que se aplicam a qualquer tarefa no projeto.

**Exemplos:**

- Convencoes de codigo (BEM, Composition API, etc.)
- Estrutura de pastas
- Padroes de nomenclatura

```yaml
---
description: Padroes gerais de desenvolvimento
alwaysApply: true
---
```

### 2. Auto Attached (Anexadas automaticamente)

Carregadas apenas quando o agente trabalha com **arquivos que correspondem a um padrao**.

**Quando usar:** Regras especificas para certos tipos de arquivo.

**Exemplos:**

- Regras de Vue quando trabalhando com `.vue`
- Regras de teste quando trabalhando com `.spec.ts`
- Regras de estilo quando trabalhando com `.scss`

```yaml
---
description: Padroes para componentes Vue
globs: ["**/*.vue"]
---
```

### 3. Agent Requested (Sob demanda do agente)

O agente **decide** se deve carregar com base na descricao da regra. Ele le a descricao e, se parecer relevante, carrega o conteudo completo.

**Quando usar:** Regras especializadas que nao sao necessarias o tempo todo.

**Exemplos:**

- Como fazer deploy
- Como criar uma nova pagina
- Como alterar precos

```yaml
---
description: Como criar novas paginas no CMS
---
```

### 4. Manual (So quando voce pede)

Carregadas apenas quando voce explicitamente referencia com `@`.

**Quando usar:** Regras muito especificas ou raramente usadas.

---

## Onde ficam as regras

```
seu-projeto/
├── .cursor/
│   └── rules/
│       ├── geral.mdc            ← always apply
│       ├── components/
│       │   └── vue.mdc          ← auto attached para .vue
│       ├── tests/
│       │   └── unit.mdc         ← auto attached para .spec.ts
│       └── deploy/
│           └── deploy.mdc       ← agent requested
```

As regras usam a extensao `.mdc` (Markdown com frontmatter de configuracao).

---

## Anatomia de uma regra

Uma regra `.mdc` tem duas partes:

### 1. Frontmatter (configuracao)

```yaml
---
description: Breve descricao do que esta regra faz
alwaysApply: true          # ou false
globs: ["**/*.vue"]        # opcional — padrao de arquivo
---
```

### 2. Conteudo (instrucoes em Markdown)

```markdown
# Padroes de Componentes Vue

## Obrigatorio
- Usar `<script setup lang="ts">`
- CSS externo em arquivo `.scss` separado
- Textos via i18n, nunca hardcoded
- Classes CSS seguindo BEM

## Proibido
- Nao usar Options API
- Nao usar CSS inline
- Nao usar classes Tailwind padrao (usar apenas as customizadas)
```

---

## Regras vs. Repetir no prompt


| Aspecto      | Repetir no prompt           | Usar regra                 |
| ------------ | --------------------------- | -------------------------- |
| Consistencia | Depende de voce lembrar     | Automatico                 |
| Manutencao   | Espalhado em N sessoes      | Centralizado em 1 arquivo  |
| Time         | Cada um repete do seu jeito | Todos seguem a mesma regra |
| Contexto     | Ocupa espaco toda vez       | Carregado inteligentemente |


---

## Dicas importantes

1. **Comece simples** — uma regra geral com os padroes mais importantes
2. **Nao exagere** — regras demais poluem o contexto (lembre do capitulo sobre contexto)
3. **Seja especifico** — *"use BEM"* e melhor que *"escreva CSS bem organizado"*
4. **Inclua exemplos** — o agente aprende melhor com exemplos concretos
5. **Atualize conforme aprende** — regras devem evoluir com o projeto

---

## Resumo


| Conceito       | Detalhe                                              |
| -------------- | ---------------------------------------------------- |
| **O que sao**  | Instrucoes persistentes para o agente                |
| **Onde ficam** | `.cursor/rules/*.mdc`                                |
| **Tipos**      | Always Apply, Auto Attached, Agent Requested, Manual |
| **Beneficio**  | Nao precisa repetir padroes a cada sessao            |
| **Cuidado**    | Regras demais poluem contexto — mantenha enxuto      |


---

> **Proximo:** [02 - Criando Regras](./02-criando-regras.md) — tutorial passo a passo para criar suas primeiras regras

