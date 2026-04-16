# Plan Mode — Planejar Antes de Implementar

> O Plan Mode e o "arquiteto" do Cursor.
> Ele le, analisa, propoe — mas so executa quando voce aprova.

---

## O que e o Plan Mode?

O Plan Mode e um modo **colaborativo de planejamento**. O agente pode:

- Ler arquivos do projeto
- Buscar no codebase
- Propor mudancas detalhadas
- Sugerir planos passo-a-passo

O agente **NAO executa** automaticamente. Ele pede sua aprovacao antes de cada acao.

A diferenca do Ask Mode: aqui o agente vai alem de explicar — ele **desenha a solucao**.

---

## Qual a diferenca entre Ask, Plan e Agent?

| Aspecto          | Ask Mode | Plan Mode     | Agent Mode      |
| ---------------- | -------- | ------------- | --------------- |
| Le arquivos      | Sim      | Sim           | Sim             |
| Explica          | Sim      | Sim           | Sim             |
| Propoe mudancas  | Nao      | Sim           | Sim             |
| Executa mudancas | Nao      | Com aprovacao | Automaticamente |
| Roda comandos    | Nao      | Nao           | Sim             |

**Plan Mode e o meio-termo:** ele pensa e propoe, mas espera voce dizer "vai".

---

## Quando usar o Plan Mode

| Situacao                      | Por que Plan Mode                           |
| ----------------------------- | ------------------------------------------- |
| Feature nova media/grande     | Voce quer ver o plano antes de gerar codigo |
| Refatoracao                   | Precisa entender o impacto antes de alterar |
| Multiplos arquivos envolvidos | Quer saber a ordem das mudancas             |
| Decisao arquitetural          | Precisa comparar abordagens                 |
| Tarefa com risco              | Quer validar a estrategia antes de executar |

---

## Como ativar o Plan Mode

No seletor de modo do chat, selecione **"Plan"**. O agente vai automaticamente adotar o comportamento de planejamento.

---

## Exemplos de Prompts para Plan Mode

### Planejar uma feature

```
Preciso adicionar paginacao na listagem de produtos.

Crie um plano detalhado com:
1. Quais arquivos serao criados ou alterados
2. Qual a ordem de implementacao
3. Como vamos testar cada passo
4. O que nao sera alterado
```

### Planejar uma refatoracao

```
O componente ProductCard esta com 400 linhas e faz muita coisa.

Proponha um plano de refatoracao que:
- Quebre em componentes menores
- Mantenha o comportamento atual
- Seja feito de forma incremental (sem quebrar nada no meio)
```

### Comparar abordagens

```
Preciso implementar cache de API no projeto.
Quais abordagens faria sentido aqui?

Compare:
- Cache no composable
- Cache com Pinia store
- Cache com service worker

Considere o que o projeto ja usa e recomende uma abordagem.
```

### Planejar correcao de bug

```
O filtro de data nao funciona quando o usuario seleciona
o mesmo dia como inicio e fim.

Planeje a correcao:
1. Onde esta o problema (causa raiz)
2. O que precisa mudar
3. Quais testes adicionar para evitar regressao
```

---

## O output de um bom plano

Um plano bem feito pelo Plan Mode deve ter:

### Estrutura esperada

```markdown
## Plano: [nome da tarefa]

### Arquivos envolvidos

- `src/components/ProductList.vue` — adicionar controle de paginacao
- `src/composables/useProducts.ts` — adicionar parametros de pagina
- `src/api/products.ts` — atualizar chamada de API

### Passos

1. Atualizar `useProducts.ts` para aceitar `page` e `pageSize`
2. Modificar a chamada de API em `products.ts`
3. Adicionar componente de paginacao em `ProductList.vue`
4. Adicionar testes para o composable
5. Testar manualmente a navegacao entre paginas

### Verificacao

- [ ] Testes unitarios passando
- [ ] Paginacao funciona com 0, 1 e muitos resultados
- [ ] URL reflete a pagina atual

### Fora do escopo

- Nao alterar o design visual da listagem
- Nao implementar infinite scroll (fase futura)
```

---

## Do Plano para a Implementacao

Depois de aprovar o plano:

1. **Salve o plano** — pode ser num arquivo `plans/nome-da-tarefa.md` ou copie o conteudo
2. **Abra uma nova sessao** em Agent Mode
3. **Forneca o plano** como contexto inicial
4. **Implemente passo a passo** seguindo a ordem do plano

Isso garante:

- Contexto limpo na implementacao
- Passos claros para o agente seguir
- Facilidade de revisao (voce sabe o que esperar)

---

## Boas praticas no Plan Mode

1. **Peca escopo explicito** — sempre peca para definir o que esta dentro e fora do escopo
2. **Peca verificacao** — inclua no plano como saber se cada passo deu certo
3. **Revise criticamente** — o plano e tao bom quanto sua revisao. Leia antes de aprovar
4. **Itere no plano** — se algo nao esta claro, peca para detalhar antes de implementar
5. **Nao pule etapas** — se o plano tem 5 passos, nao peca para fazer tudo de uma vez

---

## Erros comuns no Plan Mode

| Erro                    | Consequencia                           | Solucao                        |
| ----------------------- | -------------------------------------- | ------------------------------ |
| Aceitar o plano sem ler | Agente implementa algo errado          | Sempre leia e valide           |
| Plano vago demais       | Agente faz suposicoes na implementacao | Peca mais detalhes             |
| Plano grande demais     | Dificil de implementar e revisar       | Quebre em planos menores       |
| Nao definir escopo      | Agente faz mais do que deveria         | Sempre defina "fora do escopo" |

---

## Resumo

| Aspecto         | Detalhe                                                 |
| --------------- | ------------------------------------------------------- |
| **Capacidade**  | Le, analisa, propoe (nao executa sozinho)               |
| **Quando usar** | Tarefas medias/grandes, refatoracoes, decisoes          |
| **Objetivo**    | Ter um plano claro antes de escrever codigo             |
| **Resultado**   | Documento de plano passo-a-passo                        |
| **Erro comum**  | Aceitar o plano sem ler ou pular para Agent Mode direto |

---

> **Proximo:** [03 - Agent Mode](./03-agent-mode.md) — executando mudancas com o agente
