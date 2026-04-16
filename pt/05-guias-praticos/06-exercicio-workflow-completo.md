# Exercicio 6: Workflow Completo — Do Zero ao Commit

> **Objetivo:** Juntar tudo que aprendeu em um fluxo real, do entendimento ao codigo pronto.
> **Modos:** Ask → Plan → Agent
> **Tempo estimado:** 30-40 minutos

---

## O Cenario

Voce recebeu uma tarefa real: adicionar uma funcionalidade no projeto. Vamos percorrer o fluxo completo usando todos os conceitos e modos.

Escolha uma feature simples do seu projeto para este exercicio. Sugestoes:

- Adicionar um campo em um formulario existente
- Criar um componente de empty state (quando nao ha dados)
- Adicionar um botao de copiar para clipboard
- Criar um tooltip reutilizavel

---

## Fase 1: Pesquisar (Ask Mode)

**Tempo:** ~5 minutos

### Mude para Ask Mode e use este prompt:

```
Eu preciso implementar [DESCREVA A FEATURE].

Me ajude a entender:

1. Quais componentes/arquivos existentes sao relevantes?
2. Existe algo similar ja implementado no projeto?
3. Quais padroes eu deveria seguir?
4. Quais arquivos precisarei criar ou alterar?
5. Tem algum edge case ou cuidado especial?

Nao implemente nada — apenas pesquise.
```

### Checklist antes de prosseguir:

- [ ] Entendi como o sistema funciona hoje
- [ ] Sei quais arquivos serao envolvidos
- [ ] Conheco os padroes a seguir
- [ ] Identifiquei possiveis riscos

> Se algum item nao esta marcado, faca mais perguntas no Ask Mode antes de prosseguir.

---

## Fase 2: Planejar (Plan Mode)

**Tempo:** ~10 minutos

### Mude para Plan Mode e use este prompt:

```
Com base na pesquisa que fizemos, crie um plano de implementacao
para [FEATURE].

Estruture assim:

## Resumo
O que sera feito em 2-3 frases.

## Arquivos
- Criar: [lista]
- Alterar: [lista]

## Passos (na ordem)
1. [passo]
2. [passo]
...

## Testes
- Como verificar cada passo
- Quais testes unitarios adicionar

## Fora do escopo
- O que NAO vamos alterar
```

### Refine o plano:

Leia o plano inteiro e peca ajustes:

```
[Se faltou detalhe]
Detalhe melhor o passo X. Quero saber exatamente quais funcoes
criar e quais tipos usar.

[Se esta grande demais]
Esse plano esta grande. Quebre em Fase 1 (MVP) e Fase 2 (melhorias).

[Se falta teste]
Adicione testes especificos para cada passo.
```

### Checklist antes de prosseguir:

- [ ] Plano esta claro e especifico
- [ ] Sei exatamente quais arquivos serao criados/alterados
- [ ] Cada passo esta detalhado
- [ ] Escopo esta definido (dentro e fora)
- [ ] Estrategia de teste esta definida

---

## Fase 3: Implementar (Agent Mode)

**Tempo:** ~15-20 minutos

### Abra uma NOVA SESSAO em Agent Mode

Isso e crucial — contexto limpo para a implementacao.

### Prompt inicial:

```
Vou implementar uma feature seguindo o plano abaixo.
Implemente UM passo de cada vez.
Apos cada passo, me mostre o que mudou e espere minha aprovacao.

[Cole o plano completo aqui]

Comece pelo passo 1.
```

### Para cada passo:

**Se o resultado esta bom:**

```
Aprovado. Prossiga para o passo 2.
```

**Se precisa de ajuste:**

```
Quase. Ajuste [problema especifico] antes de prosseguir.
```

**Se esta errado:**

```
Isso nao esta certo. O problema e [descreva].
Reverta e tente novamente considerando [instrucao].
```

---

## Fase 4: Commit e Revisao

### Apos implementar todos os passos:

```
Rode os testes para verificar se tudo esta funcionando.
```

Se passaram:

```
Faca um commit com mensagem descritiva no formato:
feat(escopo): descricao curta do que foi adicionado
```

Se falharam:

```
Os testes falharam. Analise o erro e corrija.
Nao prossiga ate todos os testes passarem.
```

### Revisao final:

```
Me mostre um resumo de todas as mudancas feitas:
- Arquivos criados
- Arquivos alterados
- Testes adicionados
- Qualquer pendencia restante
```

---

## Retrospectiva — Reflexao Pos-Exercicio

Depois de completar o fluxo, reflita:

### Tempo

| Fase                  | Tempo gasto | Valeu a pena? |
| --------------------- | ----------- | ------------- |
| Pesquisa (Ask)        | \_\_ min    |               |
| Planejamento (Plan)   | \_\_ min    |               |
| Implementacao (Agent) | \_\_ min    |               |
| Revisao e commit      | \_\_ min    |               |
| **Total**             | \_\_ min    |               |

### Qualidade

- O resultado final seguiu os padroes do projeto?
- Houve surpresas na implementacao?
- Os testes cobrem os casos importantes?
- Voce confiaria em mandar esse PR para code review?

### O que voce faria diferente?

- A pesquisa foi suficiente?
- O plano foi detalhado o bastante?
- Deveria ter pedido passos menores na implementacao?
- Alguma regra ou skill ajudaria a automatizar parte do processo?

---

## Template de Workflow — Copie e Reuse

Use este template para suas proximas tarefas:

```markdown
# Tarefa: [nome]

## Fase 1 — Pesquisa (Ask Mode)

- [ ] Entender o sistema atual
- [ ] Identificar arquivos relevantes
- [ ] Identificar padroes a seguir
- [ ] Identificar riscos e edge cases

## Fase 2 — Planejamento (Plan Mode)

- [ ] Definir arquivos a criar/alterar
- [ ] Definir passos na ordem correta
- [ ] Definir testes
- [ ] Definir escopo (dentro/fora)
- [ ] Revisar e aprovar plano

## Fase 3 — Implementacao (Agent Mode)

- [ ] Nova sessao com contexto limpo
- [ ] Implementar passo a passo
- [ ] Revisar cada mudanca
- [ ] Rodar testes a cada passo critico

## Fase 4 — Finalizacao

- [ ] Todos os testes passando
- [ ] Linting ok
- [ ] Commits com mensagens descritivas
- [ ] Pronto para PR
```

---

## Parabens!

Voce completou todos os exercicios. Agora voce sabe:

- **Pesquisar** com Ask Mode antes de agir
- **Planejar** com Plan Mode antes de implementar
- **Implementar** com Agent Mode de forma controlada
- **Usar regras** para garantir consistencia automatica
- **Criar skills** para automatizar tarefas repetitivas
- **Gerenciar contexto** para manter a qualidade das respostas

### Proximo nivel

- Explore as regras existentes do projeto em `.cursor/rules/`
- Leia as skills em `.cursor/skills/`
- Crie suas proprias regras e skills para o seu workflow
- Experimente e itere — e assim que se aprende

> _"Escolha uma ferramenta, pratique muito. E parte arte e parte ciencia — voce precisa de muita repeticao para desenvolver a intuicao do que confiar ao modelo e do que manter para voce."_
