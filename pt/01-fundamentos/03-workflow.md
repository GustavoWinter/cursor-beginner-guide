# O Workflow: Pesquisar → Planejar → Implementar

> O erro numero 1 de quem comeca com IA: pular direto para a implementacao.
> Este capitulo ensina o fluxo que evita 80% dos problemas.

---

## O Erro Classico

A maioria dos desenvolvedores abre o Cursor e escreve algo como:

> _"Implemente um sistema de autenticacao com JWT"_

O agente obedece. Gera centenas de linhas de codigo. O problema? Ele assumiu:

- Qual biblioteca usar
- Como estruturar os arquivos
- Qual padrao de erro seguir
- Como armazenar os tokens
- Qual middleware usar

Se alguma dessas suposicoes estiver errada, voce vai gastar **mais tempo corrigindo** do que teria gasto planejando.

> _"Uma linha errada de pesquisa pode gerar centenas de linhas de codigo errado."_ — Dex Horthy

---

## O Fluxo Correto

```
┌─────────────┐     ┌─────────────┐     ┌──────────────┐
│  PESQUISAR  │ ──→ │  PLANEJAR   │ ──→ │ IMPLEMENTAR  │
│  (Ask Mode) │     │ (Plan Mode) │     │ (Agent Mode) │
└─────────────┘     └─────────────┘     └──────────────┘
     │                    │                     │
     ▼                    ▼                     ▼
  Entender o          Definir os           Executar com
  problema            passos               contexto limpo
```

Cada fase tem um **modo do Cursor** especifico. Cada fase produz um **output** que alimenta a proxima.

---

## Fase 1: Pesquisar (Ask Mode)

**Objetivo:** Entender o problema antes de resolver.

**Modo do Cursor:** Ask Mode (somente leitura — o agente nao pode alterar arquivos)

**O que fazer:**

- Como o sistema funciona hoje?
- Quais arquivos sao relevantes?
- Quais padroes o projeto ja usa?
- Como os dados fluem pelo sistema?
- Quais edge cases existem?

**Exemplo de prompt:**

```
Eu preciso adicionar um filtro de busca na listagem de produtos.
Me ajude a entender:

1. Como a listagem funciona hoje? Quais componentes estao envolvidos?
2. Ja existe algum filtro implementado em outra parte do sistema?
3. De onde vem os dados? Qual API e usada?
4. Quais padroes devo seguir com base no que ja existe?
```

**Output esperado:** Um entendimento claro do problema que voce valida como humano.

**Checkpoint humano:** _"Isso bate com o meu entendimento do sistema?"_

---

## Fase 2: Planejar (Plan Mode)

**Objetivo:** Definir exatamente o que vai ser feito, antes de fazer.

**Modo do Cursor:** Plan Mode (o agente le e sugere, mas pede aprovacao antes de executar)

**O que definir:**

- Quais arquivos serao criados ou alterados
- Qual a ordem das mudancas
- Como verificar se a mudanca esta correta (testes)
- O que esta **dentro** e **fora** do escopo

**Exemplo de prompt:**

```
Com base no que pesquisamos, crie um plano para adicionar o filtro
de busca na listagem de produtos.

O plano deve incluir:
- Arquivos que serao criados ou modificados
- Ordem de implementacao
- Como vamos testar cada mudanca
- O que NAO vamos alterar neste momento
```

**Output esperado:** Um documento de plano claro e passo-a-passo.

**Checkpoint humano:** _"Os passos fazem sentido? Falta algo? Tem algo fora do escopo?"_

---

## Fase 3: Implementar (Agent Mode)

**Objetivo:** Executar o plano com contexto minimo.

**Modo do Cursor:** Agent Mode (o agente pode ler, escrever, executar comandos)

**Como fazer:**

1. Abra uma **nova sessao** (contexto limpo)
2. Forneca apenas o plano como contexto
3. Implemente passo a passo
4. Revise cada mudanca antes de prosseguir
5. Faca commits frequentes

**Exemplo de prompt:**

```
Siga o plano abaixo para implementar o filtro de busca.
Implemente um passo de cada vez e me mostre o que mudou antes
de prosseguir para o proximo.

[cole o plano aqui ou referencie o arquivo com @plano.md]
```

**Por que nova sessao?**

- Contexto limpo = melhor qualidade
- Todo o "pensamento dificil" ja foi feito na pesquisa e no plano
- Voce pode ate usar um modelo menor/mais rapido porque o plano e explicito

---

## Por que este fluxo funciona

### 1. Evita suposicoes erradas

A pesquisa garante que voce e o agente entendem o sistema antes de altera-lo.

### 2. Facilita revisao

Com um plano explicito, voce sabe exatamente o que esperar. Revisar se o agente seguiu o plano e muito mais facil do que revisar codigo gerado "do nada".

### 3. Permite correcao de rota barata

Corrigir um plano custa uma mensagem. Corrigir centenas de linhas de codigo custa horas.

### 4. Reduz contexto na implementacao

Quando voce chega na Fase 3, o contexto e so o plano. Sem historico poluido.

---

## Quando NEM todo o fluxo e necessario

Nem toda tarefa precisa das 3 fases. Use seu julgamento:

| Tipo de tarefa             | Fluxo recomendado                      |
| -------------------------- | -------------------------------------- |
| Corrigir um typo           | Direto no Agent Mode                   |
| Adicionar um campo simples | Ask → Agent                            |
| Feature nova pequena       | Ask → Agent                            |
| Feature nova media/grande  | Ask → Plan → Agent                     |
| Refatoracao grande         | Ask → Plan → Agent (multiplas sessoes) |
| Bug complexo               | Ask (debug) → Plan → Agent             |
| Mudanca arquitetural       | Ask → Plan → revisao humana → Agent    |

A regra geral: **quanto maior o risco de dar errado, mais vale investir em pesquisa e planejamento**.

---

## Resumo

| Fase        | Modo  | Objetivo       | Output                    |
| ----------- | ----- | -------------- | ------------------------- |
| Pesquisar   | Ask   | Entender       | Diagnostico validado      |
| Planejar    | Plan  | Definir passos | Plano passo-a-passo       |
| Implementar | Agent | Executar       | Codigo pronto para review |

> _"IA nao substitui pensamento. Ela amplifica o pensamento que voce fez — ou a falta dele."_ — Dex Horthy

---

> **Proximo:** [02 - Modos do Cursor](../02-modos/01-ask-mode.md) — entenda cada modo em detalhes
