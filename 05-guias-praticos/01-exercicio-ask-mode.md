# Exercicio 1: Ask Mode na Pratica

> **Objetivo:** Aprender a explorar um codebase sem alterar nada.
> **Modo:** Ask Mode
> **Tempo estimado:** 15 minutos

---

## O Cenario

Voce acabou de entrar em um projeto novo. Precisa entender como ele funciona antes de fazer qualquer mudanca. Vamos usar o Ask Mode para pesquisar.

---

## Preparacao

1. Abra o Cursor em um projeto existente (pode ser qualquer projeto)
2. Mude para **Ask Mode** no seletor de modo
3. Abra o chat

---

## Exercicio 1.1 — Visao Geral do Projeto

### Prompt para copiar e colar:

```
Me de uma visao geral deste projeto:
1. Qual framework e linguagem sao usados?
2. Qual e a estrutura de pastas principal?
3. Quais sao os comandos de build, dev e teste?
4. Existem configuracoes especiais (linters, formatters, etc)?
```

### O que observar:

- O agente vai ler arquivos como `package.json`, `tsconfig.json`, a raiz do projeto
- Ele **nao vai alterar nada** — apenas ler e responder
- A resposta deve ser um resumo organizado do projeto

### Checkpoint:

> A resposta bate com o que voce sabe do projeto? Se sim, o agente entendeu o contexto.

---

## Exercicio 1.2 — Entender um Fluxo Especifico

Escolha uma funcionalidade do projeto e peca para o agente explicar como funciona.

### Prompt para copiar e colar:

```
Explique como funciona o fluxo de [FUNCIONALIDADE] neste projeto.

Quero entender:
1. Quais componentes/arquivos estao envolvidos?
2. Como os dados fluem (da API ate a tela)?
3. Existe algum estado global (store) envolvido?
4. Quais sao os pontos de entrada (rotas, eventos, etc)?

Referencie os arquivos e linhas especificos.
```

> Substitua `[FUNCIONALIDADE]` por algo do seu projeto. Exemplos:
>
> - "listagem de produtos"
> - "autenticacao do usuario"
> - "envio de formulario de contato"

### O que observar:

- O agente deve buscar e ler os arquivos relevantes
- A resposta deve referenciar caminhos de arquivos reais
- Se o agente pedir mais contexto, forneca com `@arquivo`

---

## Exercicio 1.3 — Investigar Antes de Implementar

Imagine que voce precisa adicionar uma feature. Use o Ask Mode para **pesquisar primeiro**.

### Prompt para copiar e colar:

```
Eu preciso adicionar [NOVA FEATURE] no projeto.

Antes de implementar, me ajude a entender:
1. Existe algo similar ja implementado que eu possa usar como referencia?
2. Quais arquivos eu precisaria criar ou alterar?
3. Existem padroes no projeto que eu deveria seguir?
4. Quais edge cases eu deveria considerar?
5. Tem alguma dependencia que eu precisaria adicionar?

NAO implemente nada — apenas pesquise e responda.
```

> Substitua `[NOVA FEATURE]` por algo simples. Exemplos:
>
> - "um filtro de busca na listagem"
> - "um botao de exportar para CSV"
> - "validacao de email no formulario"

### O que observar:

- O agente pesquisa mas **nao gera codigo**
- Ele deve encontrar padroes existentes para usar como referencia
- A resposta deve te dar confianca para prosseguir com planejamento

---

## Exercicio 1.4 — Comparar Abordagens

### Prompt para copiar e colar:

```
Preciso implementar [PROBLEMA]. 
Quais abordagens faria sentido neste projeto?

Compare pelo menos 2 opcoes, considerando:
- Prós e contras de cada uma
- Qual se alinha melhor com os padroes existentes
- Complexidade de implementacao
- Facilidade de manutencao

Recomende uma opcao e justifique.
```

### O que observar:

- O agente deve analisar o projeto real, nao dar conselhos genericos
- A recomendacao deve considerar o que ja existe no codebase
- Voce deve sair com uma decisao clara

---

## O que Aprendemos

Depois destes exercicios, voce deve ter percebido que:

1. **Ask Mode impede decisoes precipitadas** — voce nao pode gerar codigo mesmo que queira
2. **Pesquisar antes e rapido** — poucos minutos de pesquisa economizam horas de refatoracao
3. **O agente le o codebase real** — as respostas sao baseadas no seu projeto, nao em exemplos genericos
4. **Voce sai sabendo o que fazer** — e essa clareza que faz a implementacao ser mais rapida

---

## Proximo passo

Agora que voce sabe pesquisar, vamos **planejar**.

> **Proximo:** [02 - Exercicio Plan Mode](./02-exercicio-plan-mode.md)

