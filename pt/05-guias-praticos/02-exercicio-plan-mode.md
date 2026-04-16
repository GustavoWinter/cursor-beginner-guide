# Exercicio 2: Plan Mode na Pratica

> **Objetivo:** Aprender a criar planos antes de implementar.
> **Modo:** Plan Mode
> **Tempo estimado:** 15 minutos
> **Pre-requisito:** Ter feito o Exercicio 1 (Ask Mode)

---

## O Cenario

Voce ja pesquisou e entendeu o sistema (Exercicio 1). Agora vai criar um **plano detalhado** antes de escrever qualquer codigo.

---

## Preparacao

1. Mude para **Plan Mode** no seletor de modo
2. Tenha em mente a feature ou mudanca que pesquisou no exercicio anterior

---

## Exercicio 2.1 — Criar um Plano Basico

### Prompt para copiar e colar:

```
Com base no que existe neste projeto, crie um plano para 
adicionar [FEATURE/MUDANCA].

O plano deve incluir:

1. **Resumo** — o que sera feito em 2-3 frases
2. **Arquivos envolvidos** — quais serao criados, quais serao alterados
3. **Passos de implementacao** — na ordem correta, um por um
4. **Testes** — como verificar se cada passo esta correto
5. **Escopo** — o que esta DENTRO e FORA do escopo

Use como referencia os padroes que ja existem no projeto.
```

### O que observar:

- O agente vai ler arquivos e propor mudancas, mas **nao executar**
- O plano deve ser especifico para o **seu** projeto (nao generico)
- Deve listar arquivos com caminhos reais

### Checkpoint:

> Leia o plano inteiro. Pergunte-se: "Se eu desse isso para um dev junior, ele conseguiria implementar?" Se nao, peca mais detalhes.

---

## Exercicio 2.2 — Refinar o Plano

Depois de ler o plano, quase sempre ha algo para melhorar. Pratique iterar.

### Prompts para refinar:

**Se faltam detalhes:**

```
O passo 3 esta vago. Detalhe exatamente:
- Quais funcoes precisam ser criadas
- Quais tipos/interfaces sao necessarios
- Qual o comportamento esperado em caso de erro
```

**Se o escopo esta grande demais:**

```
O plano esta grande demais para uma implementacao so.
Quebre em 2 planos menores:
- Plano A: o minimo viavel (funcionalidade basica)
- Plano B: melhorias e edge cases (segunda iteracao)
```

**Se falta estrategia de teste:**

```
Adicione ao plano uma secao de testes para cada passo:
- Qual teste unitario escrever
- Qual comportamento verificar manualmente
- Quais edge cases testar
```

**Se quer validar a abordagem:**

```
Antes de prosseguir, valide este plano:
- Existe algum risco que nao consideramos?
- Tem alguma dependencia entre os passos que pode dar problema?
- Tem algum passo que pode ser feito em paralelo?
```

### O que observar:

- Cada refinamento torna o plano mais **executavel**
- O tempo gasto aqui economiza tempo na implementacao
- Voce esta treinando o agente a ser mais especifico

---

## Exercicio 2.3 — Comparar: Sem Plano vs. Com Plano

Este exercicio mostra a diferenca entre implementar direto e implementar com plano.

### Parte A — Sem plano (observe o resultado)

Abra uma nova sessao em **Agent Mode** e peca diretamente:

```
Adicione um componente de alerta/notificacao reutilizavel no projeto.
```

Observe:

- O agente vai escolher onde colocar o arquivo
- Vai decidir a API do componente (props, eventos)
- Vai escolher o estilo sozinho
- Pode ou nao criar testes

**Nao aceite as mudancas.** Apenas observe o que o agente decidiu sozinho.

### Parte B — Com plano (compare)

Abra uma nova sessao em **Plan Mode** e peca:

```
Quero criar um componente de alerta/notificacao reutilizavel.

Antes de implementar, crie um plano que defina:
1. Onde o componente vai ficar (pasta e nome do arquivo)
2. Quais props ele vai ter (tipo, severidade, mensagem, etc)
3. Quais eventos vai emitir (fechar, acao, etc)
4. Como vai ser o CSS (seguindo padroes do projeto)
5. Quais variantes existem (sucesso, erro, aviso, info)
6. Quais testes criar
7. Como vai ser usado nos outros componentes
```

### Compare os dois resultados:

- O resultado com plano e mais **previsiivel**?
- O plano te deu **controle** sobre as decisoes?
- Voce se sentiria mais confiante implementando com o plano?

---

## Exercicio 2.4 — Salvar o Plano

Bons planos devem ser salvos para referencia. Pratique:

### Prompt para copiar e colar:

```
Salve este plano como um arquivo Markdown em plans/nome-da-feature.md

Formate de forma clara com:
- Titulo e data
- Resumo
- Passos numerados
- Checklist de validacao
```

> **Nota:** Esse exercicio funciona em Agent Mode, ja que precisa criar um arquivo. E um bom exemplo de quando mudar de modo faz sentido.

---

## O que Aprendemos

1. **Planos reduzem surpresas** — voce sabe exatamente o que vai acontecer
2. **Iterar no plano e barato** — corrigir um plano leva segundos; corrigir codigo leva minutos
3. **Planos dao controle** — voce decide a abordagem, nao o agente
4. **O tempo investido retorna** — implementacao com plano e mais rapida e mais segura

---

## Proximo passo

Com o plano pronto, vamos **implementar**.

> **Proximo:** [03 - Exercicio Agent Mode](./03-exercicio-agent-mode.md)

