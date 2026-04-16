# O Modelo Mental Correto

> Antes de abrir o Cursor, voce precisa ajustar como **pensa** sobre IA.
> Esse ajuste mental e a diferenca entre frustacao e produtividade.

---

## Usar IA vs. Trabalhar com IA

A maioria dos desenvolvedores diz que "usa IA para codar mais rapido". Mas se voce perguntar *como* exatamente, poucos conseguem explicar o fluxo real: o que delegam, o que mantem para si, como decidem entre os dois.

Essa diferenca importa. Existe um abismo entre:

- **Usar IA** — aceitar sugestoes de autocomplete e esperar que funcione
- **Trabalhar com IA** — direcionar o trabalho, revisar criticamente, e decidir o que o agente pode ou nao fazer

Trabalhar com IA e um papel ativo. Voce e o lider tecnico; o agente e o executor.

---

## O Agente como Junior Dev

O modelo mental mais util para trabalhar com o Cursor:

> **Pense no agente como um junior developer entusiasmado, extremamente bem-lido, e frequentemente errado com confianca.**

### O que o agente faz bem


| Ponto forte            | Exemplo                                         |
| ---------------------- | ----------------------------------------------- |
| **Velocidade**         | Gera centenas de linhas em segundos             |
| **Sem ego**            | Reescreve o mesmo codigo 6 vezes sem reclamar   |
| **Conhecimento amplo** | Conhece muitas linguagens, frameworks e padroes |
| **Incansavel**         | Nao cansa, nao distrai, nao precisa de cafe     |


### O que o agente NAO faz bem


| Ponto fraco                | Exemplo                                                        |
| -------------------------- | -------------------------------------------------------------- |
| **Sem julgamento**         | Nao sabe se aquele endpoint e critico para o negocio           |
| **Sem contexto historico** | Nao sabe por que voce escolheu essa arquitetura 3 meses atras  |
| **Confianca excessiva**    | Escreve codigo tecnicamente correto mas contextualmente errado |
| **Sem visao de sistema**   | Pode quebrar uma integracao que ele nem sabe que existe        |


### Na pratica

Imagine que voce pede ao agente: *"Crie um endpoint de pagamento"*.

O agente vai gerar um endpoint funcional. Mas ele nao sabe que:

- O seu sistema usa um gateway de pagamento especifico
- Existe uma fila de processamento assincrono
- O time de seguranca exige um padrao especifico de logs
- Existe uma regra de negocio sobre parcelamento que nao esta documentada

O codigo vai compilar. Os testes vao passar. Mas nao vai servir para producao.

**Esse e o gap que voce precisa preencher.**

---

## Seu Papel: Diretor do Trabalho

Se o agente e o junior dev, voce e o **tech lead**. Seu trabalho nao e escrever cada linha de codigo — e garantir que o resultado final esta correto.

Isso significa:

1. **Definir o que precisa ser feito** — com clareza suficiente para o agente executar
2. **Fornecer contexto** — o agente so sabe o que voce conta para ele
3. **Revisar o resultado** — nunca aceite codigo sem ler
4. **Corrigir a rota** — quando o agente erra, redirecione com instrucoes claras

### Analogia pratica


| Situacao                             | Sem modelo mental | Com modelo mental                               |
| ------------------------------------ | ----------------- | ----------------------------------------------- |
| Agente gera codigo errado            | "IA nao funciona" | "Eu nao dei contexto suficiente"                |
| Agente ignora padrao do projeto      | "IA e burra"      | "Eu preciso criar uma regra para isso"          |
| Resultado ficou bom de primeira      | "IA e magica"     | "O prompt estava bem especifico"                |
| Resultado degrade ao longo da sessao | "IA cansou?"      | "O contexto ficou poluido, hora de nova sessao" |


---

## Resumo

- O agente e uma ferramenta poderosa, mas **sem julgamento**
- Voce precisa ser o **diretor do trabalho**, nao apenas um consumidor de sugestoes
- A qualidade do output depende diretamente da qualidade do **input que voce fornece**
- Quando o resultado e ruim, a primeira pergunta deve ser: *"O que eu poderia ter feito diferente?"*

---

> **Proximo:** [02 - O que e Contexto](./02-contexto.md) — o conceito mais importante para trabalhar com IA

