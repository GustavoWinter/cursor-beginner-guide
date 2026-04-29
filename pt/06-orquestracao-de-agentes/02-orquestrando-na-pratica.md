# Orquestrando na Pratica — Passo a Passo

> Desenhe um fluxo consciente: **skill** define o processo, **agente** implementa, **sub-agente** apoia quando fizer sentido.

---

## Quando montar um fluxo de orquestracao

Faca isso quando:

- A tarefa tem **varias etapas** e voce ja repetiu prompt parecido antes
- Voce precisa **explorar muito codigo** antes de tocar em arquivos
- Varias pessoas no time devem chegar ao **mesmo resultado**
- Voce quer **menos ruido** no contexto da conversa principal

---

## Passo a passo

### 1. Liste o resultado final

Escreva em uma linha o que deve existir quando terminar (arquivos, PR, testes passando). Isso vira criterio de sucesso para o **agente principal**.

**Exemplo:** "Nova rota `/relatorios` com pagina, teste de fumaca e entrada no menu."

---

### 2. Separe "padrao" de "processo"

- **Padrao** (linguagem, pastas, testes) → ja deve estar em **regras**.
- **Processo** (ordem dos arquivos, checklist, deploy) → candidato a **skill**.

Se o processo tiver mais de tres passos repetiveis, crie ou atualize `.cursor/skills/<nome>/SKILL.md`.

---

### 3. Escreva a skill com os tres publicos em mente

No `SKILL.md`, deixe explicito:

1. **Quando usar** — gatilhos para o agente principal carregar a skill.
2. **Passos ordenados** — o que fazer em sequencia.
3. **Validacao** — checkboxes que o agente pode seguir antes de encerrar.

Assim o **agente** nao improvisa a ordem; ele **segue o roteiro**.

Trecho minimo de estrutura:

```markdown
# Nome da skill

> Uma linha: o que entrega e quando usar.

## Trigger

- Pedidos como: "..."
- Quando existir: ...

## Passos

### 1. ...

### 2. ...

## Validacao

- [ ] ...
```

---

### 4. Decida se precisa de sub-agente

Antes de editar, pergunte: "Preciso de **mapa amplo** do repo sem carregar tudo na conversa principal?"

- **Sim** — use um sub-agente de **exploracao** (somente leitura): pedido claro do que descobrir (pastas-chave, padroes, arquivos similares).
- **Nao** — siga direto com o **agente principal** e a skill.

**Bom pedido para sub-agente:**

```
Explore onde rotas e paginas sao registradas neste projeto.
Resuma: arquivos principais, 1 exemplo existente, convencoes de nome.
Nao sugira mudancas ainda.
```

**O que voce faz depois:** cola o resumo na conversa do **agente principal** e pede para implementar **seguindo a skill** X.

---

### 5. Execute com o agente principal

Na sessao principal:

1. Mencione a **skill** se ela nao for detectada sozinha.
2. Anexe **contexto minimo** (arquivos abertos, `@arquivo` pontuais).
3. Peça para **citar** onde aplicou cada passo da skill (facilita revisar).

**Exemplo de prompt:**

```
Use a skill `create-page` (em .cursor/skills/create-page/SKILL.md).
Implemente a pagina de relatorios conforme o resumo de exploracao abaixo.
[...cole o resumo do sub-agente...]
```

---

### 6. Revise como orquestrador humano

Checklist rapido:

- [ ] Regras respeitadas (lint, estilo, i18n)?
- [ ] Passos da skill todos cobertos?
- [ ] Nada de instrucoes contraditorias entre skill e regra (se houver, ajuste a skill)?

---

## Exemplo completo (narrativa)

**Cenario:** adicionar um endpoint e um client no SDK interno.

1. **Sub-agente:** mapear onde outros endpoints do SDK sao definidos e como testes sao nomeados.
2. **Skill `add-sdk-endpoint`:** passos — contrato, implementacao, teste, exemplo no README do pacote.
3. **Agente principal:** implementa usando o resumo + skill; abre PR.

Se algo no repo mudou, voce atualiza so a **skill** (e as **regras**, se o padrao mudou).

---

## Organizando skills para orquestracao

Evite um "deus skill" que faz tudo. Prefira:

```
.cursor/skills/
├── explore-feature-area/   ← pode ser acionada por exploracao
├── add-sdk-endpoint/       ← processo fechado
└── release-internal-pkg/   ← outro processo
```

Skills **pequenas e compostaveis** sao mais faceis de acionar na ordem certa pelo agente principal.

---

## Testando o fluxo

1. Nova conversa (contexto limpo).
2. Repita apenas o **pedido curto** + referencia a skill.
3. Verifique se o agente carregou a skill e se os passos batem com o PR.
4. Opcional: rode de novo com **sub-agente** desligado na primeira fase e compare qualidade do resultado.

---

## Resumo

1. Defina **resultado final** e o que e **padrao** (regra) vs **processo** (skill).
2. Mantenha `SKILL.md` com trigger, passos e validacao.
3. Use **sub-agente** para exploracao/resumo; **agente principal** para edicao.
4. Itere skills quando o fluxo real do time mudar.

---

> **Proximo:** [05 - Guias Praticos](../05-guias-praticos/01-exercicio-ask-mode.md) — pratique modos e fluxos no projeto
