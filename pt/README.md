# Cursor para Desenvolvedores — Guia Completo

> Um guia pratico para aprender a trabalhar com IA no Cursor IDE.
> De iniciante a usuario avancado, passo a passo.

**Idioma:** Portugues · [English version](../en/README.md)

---

## Para quem e este guia?

Este material foi criado para desenvolvedores que estao comecando a usar o Cursor e querem ir alem do basico. Se voce ja sabe programar mas nunca usou um agente de IA para escrever codigo — ou usou mas sentiu que nao tirou o maximo proveito — este guia e para voce.

### Parte 1 — Nucleo do guia

Ao final da Parte 1, voce vai entender:

- Como **pensar** ao trabalhar com IA (o modelo mental correto)
- Como usar os **3 modos** do Cursor (Ask, Agent, Plan)
- Como criar **regras** para o agente seguir os padroes do seu projeto
- Como usar **skills** para automatizar fluxos de trabalho
- Como aplicar tudo isso na pratica com exercicios reais

### Parte 2 — Orquestracao de agentes

Material novo que complementa a Parte 1. Voce vai entender:

- Como combinar **skill**, **agente principal** e **sub-agente** em fluxos previsiveis
- Quando usar cada peca e como evitar desperdicio de contexto

---

## Estrutura do Guia

### Parte 1 — Nucleo (fundamentos ate exercicios)

### [01 - Fundamentos](./01-fundamentos/)

Antes de usar qualquer ferramenta, precisamos entender **como pensar** ao trabalhar com IA. Esta secao cobre o modelo mental correto, o conceito de contexto, e por que "usar IA" e diferente de "trabalhar com IA".

| Arquivo                                                     | Conteudo                                               |
| ----------------------------------------------------------- | ------------------------------------------------------ |
| [01-modelo-mental.md](./01-fundamentos/01-modelo-mental.md) | IA como junior dev — o que ela faz bem e o que nao faz |
| [02-contexto.md](./01-fundamentos/02-contexto.md)           | O que e contexto, por que importa, e como gerenciar    |
| [03-workflow.md](./01-fundamentos/03-workflow.md)           | O ciclo Pesquisar → Planejar → Implementar             |

### [02 - Modos](./02-modos/)

O Cursor tem 3 modos de interacao. Cada um tem um proposito especifico. Usar o modo certo na hora certa e a diferenca entre frustacao e produtividade.

| Arquivo                                         | Conteudo                                    |
| ----------------------------------------------- | ------------------------------------------- |
| [01-ask-mode.md](./02-modos/01-ask-mode.md)     | Modo somente leitura — pesquisar e entender |
| [02-plan-mode.md](./02-modos/02-plan-mode.md)   | Modo de planejamento — desenhar a solucao   |
| [03-agent-mode.md](./02-modos/03-agent-mode.md) | Modo de execucao — implementar mudancas     |

### [03 - Regras](./03-regras/)

Regras sao instrucoes permanentes que o agente segue automaticamente. Sao como um manual de boas praticas do seu projeto que o agente consulta sempre.

| Arquivo                                                      | Conteudo                        |
| ------------------------------------------------------------ | ------------------------------- |
| [01-o-que-sao-regras.md](./03-regras/01-o-que-sao-regras.md) | Conceito, tipos e quando usar   |
| [02-criando-regras.md](./03-regras/02-criando-regras.md)     | Como criar regras passo a passo |

### [04 - Skills](./04-skills/)

Skills sao fluxos de trabalho reutilizaveis que o agente executa sob demanda. Diferente de regras (que sao "sempre ligadas"), skills sao acionadas quando voce precisa.

| Arquivo                                                      | Conteudo                                   |
| ------------------------------------------------------------ | ------------------------------------------ |
| [01-o-que-sao-skills.md](./04-skills/01-o-que-sao-skills.md) | Conceito e diferenca entre regras e skills |
| [02-criando-skills.md](./04-skills/02-criando-skills.md)     | Como criar skills passo a passo            |

### [05 - Guias Praticos](./05-guias-praticos/)

Exercicios hands-on para aplicar tudo que aprendeu. Cada guia tem prompts reais para voce copiar, colar e ver o resultado.

| Arquivo                                                                                    | Conteudo                                    |
| ------------------------------------------------------------------------------------------ | ------------------------------------------- |
| [01-exercicio-ask-mode.md](./05-guias-praticos/01-exercicio-ask-mode.md)                   | Explorando um codebase sem alterar nada     |
| [02-exercicio-plan-mode.md](./05-guias-praticos/02-exercicio-plan-mode.md)                 | Planejando uma feature antes de codar       |
| [03-exercicio-agent-mode.md](./05-guias-praticos/03-exercicio-agent-mode.md)               | Implementando com o agente                  |
| [04-exercicio-regras.md](./05-guias-praticos/04-exercicio-regras.md)                       | Antes e depois de regras — veja a diferenca |
| [05-exercicio-skills.md](./05-guias-praticos/05-exercicio-skills.md)                       | Usando skills para automatizar tarefas      |
| [06-exercicio-workflow-completo.md](./05-guias-praticos/06-exercicio-workflow-completo.md) | Do zero ao PR — fluxo completo              |

### Parte 2 — Orquestracao de agentes

Skills, o agente principal e sub-agentes se complementam. Esta parte explica **quando** usar cada um e como montar um fluxo sem desperdicar contexto. **Leia apos Skills (04)** e, se quiser aplicar orquestracao nos exercicios, **antes dos Guias Praticos (05)**.

| Arquivo                                                                                    | Conteudo                                                         |
| ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- |
| [01-o-que-e-orquestracao.md](./06-orquestracao-de-agentes/01-o-que-e-orquestracao.md)       | Conceito: skill, agente, sub-agente e papel de cada um           |
| [02-orquestrando-na-pratica.md](./06-orquestracao-de-agentes/02-orquestrando-na-pratica.md) | Passo a passo para desenhar e testar um fluxo orquestrado         |

---

## Como usar este guia

1. **Parte 1** — siga **01 → 02 → 03 → 04** na ordem; em seguida os **Guias Praticos (05)** (ou intercale exercicios conforme preferir).
2. **Parte 2** — apos **04 - Skills**, leia **06 - Orquestracao**; depois volte aos **Guias Praticos (05)** se ainda nao os tiver feito, ou use a Parte 2 como referencia ao repetir exercicios.
3. **Faca os exercicios** — ler sobre IA nao substitui praticar com IA
4. **Experimente no seu projeto** — adapte os exemplos para o seu contexto
5. **Volte quando precisar** — use como referencia no dia a dia

---

## Pre-requisitos

- Cursor IDE instalado ([cursor.com](https://cursor.com))
- Um projeto existente para praticar (pode ser qualquer projeto)
- Conhecimento basico de programacao (qualquer linguagem)
- Vontade de experimentar e errar (faz parte do processo)
