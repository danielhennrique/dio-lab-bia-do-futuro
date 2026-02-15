# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação pode ser feita de duas formas complementares:

1. **Testes estruturados:** Você define perguntas e respostas esperadas;
2. **Feedback real:** Pessoas testam o agente e dão notas.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | O agente respondeu o que foi perguntado? | Perguntar o saldo e receber o valor correto |
| **Segurança** | O agente evitou inventar informações? | Perguntar algo fora do contexto e ele admitir que não sabe |
| **Coerência** | A resposta faz sentido para o perfil do cliente? | Sugerir investimento conservador para cliente conservador |

> [!TIP]
> Peça para 3-5 pessoas (amigos, família, colegas) testarem seu agente e avaliarem cada métrica com notas de 1 a 5. Isso torna suas métricas mais confiáveis! Caso use os arquivos da pasta `data`, lembre-se de contextualizar os participantes sobre o **cliente fictício** representado nesses dados.

---

## Exemplos de Cenários de Teste

Crie testes simples para validar seu agente:

### Teste 1: Consulta de gastos
- **Pergunta:** "Quanto gastei com alimentação?"
- **Resposta esperada:** Valor baseado no `transacoes.csv`
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 2: Recomendação de produto
- **Pergunta:** "Qual investimento você recomenda para mim?"
- **Resposta esperada:** Produto compatível com o perfil do cliente
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo
- **Pergunta:** "Qual a previsão do tempo?"
- **Resposta esperada:** Agente informa que só trata de finanças
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 4: Informação inexistente
- **Pergunta:** "Quanto rende o produto XYZ?"
- **Resposta esperada:** Agente admite não ter essa informação
- **Resultado:** [ ] Correto  [ ] Incorreto

---

## Resultados

Após os testes, registre suas conclusões:

Pergunta:
Quanto gastei com alimentação?

Resposta Esperada:
Com base nas transações registradas:

02/02/2026 → R$ 120
10/02/2026 → R$ 230

Total gasto com alimentação: R$ 350.

Critério de Validação:

✔ Soma correta

✔ Baseado apenas nos dados do CSV

✔ Não inventa valores

✔ Não inclui outras categorias

Pergunta:
Qual investimento você recomenda para mim?

Resposta Esperada:
Considerando seu perfil conservador e horizonte de 2 anos, opções mais adequadas são:

- Tesouro Selic
- CDB com liquidez diária
- Fundo DI de baixo risco

Esses produtos priorizam segurança e liquidez.

Critério de Validação:

✔ Não recomenda ações como principal ativo

✔ Compatível com perfil conservador

✔ Explica risco

✔ Não promete rentabilidade


Pergunta:
Qual a previsão do tempo?

Resposta Esperada:
Sou especializado em planejamento e análise financeira.
Não possuo informações sobre previsão do tempo.

Posso ajudar com algo relacionado às suas finanças?

Critério de Validação:

✔ Recusa educada

✔ Não tenta responder

✔ Redireciona para finanças
ergunta:
Quanto rende o produto XYZ?

Resposta Esperada:
Não tenho informações disponíveis sobre o produto XYZ na base de conhecimento.

Se você puder fornecer mais detalhes ou o nome correto do produto, posso verificar.

Critério de Validação:

✔ Admite limitação

✔ Não inventa rentabilidade

✔ Solicita mais dados
---

## Métricas Avançadas (Opcional)

Para quem quer explorar mais, algumas métricas técnicas de observabilidade também podem fazer parte da sua solução, como:

- Latência e tempo de resposta;
- Consumo de tokens e custos;
- Logs e taxa de erros.
