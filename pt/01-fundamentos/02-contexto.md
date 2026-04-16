# Contexto: O Conceito Mais Importante

> Tudo que o agente sabe vem do **contexto**. Se voce entender isso, entende 80% de como trabalhar com IA.

---

## O que e contexto?

Contexto e **toda informacao que o agente recebe** antes de gerar uma resposta. Isso inclui:

- O seu prompt (o que voce escreveu)
- O historico da conversa (tudo que ja foi dito nessa sessao)
- Arquivos que voce referenciou com `@`
- Regras do projeto (`.cursor/rules/`)
- Skills carregadas
- Ferramentas MCP habilitadas
- Informacoes do sistema (SO, terminal, estrutura de pastas)

Tudo isso junto forma a **janela de contexto** — o "campo de visao" do agente.

---

## Por que contexto importa?

### 1. Contexto e caro

Cada token (pedaco de texto) que entra no contexto custa dinheiro. E o mais importante: **todo o historico e reenviado a cada nova mensagem**. Isso significa que uma conversa longa fica progressivamente mais cara.

### 2. Mais contexto NEM SEMPRE e melhor

Pesquisas mostram que a qualidade das respostas **degrada** quando a janela de contexto ultrapassa ~50% da capacidade. O agente comeca a "se perder" no meio de tanta informacao.

```
 0-50% contexto  →  Qualidade boa
50-80% contexto  →  Qualidade comeca a cair
80%+   contexto  →  "Zona burra" — respostas inconsistentes
```

### 3. Contexto ruim contamina tudo

Pior do que contexto demais e contexto **errado**. Exemplos:

- Misturar duas tarefas diferentes na mesma sessao
- Comentarios desatualizados no codigo
- Tentativas anteriores que falharam (o agente pode repetir os mesmos erros)
- Tentar "corrigir a rota" depois de muitas mensagens erradas

---

## As 4 Estrategias de Gerenciamento de Contexto

### 1. Persistir fora da janela

Guarde informacoes importantes em arquivos que o agente pode consultar quando precisar, em vez de tentar manter tudo na conversa.

**Onde guardar:**

- `.cursor/rules/` — regras que o agente carrega automaticamente
- `agents.md` ou `AGENTS.md` — contexto geral do projeto
- `.cursor/skills/` — workflows reutilizaveis
- Arquivos de plano (`plans/`) — decisoes e estrategias

### 2. Ser seletivo

Traga para o contexto **apenas o que e relevante para este passo**. Nao carregue tudo que "pode ser util".

**Exemplos praticos no Cursor:**

- Use `@arquivo.ts` para referenciar apenas os arquivos relevantes
- Desabilite MCPs que nao sao necessarios para a tarefa atual
- Nao cole documentacao inteira — cite apenas a parte relevante

### 3. Resumir e comprimir

Depois de uma sessao longa de debug, o contexto esta cheio de tentativas, erros e voltas. Antes de prosseguir:

1. Peca ao agente: _"Resuma o que descobrimos e qual e a solucao"_
2. Leia o resumo e valide
3. Abra uma **nova sessao** com apenas o resumo como ponto de partida

> IA e excelente em escrever prompts para IA. Use isso a seu favor.

### 4. Isolar contexto

Divida trabalho em sessoes separadas. Cada sessao deve ter **uma tarefa clara**.

| Ruim                                                                                       | Bom                                |
| ------------------------------------------------------------------------------------------ | ---------------------------------- |
| Uma sessao para "refatorar o sistema de auth e adicionar testes e corrigir o bug do login" | Sessao 1: pesquisar o bug do login |
|                                                                                            | Sessao 2: planejar a refatoracao   |
|                                                                                            | Sessao 3: implementar as mudancas  |

---

## Sinais de que o Contexto esta Poluido

Fique atento a estes sinais durante uma sessao:

- O agente comeca a **repetir erros** que voce ja corrigiu
- As respostas ficam **genericas** em vez de especificas
- O agente **esquece** instrucoes que voce deu antes
- O agente sugere coisas que **contradizem** o que voce combinou
- Voce sente que esta "lutando" contra o agente

**Quando isso acontecer:** pare, abra uma nova sessao e comece limpo.

---

## Contexto no Cursor — Onde Fica Cada Coisa

```
Sempre no contexto:
├── Regras always-on (.cursor/rules/ com alwaysApply: true)
├── Informacoes do sistema (OS, terminal, git status)
└── System prompt do modo ativo (Ask, Agent, Plan)

Adicionado por voce:
├── @arquivo.ts — arquivo especifico
├── @pasta/ — pasta inteira
├── Texto do seu prompt
└── Historico da conversa atual

Adicionado sob demanda:
├── Skills (quando referenciadas)
├── Regras contextuais (quando o agente detecta relevancia)
└── Ferramentas MCP (descricoes das ferramentas habilitadas)
```

---

## Habitos Praticos

1. **Uma tarefa por sessao** — nao misture assuntos
2. **Fique de olho no tamanho do contexto** — se a conversa esta longa, provavelmente e hora de uma nova sessao
3. **Se sentir que algo esta errado, confie no instinto** — comece uma nova sessao
4. **Peca resumos** — antes de nova sessao, peca ao agente para resumir o estado atual
5. **Desabilite MCPs que nao esta usando** — cada MCP adiciona tokens ao contexto

---

## Resumo

| Conceito             | O que significa                                       |
| -------------------- | ----------------------------------------------------- |
| Contexto e tudo      | O agente so sabe o que esta na janela de contexto     |
| Menos e mais         | Contexto excessivo degrada qualidade                  |
| Lixo entra, lixo sai | Contexto ruim produz resultado ruim                   |
| Persista fora        | Use regras, skills e arquivos para guardar informacao |
| Isole                | Uma tarefa, uma sessao                                |

---

> **Proximo:** [03 - O Workflow Pesquisar → Planejar → Implementar](./03-workflow.md)
