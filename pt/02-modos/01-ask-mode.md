# Ask Mode — Pesquisar e Entender

> O modo mais subestimado do Cursor.
> Aqui voce transforma o agente em um **pesquisador** que so pode ler e conversar.

---

## O que e o Ask Mode?

O Ask Mode e um modo **somente leitura**. O agente pode:

- Ler arquivos do projeto
- Buscar no codebase
- Responder perguntas
- Analisar codigo

O agente **NAO pode**:

- Criar ou editar arquivos
- Executar comandos no terminal
- Fazer commits
- Alterar qualquer coisa no projeto

---

## Por que isso e poderoso?

Parece limitante, mas e exatamente o contrario. Ao remover a capacidade de agir, voce forca o agente a **pensar** em vez de sair executando.

Sem Ask Mode, o comportamento padrao e:

1. Voce pergunta algo
2. O agente imediatamente comeca a gerar codigo
3. Voce recebe 200 linhas que pode ou nao estar certas

Com Ask Mode:

1. Voce pergunta algo
2. O agente pesquisa, analisa, e **explica**
3. Voce entende o problema antes de tocar em qualquer codigo

---

## Como ativar o Ask Mode

No Cursor, no campo de chat, voce vera um seletor de modo. Clique nele e selecione **"Ask"**.

Voce tambem pode usar o atalho de teclado ou digitar diretamente no campo.

---

## Quando usar o Ask Mode

| Situacao                        | Exemplo de prompt                                                                         |
| ------------------------------- | ----------------------------------------------------------------------------------------- |
| **Entender codigo existente**   | _"Como funciona o sistema de autenticacao neste projeto?"_                                |
| **Investigar um bug**           | _"O que pode causar este erro? @arquivo-com-erro.ts"_                                     |
| **Comparar abordagens**         | _"Quais sao os pros e contras de usar Pinia vs composables para este caso?"_              |
| **Aprender padroes do projeto** | _"Quais padroes de componentes este projeto usa? Me mostre exemplos."_                    |
| **Preparar uma mudanca**        | _"Se eu precisar adicionar um novo campo no formulario, quais arquivos preciso alterar?"_ |
| **Revisar um conceito**         | _"Me explique como o Vue Router funciona neste projeto."_                                 |

---

## Exemplos de Prompts para Ask Mode

### Explorar o codebase

```
Me de uma visao geral da estrutura deste projeto.
Quais sao as pastas principais e o que cada uma contem?
```

### Investigar como algo funciona

```
Como os dados de produtos chegam ate o componente de listagem?
Trace o caminho desde a API ate o template.
Referencie os arquivos envolvidos.
```

### Preparar uma implementacao

```
Eu preciso adicionar validacao de CPF no formulario de cadastro.

1. Onde fica o formulario atual? Quais componentes estao envolvidos?
2. Ja existe alguma validacao similar no projeto que eu possa seguir como exemplo?
3. Quais arquivos eu precisaria alterar?
4. Tem algum utilitario de validacao ja criado?
```

### Entender um erro

```
Estou recebendo este erro:

[cole o erro aqui]

Analise o erro, veja os arquivos relevantes do projeto,
e me explique o que pode estar causando isso.
Nao corrija — apenas explique.
```

---

## Boas praticas no Ask Mode

1. **Seja especifico** — Em vez de _"como funciona o auth?"_, pergunte _"como o token JWT e validado no middleware de autenticacao?"_
2. **Referencie arquivos** — Use `@` para apontar arquivos especificos. Isso reduz ambiguidade e foca o agente.
3. **Peca referencias** — Termine com _"me mostre os arquivos e linhas relevantes"_ para obter respostas concretas.
4. **Nao tenha pressa** — O objetivo aqui e entender, nao resolver. Faca quantas perguntas precisar.
5. **Valide mentalmente** — Antes de sair do Ask Mode, se pergunte: _"Eu entendo o problema o suficiente para explicar para outra pessoa?"_

---

## O que o Ask Mode NAO faz

- Nao gera codigo para voce copiar e colar (esse e o papel do Agent Mode)
- Nao executa mudancas (nao pode)
- Nao substitui ler o codigo voce mesmo (mas acelera muito)

---

## Resumo

| Aspecto         | Detalhe                                    |
| --------------- | ------------------------------------------ |
| **Capacidade**  | Leitura e conversa apenas                  |
| **Quando usar** | Antes de implementar qualquer coisa        |
| **Objetivo**    | Entender o problema e o sistema            |
| **Resultado**   | Voce sai sabendo exatamente o que fazer    |
| **Erro comum**  | Pular direto para Agent Mode sem pesquisar |

---

> **Proximo:** [02 - Plan Mode](./02-plan-mode.md) — desenhando a solucao antes de implementar
