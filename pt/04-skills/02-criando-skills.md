# Criando Skills — Passo a Passo

> Aprenda a transformar tarefas repetitivas em workflows automatizados.

---

## Quando criar uma Skill

Crie uma skill quando:

- Voce faz a **mesma coisa mais de duas vezes**
- O processo tem **mais de 3 passos**
- Outras pessoas no time precisam fazer a **mesma tarefa**
- Voce quer **consistencia** no resultado

---

## Passo a Passo

### 1. Crie a estrutura de pastas

```
mkdir -p .cursor/skills/nome-da-skill
```

### 2. Crie o arquivo SKILL.md

O arquivo deve se chamar `SKILL.md` (em maiusculas) e ficar dentro da pasta da skill.

```
.cursor/
└── skills/
    └── nome-da-skill/
        └── SKILL.md
```

### 3. Escreva a skill

A estrutura recomendada:

```markdown
# Nome da Skill

> Descricao em uma linha: o que faz e quando usar.

## Trigger

Use esta skill quando:

- O usuario pede para [acao]
- O usuario menciona [palavra-chave]

## Pre-requisitos

- O que precisa existir antes de comecar

## Passos

### 1. Nome do passo

Instrucoes detalhadas.

### 2. Nome do passo

Instrucoes detalhadas.

## Validacao

Como verificar se tudo deu certo.

## Exemplo

Prompt de exemplo e resultado esperado.
```

---

## Exemplo Completo: Skill de Criar Pagina

Vamos criar uma skill para adicionar uma nova pagina no projeto:

```
mkdir -p .cursor/skills/create-page
```

Conteudo do `SKILL.md`:

```markdown
# Criar Nova Pagina

> Cria uma nova pagina no projeto com rota, componente e i18n.
> Use quando o usuario pedir para criar uma pagina, tela ou view.

## Trigger

- "Crie uma nova pagina"
- "Adicione uma tela de..."
- "Preciso de uma nova view para..."

## Pre-requisitos

- Nome da pagina
- Rota desejada (ex: /produtos, /configuracoes)

## Passos

### 1. Criar o componente da pagina

- Local: `src/pages/[NomeDaPagina]/[NomeDaPagina].vue`
- Usar `<script setup lang="ts">`
- Incluir estrutura basica com titulo e slot de conteudo

### 2. Criar o arquivo de estilos

- Local: `src/pages/[NomeDaPagina]/[NomeDaPagina].scss`
- Criar classe raiz com BEM
- Incluir estilos basicos de layout

### 3. Registrar a rota

- Arquivo: `src/router/index.ts`
- Adicionar rota com lazy loading
- Incluir meta title

Exemplo:
{
path: '/nome-da-pagina',
name: 'NomeDaPagina',
component: () => import('@/pages/NomeDaPagina/NomeDaPagina.vue'),
meta: { title: 'Nome da Pagina' }
}

### 4. Criar arquivo de i18n

- Local: `src/i18n/pages/nome-da-pagina.json`
- Incluir ao menos o titulo da pagina

### 5. Criar teste basico

- Local: `src/pages/[NomeDaPagina]/__tests__/[NomeDaPagina].spec.ts`
- Testar que a pagina renderiza sem erro
- Testar que o titulo aparece

## Validacao

- [ ] Componente criado com estrutura padrao
- [ ] SCSS criado com BEM
- [ ] Rota registrada com lazy loading
- [ ] Arquivo i18n criado
- [ ] Teste basico criado e passando
- [ ] Pagina acessivel pela rota no browser

## Exemplo de uso

Prompt do usuario:

> Crie uma nova pagina de configuracoes do usuario acessivel em /settings

Resultado esperado:

- src/pages/UserSettings/UserSettings.vue
- src/pages/UserSettings/UserSettings.scss
- src/pages/UserSettings/**tests**/UserSettings.spec.ts
- src/i18n/pages/user-settings.json
- Rota /settings adicionada em src/router/index.ts
```

---

## Pedindo para o agente criar a Skill

Voce pode pedir ao agente para criar skills baseadas no que ele observa no projeto:

```
Analise como as paginas existentes sao estruturadas neste projeto.
Com base nisso, crie uma skill em .cursor/skills/create-page/SKILL.md
que documente o processo completo de criar uma nova pagina.

A skill deve incluir:
- Todos os arquivos que precisam ser criados
- A ordem correta dos passos
- Exemplos baseados no que ja existe
- Checklist de validacao
```

---

## Organizando Skills

Conforme voce cria mais skills, mantenha organizado:

```
.cursor/
└── skills/
    ├── create-vue-component/    ← Criacao
    │   └── SKILL.md
    ├── create-page/             ← Criacao
    │   └── SKILL.md
    ├── code-review/             ← Qualidade
    │   └── SKILL.md
    ├── pre-commit-check/        ← Qualidade
    │   └── SKILL.md
    └── deploy/                  ← Operacoes
        └── SKILL.md
```

---

## Skills com arquivos de referencia

Skills podem incluir arquivos extras na mesma pasta para o agente usar como referencia:

```
.cursor/
└── skills/
    └── create-vue-component/
        ├── SKILL.md
        ├── template.vue         ← template de referencia
        └── template.scss        ← template SCSS de referencia
```

No `SKILL.md`, voce pode referenciar:

```markdown
### 1. Criar o componente

Use o template em `template.vue` como base e adapte para o caso.
```

---

## Testando sua Skill

1. Abra uma nova sessao no Cursor
2. Faca um pedido que deveria acionar a skill
3. Verifique se o agente:
   - Detectou e carregou a skill
   - Seguiu os passos na ordem
   - Criou todos os arquivos listados
   - O resultado segue os padroes

Se a skill nao foi detectada, verifique:

- O arquivo se chama `SKILL.md` (maiusculas)?
- A descricao e clara sobre quando usar?
- A pasta esta dentro de `.cursor/skills/`?

---

## Resumo

1. Crie a pasta em `.cursor/skills/nome-da-skill/`
2. Crie o `SKILL.md` com passos claros e ordenados
3. Inclua exemplos e checklist de validacao
4. Teste em uma nova sessao
5. Itere e melhore conforme usa

---

> **Proximo:** [06 - Orquestracao de Agentes](../06-orquestracao-de-agentes/01-o-que-e-orquestracao.md) — skill, agente e sub-agente no mesmo fluxo
