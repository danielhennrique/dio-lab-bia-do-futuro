# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | HISTÓRICO DOS ATENDIMENTOS |
| `perfil_investidor.json` | JSON | PERFIL DO INVESTIDOR |
| `produtos_financeiros.json` | JSON |PRODUTOS FINANCEIROS |
| `transacoes.csv` | CSV | TRANSAÇÕES gastos do cliente |

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

[Os JSON/CSV são carregados no início da sessão e incluídos no contexto do prompt]

### Como os dados são usados no prompt?

 [Os dados vão no system prompt, São consultados dinamicamente]

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Dados do Cliente:
- Nome: João Silva
- Perfil: Moderado
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55
...
```
