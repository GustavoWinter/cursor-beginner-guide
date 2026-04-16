# Exercicio 3: Agent Mode na Pratica

> **Objetivo:** Implementar mudancas seguindo um plano, com revisao cuidadosa.
> **Modo:** Agent Mode
> **Tempo estimado:** 20 minutos
> **Pre-requisito:** Ter feito os Exercicios 1 e 2

---

## O Cenario

Voce pesquisou (Ask Mode), planejou (Plan Mode), e agora vai implementar (Agent Mode). Este e o momento onde codigo e realmente escrito.

---

## Preparacao

1. Mude para **Agent Mode**
2. Abra uma **nova sessao** (contexto limpo!)
3. Tenha o plano do Exercicio 2 em maos

---

## Exercicio 3.1 — Implementar Passo a Passo

A chave do Agent Mode e **nao pedir tudo de uma vez**.

### Prompt para copiar e colar:

```
Vou implementar uma mudanca seguindo um plano.
Implemente UM passo de cada vez e me mostre o que mudou
antes de prosseguir para o proximo.

Plano:
1. [Cole o primeiro passo do seu plano]
2. [Cole o segundo passo]
3. [Cole o terceiro passo]

Comece pelo passo 1.
```

### O que observar:

- O agente deve implementar **apenas o passo 1** e parar
- Ele vai mostrar o diff (o que mudou)
- Voce revisa antes de autorizar o proximo passo

### Como revisar:

- O codigo faz o que o passo pedia?
- Segue os padroes do projeto?
- Nao alterou nada alem do esperado?

Se tudo estiver ok, responda:

```
Ok, prossiga para o passo 2.
```

Se algo esta errado:

```
O passo 1 nao esta correto. O problema e: [descreva].
Corrija antes de prosseguir.
```

---

## Exercicio 3.2 — Usar @ para Contexto Preciso

Pratique referenciar arquivos para dar contexto exato ao agente.

### Prompt para copiar e colar:

```
Olhe o componente @src/components/[ComponenteExistente].vue
e crie um novo componente similar chamado [NovoNome].

As diferencas devem ser:
- [diferenca 1]
- [diferenca 2]

Mantenha o mesmo padrao de props, estilos e estrutura.
```

### O que observar:

- Ao usar `@`, o agente le o arquivo exato como referencia
- O resultado deve ser consistente com o original
- Compare: o novo componente segue o mesmo padrao?

---

## Exercicio 3.3 — Commit Incremental com Git

Pratique a revisao e commit passo a passo.

### Fluxo:

**Apos o agente fazer uma mudanca:**

1. Revise o diff no Cursor (ele mostra automaticamente)
2. Se aprovado, peca o commit:

```
Faca um commit desta mudanca com uma mensagem descritiva.
Use o formato: tipo(escopo): descricao

Exemplos:
- feat(products): adiciona campo de filtro
- fix(auth): corrige validacao de token expirado
```

1. Verifique o resultado:

```
Rode git log --oneline -5 para ver os ultimos commits.
```

### O que observar:

- Cada commit deve ser **pequeno e focado**
- A mensagem deve descrever o **que** e o **por que**
- Se algo der errado, voce pode reverter um commit especifico

---

## Exercicio 3.4 — Corrigir Quando o Agente Erra

Erros vao acontecer. Pratique lidar com eles.

### Cenario simulado:

Peca ao agente algo propositalmente vago e veja o que acontece:

```
Melhore o formulario de cadastro.
```

O agente provavelmente vai:

- Fazer mudancas que voce nao queria
- Assumir coisas que nao estao certas
- Alterar mais arquivos do que necessario

### Como corrigir:

**Opcao 1 — Pedir para reverter:**

```
Reverta todas as mudancas que voce fez.
Vamos recomecar com instrucoes mais especificas.
```

**Opcao 2 — Aceitar parcialmente:**

```
A mudanca no arquivo X esta boa, mas as mudancas nos arquivos
Y e Z nao sao o que eu queria. Reverta apenas Y e Z.
```

**Opcao 3 — Usar Git para reverter:**

```
git checkout -- src/components/FormularioCadastro.vue
```

### Licao:

> Prompts vagos geram resultados imprevisíveis. Quanto mais especifico voce for, melhor o resultado.

---

## Exercicio 3.5 — Nova Sessao para Nova Tarefa

Pratique o habito de separar tarefas em sessoes.

### Cenario:

Voce terminou de implementar a feature do plano. Agora precisa corrigir um bug nao relacionado.

**ERRADO** — continuar na mesma sessao:

```
Agora corrija o bug no componente de login onde...
```

**CORRETO** — nova sessao:

1. Feche a sessao atual (ou abra uma nova)
2. Na nova sessao, comece limpo:

```
Preciso corrigir um bug no componente de login.
O problema e: [descreva o bug]
O arquivo relevante e: @src/components/Login.vue
```

### Por que isso importa:

- Contexto limpo = melhor qualidade
- O agente nao vai confundir a feature anterior com o bug
- Mais facil de rastrear o que foi feito em cada sessao

---

## Checklist de Revisao — Use em Toda Implementacao

Copie este checklist e use sempre que o agente fizer mudancas:

```
## Revisao de Implementacao

### Codigo
- [ ] Faz o que foi pedido?
- [ ] Segue os padroes do projeto?
- [ ] Nomes de variaveis e funcoes sao claros?
- [ ] Nao tem logica duplicada?
- [ ] Nao introduziu dependencias desnecessarias?

### Escopo
- [ ] So alterou os arquivos esperados?
- [ ] Nao fez mudancas fora do escopo?
- [ ] Nao removeu nada que nao deveria?

### Qualidade
- [ ] Testes passam?
- [ ] Linting esta ok?
- [ ] Build funciona?

### Git
- [ ] Commit com mensagem descritiva?
- [ ] Diff revisado antes do commit?
```

---

## O que Aprendemos

1. **Passo a passo e mais seguro** do que "faca tudo de uma vez"
2. **@ da contexto preciso** — use para referenciar arquivos
3. **Commits pequenos** permitem reverter sem perder tudo
4. **Prompts vagos geram resultados vagos** — seja especifico
5. **Nova tarefa = nova sessao** — nunca misture assuntos

---

## Proximo passo

Agora vamos ver como **regras** mudam a qualidade do output.

> **Proximo:** [04 - Exercicio Regras](./04-exercicio-regras.md)
