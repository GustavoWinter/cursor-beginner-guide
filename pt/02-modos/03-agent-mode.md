# Agent Mode — Implementar e Executar

> O modo mais poderoso do Cursor.
> Aqui o agente pode ler, escrever, criar arquivos e rodar comandos.
> Com grande poder vem grande responsabilidade.

---

## O que e o Agent Mode?

O Agent Mode e o modo de **execucao completa**. O agente pode:

- Ler e buscar arquivos
- Criar novos arquivos
- Editar arquivos existentes
- Executar comandos no terminal
- Instalar dependencias
- Rodar testes
- Fazer commits (se voce permitir)

Este e o modo onde codigo e realmente escrito e mudancas acontecem.

---

## Quando usar o Agent Mode

| Situacao                           | Exemplo                                                     |
| ---------------------------------- | ----------------------------------------------------------- |
| **Implementar um plano**           | Voce ja pesquisou e planejou, agora e hora de executar      |
| **Tarefas simples e diretas**      | Renomear uma variavel, corrigir um typo, adicionar um campo |
| **Executar com instrucoes claras** | Voce sabe exatamente o que quer e consegue descrever        |
| **Gerar codigo boilerplate**       | Criar um componente seguindo um padrao existente            |

---

## Quando NAO usar o Agent Mode (direto)

| Situacao                                    | Modo recomendado   |
| ------------------------------------------- | ------------------ |
| Voce nao entende o problema                 | Ask Mode primeiro  |
| A tarefa e complexa e ambigua               | Plan Mode primeiro |
| Voce quer explorar opcoes                   | Ask ou Plan Mode   |
| Voce nao sabe quais arquivos serao afetados | Ask Mode primeiro  |

**Regra de ouro:** Se voce nao consegue explicar para um colega o que precisa ser feito, voce nao esta pronto para o Agent Mode.

---

## Como funciona na pratica

### 1. O agente age por conta propria

Diferente do Plan Mode, aqui o agente **executa** sem pedir permissao a cada passo. Ele vai:

1. Analisar o que voce pediu
2. Decidir quais arquivos ler
3. Fazer as mudancas
4. Rodar comandos se necessario
5. Te mostrar o resultado

### 2. Voce revisa depois

O Cursor mostra um **diff** (comparacao antes/depois) de cada arquivo alterado. Voce pode:

- **Aceitar** a mudanca
- **Rejeitar** a mudanca
- **Pedir ajustes** com um novo prompt

---

## Exemplos de Prompts para Agent Mode

### Tarefa simples e direta

```
Adicione um campo "telefone" no formulario de cadastro.
Siga o mesmo padrao dos campos existentes.
O campo deve ser obrigatorio e aceitar apenas numeros.
```

### Implementar a partir de um plano

```
Implemente o plano descrito em @plans/paginacao.md

Siga os passos na ordem. Depois de cada passo, me mostre
o que mudou antes de continuar.
```

### Corrigir um bug especifico

```
O botao de "Salvar" no componente @src/components/UserForm.vue
nao esta desabilitando durante o envio do formulario.

Corrija isso adicionando um estado de loading que:
- Desabilita o botao durante o submit
- Mostra um texto "Salvando..." no botao
- Reabilita o botao apos a resposta (sucesso ou erro)
```

### Gerar codigo seguindo padrao existente

```
Crie um novo composable useCategories seguindo o mesmo padrao
de @src/composables/useProducts.ts

Deve buscar categorias da API /api/categories e retornar:
- categories (lista)
- isLoading
- error
- fetchCategories()
```

---

## Revisando o trabalho do agente

Depois que o agente faz mudancas, trate como um **code review de um junior**:

### Checklist de revisao

- O codigo faz o que foi pedido?
- Segue os padroes do projeto?
- Nao tem efeitos colaterais inesperados?
- Os nomes de variaveis e funcoes fazem sentido?
- Nao introduziu dependencias desnecessarias?
- Os testes passam?

### Use o Git como aliado

```
# Veja o que mudou antes de commitar
git diff

# Se algo esta errado, reverta
git checkout -- arquivo-com-problema.ts

# Commite passo a passo, nao tudo de uma vez
git add arquivo-correto.ts
git commit -m "feat: adiciona campo telefone no cadastro"
```

Commits frequentes permitem reverter mudancas especificas sem perder tudo.

---

## Controle de autonomia

Voce pode configurar o que o agente pode fazer automaticamente no Cursor:

| Acao              | Recomendacao para iniciantes  |
| ----------------- | ----------------------------- |
| Ler arquivos      | Permitir                      |
| Escrever arquivos | Permitir (voce revisa depois) |
| Rodar comandos    | Revisar caso a caso           |
| Instalar pacotes  | Aprovar manualmente           |
| Fazer commits     | Aprovar manualmente           |

Comece conservador e va liberando conforme ganha confianca.

---

## Boas praticas no Agent Mode

1. **De instrucoes claras** — quanto mais especifico, melhor o resultado
2. **Referencie arquivos** — use `@` para apontar exatamente onde o agente deve trabalhar
3. **Peca passo a passo** — _"faca um passo de cada vez e me mostre antes de continuar"_
4. **Revise tudo** — nunca aceite mudancas sem ler o diff
5. **Commite frequentemente** — commits pequenos sao mais faceis de reverter
6. **Comece nova sessao para nova tarefa** — nao reutilize sessoes longas

---

## Erros comuns no Agent Mode

| Erro                     | O que acontece                            | Como evitar               |
| ------------------------ | ----------------------------------------- | ------------------------- |
| Prompt vago              | Agente assume e gera codigo que nao serve | Seja especifico           |
| Nao revisar o diff       | Bugs vao para producao                    | Sempre leia o diff        |
| Sessao muito longa       | Qualidade degrada                         | Nova sessao a cada tarefa |
| Aceitar tudo de uma vez  | Dificil reverter se algo esta errado      | Commite por partes        |
| Nao referenciar arquivos | Agente pode alterar arquivos errados      | Use `@` sempre            |

---

## Agent Mode + Git = Workflow Seguro

```
1. Agent faz mudancas
         ↓
2. Voce revisa o diff (git diff)
         ↓
3. Aceita? → git add + commit com mensagem clara
   Rejeita? → git checkout -- arquivo.ts
         ↓
4. Proximo passo do plano
         ↓
5. Repete ate concluir
```

Pense no Git como seu **primeiro code review** antes do PR ir para o time.

---

## Resumo

| Aspecto         | Detalhe                                    |
| --------------- | ------------------------------------------ |
| **Capacidade**  | Leitura, escrita, execucao — tudo          |
| **Quando usar** | Tarefas claras, apos pesquisa/planejamento |
| **Objetivo**    | Implementar mudancas no codigo             |
| **Resultado**   | Codigo pronto para commit e review         |
| **Erro comum**  | Usar sem pesquisar/planejar antes          |

---

> **Proximo:** [03 - Regras](../03-regras/01-o-que-sao-regras.md) — ensinando o agente a seguir os padroes do seu projeto
