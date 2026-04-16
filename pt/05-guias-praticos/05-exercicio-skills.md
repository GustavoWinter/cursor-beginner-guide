# Exercicio 5: Skills na Pratica

> **Objetivo:** Criar e usar uma skill para automatizar um workflow repetitivo.
> **Modo:** Agent Mode
> **Tempo estimado:** 20 minutos

---

## O Cenario

Voce vai criar uma skill do zero, usar ela, e ver como simplifica tarefas repetitivas.

---

## Exercicio 5.1 — Criar uma Skill Simples

Vamos criar uma skill para gerar um componente Vue completo (componente + scss + teste + i18n).

### Prompt para copiar e colar:

```
Crie uma skill em .cursor/skills/create-vue-component/SKILL.md

A skill deve documentar o processo completo de criar um componente Vue
neste projeto. Analise os componentes existentes e extraia o padrao.

A skill deve cobrir:
1. Criacao do arquivo .vue (com script setup + ts)
2. Criacao do arquivo .scss (com BEM)
3. Criacao do arquivo de i18n (se aplicavel)
4. Criacao do arquivo de teste (.spec.ts)
5. Checklist de validacao

Inclua a secao "Trigger" explicando quando usar esta skill.
Inclua exemplos concretos baseados no que ja existe no projeto.
```

### O que observar:

- O agente vai **analisar componentes existentes** antes de criar a skill
- A skill deve refletir os padroes **reais** do projeto
- Deve ser detalhada o suficiente para seguir sem ambiguidade

---

## Exercicio 5.2 — Usar a Skill

Agora abra uma **nova sessao** e use a skill que criou.

### Prompt para copiar e colar:

```
Crie um componente de feedback de usuario (UserFeedback) que:
- Mostra um campo de texto para o usuario escrever
- Tem um botao de enviar
- Mostra estado de loading durante o envio
- Mostra mensagem de sucesso ou erro apos envio
```

### O que observar:

- O agente deve detectar e carregar a skill
- Deve seguir todos os passos na ordem
- Deve criar todos os arquivos listados na skill
- O resultado deve ser consistente com os componentes existentes

### Verifique:

- Arquivo `.vue` criado com a estrutura correta?
- Arquivo `.scss` criado com BEM?
- Arquivo de i18n criado?
- Arquivo de teste criado?
- Segue os padroes dos componentes existentes?

---

## Exercicio 5.3 — Comparar: Com e Sem Skill

### Sem skill (resultado tipico):

O agente cria o `.vue` e talvez o `.scss`. Esquece o i18n. Nao cria testes. Coloca na pasta errada.

### Com skill:

O agente segue o checklist completo. Todos os arquivos sao criados. Tudo no lugar certo. Padroes seguidos.

| Aspecto          | Sem skill                     | Com skill                        |
| ---------------- | ----------------------------- | -------------------------------- |
| Arquivos criados | 1-2                           | 3-4 (todos)                      |
| i18n             | Esquecido                     | Incluido                         |
| Testes           | Esquecido                     | Incluido                         |
| Pasta correta    | Talvez                        | Sim                              |
| Consistencia     | Varia                         | Sempre igual                     |
| Tempo do prompt  | Longo (precisa detalhar tudo) | Curto (skill cuida dos detalhes) |

---

## Exercicio 5.4 — Criar uma Skill de Pre-Commit

Vamos criar outra skill util: um checklist antes de commitar.

### Prompt para copiar e colar:

```
Crie uma skill em .cursor/skills/pre-commit-review/SKILL.md

Esta skill deve ser usada antes de fazer commit. Ela deve:

1. Listar todos os arquivos modificados (git diff --name-only)
2. Para cada arquivo modificado:
   - Verificar se segue os padroes do projeto
   - Verificar se tem problemas de linting
   - Verificar se textos hardcoded deveriam usar i18n
3. Rodar os testes relacionados
4. Gerar um resumo com:
   - O que esta ok
   - O que precisa corrigir
   - Sugestao de mensagem de commit

Trigger: "pre-commit review", "revisar antes de commitar",
"verificar mudancas antes de commit"
```

### Testar a skill:

Depois de criar, faca uma mudanca qualquer no projeto e use:

```
Faca uma revisao pre-commit das mudancas atuais.
```

---

## Exercicio 5.5 — Iterar e Melhorar uma Skill

Skills devem evoluir. Pratique melhorar uma skill existente.

### Prompt para copiar e colar:

```
Leia a skill em @.cursor/skills/create-vue-component/SKILL.md

Com base na minha experiencia usando ela, adicione:
1. Um passo para registrar o componente no barrel export (index.ts)
   se existir
2. Exemplos de como lidar com props complexas (arrays, objetos)
3. Um passo para verificar acessibilidade basica (aria-labels, roles)

Atualize o SKILL.md mantendo a estrutura existente.
```

### O que observar:

- Skills sao documentos vivos — devem ser atualizadas
- Cada iteracao torna a skill mais completa
- O agente le a skill existente e **expande** sem perder o que ja tinha

---

## Quando Criar uma Skill

Use este fluxograma mental:

```
Voce fez essa tarefa antes?
       │
       ├── Nao → Faca manualmente, aprenda o processo
       │
       └── Sim → Quantas vezes?
                    │
                    ├── 1 vez → Provavelmente nao precisa de skill ainda
                    │
                    └── 2+ vezes → Crie uma skill!
                                     │
                                     └── O processo tem mais de 3 passos?
                                           │
                                           ├── Sim → Skill detalhada
                                           └── Nao → Talvez uma regra baste
```

---

## Resumo do que Aprendemos

1. **Skills automatizam fluxos completos** — nao apenas padroes
2. **O agente cria skills melhores** quando analisa codigo existente
3. **Skills reduzem o tamanho dos prompts** — voce nao precisa repetir tudo
4. **Skills garantem consistencia** — toda vez o mesmo resultado
5. **Skills devem evoluir** — atualize conforme aprende

---

> **Proximo:** [06 - Workflow Completo](./06-exercicio-workflow-completo.md) — juntando tudo em um fluxo real
