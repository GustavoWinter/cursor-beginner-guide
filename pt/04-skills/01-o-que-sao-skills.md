# Skills — Workflows Reutilizaveis

> Regras dizem **como** fazer. Skills dizem **o que** fazer.
> Sao playbooks que o agente executa sob demanda.

---

## O que sao Skills?

Skills sao **fluxos de trabalho completos** que o agente pode executar quando solicitado. Enquanto regras definem padroes ("use BEM", "use i18n"), skills definem processos ("para criar um componente Vue, siga estes 7 passos").

Pense em skills como **receitas de bolo** — instrucoes passo a passo para realizar uma tarefa especifica de forma consistente.

---

## Regras vs. Skills

| Aspecto             | Regras                                         | Skills                                                                             |
| ------------------- | ---------------------------------------------- | ---------------------------------------------------------------------------------- |
| **O que fazem**     | Definem padroes e convencoes                   | Definem fluxos de trabalho completos                                               |
| **Quando carregam** | Automaticamente (always apply) ou por contexto | Sob demanda (quando voce pede)                                                     |
| **Analogia**        | Manual de estilo                               | Receita de bolo                                                                    |
| **Exemplo**         | "Use BEM para CSS"                             | "Para criar um componente: 1) crie o .vue, 2) crie o .scss, 3) crie o .spec.ts..." |
| **Tamanho**         | Geralmente curtas e focadas                    | Geralmente longas e detalhadas                                                     |
| **Onde ficam**      | `.cursor/rules/`                               | `.cursor/skills/`                                                                  |

---

## Quando usar Skills

| Situacao              | Exemplo de skill                                                  |
| --------------------- | ----------------------------------------------------------------- |
| Tarefa repetitiva     | "Criar componente Vue" — toda vez o mesmo fluxo                   |
| Processo multi-etapas | "Do PBI ao PR" — buscar card, implementar, criar branch, abrir PR |
| Padrao complexo       | "Code review" — checklist de validacao com multiplos criterios    |
| Onboarding            | "Setup do projeto" — passos para configurar ambiente local        |
| Fluxo de deploy       | "Deploy" — criar branch, atualizar changelog, tag, PR             |

---

## Anatomia de uma Skill

Skills ficam em `.cursor/skills/` e seguem esta estrutura:

```
.cursor/
└── skills/
    └── nome-da-skill/
        └── SKILL.md
```

### O arquivo SKILL.md

```markdown
# Nome da Skill

> Descricao curta: quando e por que usar esta skill.

## Quando usar

- Situacao A
- Situacao B

## Passos

### 1. Primeiro passo

Instrucoes detalhadas...

### 2. Segundo passo

Instrucoes detalhadas...

### 3. Terceiro passo

Instrucoes detalhadas...

## Exemplo de uso

Prompt que o usuario pode usar para acionar esta skill.

## Output esperado

O que o usuario deve receber ao final.
```

---

## Como usar uma Skill

### Forma explicita

O Cursor detecta skills pela descricao no `SKILL.md`. Quando voce pede algo que corresponde a descricao, o agente carrega e segue a skill.

```
Crie um componente Vue para exibir detalhes de um pedido.
```

Se existir uma skill "create-vue-component" cuja descricao diz "Use quando criando novos componentes Vue", o agente vai carregar e seguir.

### Forma direta

Voce tambem pode referenciar diretamente:

```
Use a skill de criacao de componentes para criar um
componente de lista de notificacoes.
```

---

## Exemplos de Skills Uteis

### Skill: Criar Componente Vue

```markdown
# Criar Componente Vue

> Cria um componente Vue completo seguindo os padroes do projeto.
> Use quando criando novos componentes Vue.

## Passos

### 1. Criar o arquivo .vue

- Local: `src/components/[NomeDoComponente].vue`
- Usar `<script setup lang="ts">`
- Tipar todas as props e emits

### 2. Criar o arquivo .scss

- Local: `src/components/[NomeDoComponente].scss`
- Seguir metodologia BEM
- Usar apenas classes Tailwind customizadas

### 3. Criar o arquivo de i18n

- Local: `src/i18n/[feature]/[nome-componente].json`
- Extrair todos os textos visiveis

### 4. Criar o arquivo de teste

- Local: `src/components/__tests__/[NomeDoComponente].spec.ts`
- Cobrir renderizacao, props, eventos

### 5. Registrar o componente (se necessario)

- Verificar se precisa importar em algum index ou rota
```

### Skill: Code Review

```markdown
# Code Review

> Realiza code review seguindo os padroes do projeto.
> Use quando revisando PRs ou mudancas de codigo.

## Checklist

### Qualidade de codigo

- [ ] Nomes claros e descritivos
- [ ] Funcoes com responsabilidade unica
- [ ] Sem logica duplicada

### Padroes do projeto

- [ ] Composition API com script setup
- [ ] BEM para CSS
- [ ] i18n para textos
- [ ] SCSS externo

### Seguranca

- [ ] Sem credenciais hardcoded
- [ ] Inputs sanitizados
- [ ] Sem dados sensiveis em logs

### Testes

- [ ] Testes unitarios para nova logica
- [ ] Testes existentes passando
```

---

## Skills vs. Repetir instrucoes

| Cenario                      | Sem skill                           | Com skill                     |
| ---------------------------- | ----------------------------------- | ----------------------------- |
| Criar componente pela 1a vez | Escreve 15 linhas de prompt         | Escreve 15 linhas de prompt   |
| Criar componente pela 5a vez | Escreve 15 linhas de prompt de novo | "Crie um componente de X"     |
| Novo membro no time          | Precisa aprender os padroes         | Skill ja documenta o processo |
| Mudar o padrao               | Atualiza em cada sessao futura      | Atualiza uma vez no SKILL.md  |

A partir da **segunda vez** que voce faz algo, considere criar uma skill.

---

## Boas praticas para Skills

1. **Uma skill, um proposito** — nao misture "criar componente" com "fazer deploy"
2. **Passos claros e ordenados** — o agente segue na sequencia
3. **Inclua exemplos** — quanto mais concreto, melhor o resultado
4. **Defina o output esperado** — o que deve existir ao final da skill
5. **Atualize com frequencia** — se o processo mudou, atualize a skill

---

## Resumo

| Conceito                | Detalhe                                                   |
| ----------------------- | --------------------------------------------------------- |
| **O que sao**           | Fluxos de trabalho reutilizaveis                          |
| **Onde ficam**          | `.cursor/skills/nome-da-skill/SKILL.md`                   |
| **Quando usar**         | Tarefas repetitivas ou processos multi-etapas             |
| **Diferenca de regras** | Regras = padroes (como), Skills = processos (o que fazer) |
| **Beneficio**           | Consistencia e velocidade em tarefas repetidas            |

---

> **Proximo:** [02 - Criando Skills](./02-criando-skills.md) — tutorial para criar suas primeiras skills
