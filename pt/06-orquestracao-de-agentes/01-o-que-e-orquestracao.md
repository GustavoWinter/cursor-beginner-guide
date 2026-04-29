# Orquestracao de Agentes — Visao Geral

> **Agente** executa. **Sub-agente** delega trabalho isolado. **Skill** documenta o processo.
> Orquestrar e escolher qual peca usar em cada momento.

---

## O que e orquestracao de agentes?

**Orquestracao** e a forma como voce combina o **agente principal** (a conversa onde voce pede mudancas), **sub-agentes** (sessoes especializadas ou em segundo plano que exploram ou executam tarefas isoladas) e **skills** (playbooks em arquivo que o agente segue sob demanda) para obter resultado previsivel sem perder contexto nem repetir prompt gigante.

Pense em tres camadas:

| Camada        | Papel resumido                                              |
| ------------- | ----------------------------------------------------------- |
| **Skill**     | *O que fazer* — passos reutilizaveis, versionados no repo   |
| **Agente**    | *Quem executa* no seu projeto — ferramentas, arquivos, PR   |
| **Sub-agente**| *Quem ajuda em paralelo ou a parte* — ferramentas, MCP, terminal, edicoes conforme o escopo; muitas vezes exploracao ou resumo |

Quando essas tres ideias estao alinhadas, voce nao depende de "sorte no prompt": voce **dirige** o fluxo.

---

## Os tres pilares

### 1. Skill — o playbook

Skills sao fluxos em `.cursor/skills/` (arquivo `SKILL.md`) que descrevem **passos**, **gatilhos** e **validacao**. O agente principal carrega uma skill quando o pedido combina com a descricao ou quando voce pede explicitamente.

**Na orquestracao:** a skill e o **roteiro**. Ela reduz ambiguidade: o agente sabe a ordem das acoes e o que entregar ao final.

> Detalhes: [04 - Skills](../04-skills/01-o-que-sao-skills.md).

### 2. Agente (principal) — o executor no projeto

O **agente principal** e a sessao interativa (por exemplo, no modo Agent) que tem acesso ao seu workspace, regras carregadas, terminal, busca no codigo e edicoes. E ele quem aplica **regras** sempre que faz sentido e **skills** quando o contexto pede.

**Na orquestracao:** o agente principal e o **maestro no repositorio** — quem mantem coerencia com o restante do codigo e com as convenções do time.

### 3. Sub-agente — delegacao com contexto proprio

**Sub-agentes** sao execucoes **separadas** do fio principal: outro contexto (ou outro foco). Eles **nao** ficam limitados a ler arquivos — conforme a tarefa e o modo, podem **rodar comandos**, **chamar ferramentas MCP**, usar o **terminal** e **editar arquivos** como o agente principal. Um padrao comum continua sendo trabalho de **objetivo unico** (explorar o repo, revisar padroes, preparar um resumo) para a conversa principal nao inchhar. O que produzem volta **condensado** para o agente principal, que **integra** (e em refactors amplos costuma ser quem **aplica** mudancas para manter tudo coerente).

**Na orquestracao:** sub-agente e **dividir para conquistar** — exploracao ampla ou tarefa longa sem encher o contexto da conversa principal com milhares de linhas.

O Cursor ainda oferece **sub-agentes nativos** (por exemplo exploracao, bash, browser) e **sub-agentes customizados**: cada um e um arquivo Markdown com *frontmatter* YAML. No **projeto**, coloque esses arquivos em **`.cursor/agents/`** (nome da pasta em ingles `agents`, dentro de `.cursor` — nao e uma pasta `agentes` na raiz do repo; o produto carrega por esse caminho). Para todos os seus projetos, use `~/.cursor/agents/`. Campos e precedencia: [Subagents — documentacao Cursor](https://cursor.com/docs/subagents). Para um **modelo de arquivo** no estilo oficial (YAML + corpo), siga [02 - Orquestrando na pratica](./02-orquestrando-na-pratica.md).

---

## Quando usar o que?

| Necessidade                         | Melhor escolha tendencial        |
| ----------------------------------- | -------------------------------- |
| Processo repetido no mesmo projeto  | **Skill**                        |
| Implementar, refatorar, commit      | **Agente principal**             |
| Mapear codebase grande sem editar   | **Sub-agente** de exploracao   |
| Varias frentes de pesquisa em paralelo | **Sub-agentes** em paralelo |
| Padrao global (estilo, stack)       | **Regras** (complementam tudo)   |

Regras continuam sendo a base: dizem **como** o codigo deve ser. Skills dizem **o que fazer** em tarefas especificas. O agente principal **aplica** ambos. Sub-agentes **informam**, preparam ou executam acoes isoladas (incluindo MCP e terminal); o agente principal ainda **coordena** o que entra no plano compartilhado para a sessao permanecer coerente.

---

## Fluxo mental simples

```
Regra (sempre) → Skill (se aplicavel) → Agente principal (edita)
                      ↑
              Sub-agente (opcional: explorar / MCP / terminal / resumo)
```

1. Garanta que **regras** cobrem o essencial do projeto.
2. Para tarefas que se repetem, tenha uma **skill** com passos e checklist.
3. Use o **agente principal** para implementar seguindo skill e regras.
4. Acione **sub-agente** quando precisar de exploracao ampla, preparacao com ferramentas (MCP, terminal) ou entrega resumida antes de codar.

---

## Erros comuns

| Erro                                      | Efeito                          | Ajuste                                      |
| ----------------------------------------- | ------------------------------- | ------------------------------------------- |
| Prompt enorme toda vez                    | Inconsistencia, cansaco         | Extrair para **skill** ou **regra**       |
| Sub-agente para tudo                    | Overhead, perda de visao        | Usar so quando **isolamento** ajuda       |
| Muitas skills sobrepostas               | Conflito de instrucoes          | Uma skill por **proposito** claro         |
| Ignorar o agente principal no refactor  | PRs incoerentes com o repo      | Quem **edita** deve ver o projeto inteiro |

---

## Resumo

| Conceito          | Lembrete em uma frase                                      |
| ----------------- | ---------------------------------------------------------- |
| **Skill**         | Roteiro versionado; acionado sob demanda                   |
| **Agente**        | Executor no workspace com regras, tools e contexto vivo  |
| **Sub-agente**    | Ajuda lateral com contexto proprio; ferramentas/MCP/terminal permitidos; devolve resumo ou repasse |
| **Orquestracao**  | Combinar os tres (e regras) na ordem certa para cada tarefa |

---

> **Proximo:** [02 - Orquestrando na pratica](./02-orquestrando-na-pratica.md) — passo a passo para desenhar um fluxo com skill, agente e sub-agente
