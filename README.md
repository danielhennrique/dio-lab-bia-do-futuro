# 🤖 Agente Financeiro Inteligente com IA Generativa

## Contexto

Os assistentes virtuais no setor financeiro estão evoluindo de simples chatbots reativos para **agentes inteligentes e proativos**. Neste desafio, você vai idealizar e prototipar um agente financeiro que utiliza IA Generativa para:

- **Antecipar necessidades** ao invés de apenas responder perguntas
- **Personalizar** sugestões com base no contexto de cada cliente
- **Cocriar soluções** financeiras de forma consultiva
- **Garantir segurança** e confiabilidade nas respostas (anti-alucinação)

> [!TIP]
> Na pasta [`examples/`](./examples/) você encontra referências de implementação para cada etapa deste desafio.

---

## O Que Você Deve Entregar

### 1. Documentação do Agente

Defina **o que** seu agente faz e **como** ele funciona:

- **Caso de Uso:** Qual problema financeiro ele resolve? (ex: consultoria de investimentos, planejamento de metas, alertas de gastos)
- **Persona e Tom de Voz:** Como o agente se comporta e se comunica?
- **Arquitetura:** Fluxo de dados e integração com a base de conhecimento
- **Segurança:** Como evitar alucinações e garantir respostas confiáveis?

📄 **Template:** [`docs/01-documentacao-agente.md`](./docs/01-documentacao-agente.md)

---

### 2. Base de Conhecimento

Utilize os **dados mockados** disponíveis na pasta [`data/`](./data/) para alimentar seu agente:

| Arquivo | Formato | Descrição |
|---------|---------|-----------|
| `transacoes.csv` | CSV | Histórico de transações do cliente |
| `historico_atendimento.csv` | CSV | Histórico de atendimentos anteriores |
| `perfil_investidor.json` | JSON | Perfil e preferências do cliente |
| `produtos_financeiros.json` | JSON | Produtos e serviços disponíveis |

Você pode adaptar ou expandir esses dados conforme seu caso de uso.

📄 **Template:** [`docs/02-base-conhecimento.md`](./docs/02-base-conhecimento.md)

---

### 3. Prompts do Agente

Documente os prompts que definem o comportamento do seu agente:

- **System Prompt:** Instruções gerais de comportamento e restrições
- **Exemplos de Interação:** Cenários de uso com entrada e saída esperada
- **Tratamento de Edge Cases:** Como o agente lida com situações limite

📄 **Template:** [`docs/03-prompts.md`](./docs/03-prompts.md)

---

### 4. Aplicação Funcional

Desenvolva um **protótipo funcional** do seu agente:

- Chatbot interativo (sugestão: Streamlit, Gradio ou similar)
- Integração com LLM (via API ou modelo local)
- Conexão com a base de conhecimento

📁 **Pasta:** [`src/`](./src/)

---

### 5. Avaliação e Métricas

Descreva como você avalia a qualidade do seu agente:

**Métricas Sugeridas:**
- Precisão/assertividade das respostas
- Taxa de respostas seguras (sem alucinações)
- Coerência com o perfil do cliente

📄 **Template:** [`docs/04-metricas.md`](./docs/04-metricas.md)

---

### 6. Pitch

Grave um **pitch de 3 minutos** (estilo elevador) apresentando:

- Qual problema seu agente resolve?
- Como ele funciona na prática?
- Por que essa solução é inovadora?

📄 **Template:** [`docs/05-pitch.md`](./docs/05-pitch.md)

---

## Ferramentas Sugeridas

Todas as ferramentas abaixo possuem versões gratuitas:

| Categoria | Ferramentas |
|-----------|-------------|
| **LLMs** | [ChatGPT](https://chat.openai.com/), [Copilot](https://copilot.microsoft.com/), [Gemini](https://gemini.google.com/), [Claude](https://claude.ai/), [Ollama](https://ollama.ai/) |
| **Desenvolvimento** | [Streamlit](https://streamlit.io/), [Gradio](https://www.gradio.app/), [Google Colab](https://colab.research.google.com/) |
| **Orquestração** | [LangChain](https://www.langchain.com/), [LangFlow](https://www.langflow.org/), [CrewAI](https://www.crewai.com/) |
| **Diagramas** | [Mermaid](https://mermaid.js.org/), [Draw.io](https://app.diagrams.net/), [Excalidraw](https://excalidraw.com/) |

---

## Estrutura do Repositório

```
📁 lab-agente-financeiro/
│
├── 📄 README.md
│
├── 📁 data/                          # Dados mockados para o agente
│   ├── historico_atendimento.csv     # Histórico de atendimentos (CSV)
│   ├── perfil_investidor.json        # Perfil do cliente (JSON)
│   ├── produtos_financeiros.json     # Produtos disponíveis (JSON)
│   └── transacoes.csv                # Histórico de transações (CSV)
│
├── 📁 docs/                          # Documentação do projeto
│   ├── 01-documentacao-agente.md     # Caso de uso e arquitetura
│   ├── 02-base-conhecimento.md       # Estratégia de dados
│   ├── 03-prompts.md                 # Engenharia de prompts
│   ├── 04-metricas.md                # Avaliação e métricas
│   └── 05-pitch.md                   # Roteiro do pitch
│
├── 📁 src/                           # Código da aplicação
│   └── app.py                        # (exemplo de estrutura)
│
├── 📁 assets/                        # Imagens e diagramas
│   └── ...
│
└── 📁 examples/                      # Referências e exemplos
    └── README.md
```
código python

import csv
import os

class AgenteFinanceiro:

    def __init__(self, arquivo_transacoes="transacoes.csv"):
        self.arquivo = arquivo_transacoes
        self.transacoes = self.carregar_transacoes()

    # ==========================
    # CARREGAR TRANSAÇÕES
    # ==========================
    def carregar_transacoes(self):
        if not os.path.exists(self.arquivo):
            print("Arquivo de transações não encontrado.")
            return []

        transacoes = []
        with open(self.arquivo, mode='r', encoding='utf-8') as file:
            reader = csv.DictReader(file)
            for row in reader:
                transacoes.append({
                    "data": row["data"],
                    "categoria": row["categoria"],
                    "valor": float(row["valor"])
                })
        return transacoes

    # ==========================
    # CONSULTA DE GASTOS
    # ==========================
    def consultar_gastos(self, categoria):
        total = 0
        detalhes = []

        for t in self.transacoes:
            if t["categoria"].lower() == categoria.lower():
                total += t["valor"]
                detalhes.append(t)

        if total == 0:
            return f"Não encontrei gastos na categoria '{categoria}'."

        resposta = "📌 Gastos encontrados:\n"
        for d in detalhes:
            resposta += f"{d['data']} → R$ {d['valor']:.2f}\n"

        resposta += f"\nTotal gasto em {categoria}: R$ {total:.2f}"
        return resposta

    # ==========================
    # RECOMENDAÇÃO DE INVESTIMENTO
    # ==========================
    def recomendar_investimento(self, perfil):
        perfil = perfil.lower()

        if perfil == "conservador":
            return (
                "Para perfil conservador:\n"
                "- Tesouro Selic\n"
                "- CDB com liquidez diária\n"
                "- Fundos DI\n\n"
                "Esses priorizam segurança e liquidez."
            )

        elif perfil == "moderado":
            return (
                "Para perfil moderado:\n"
                "- 50% Renda Fixa\n"
                "- 30% Fundos Multimercado\n"
                "- 20% Renda Variável\n\n"
                "Equilíbrio entre risco e retorno."
            )

        elif perfil == "arrojado":
            return (
                "Para perfil arrojado:\n"
                "- Maior exposição em ações\n"
                "- Fundos de ações\n"
                "- ETFs\n\n"
                "Maior potencial de retorno com maior risco."
            )

        else:
            return (
                "Não reconheci o perfil informado.\n"
                "Informe: conservador, moderado ou arrojado."
            )

    # ==========================
    # TRATAMENTO PRINCIPAL
    # ==========================
    def responder(self, pergunta):
        pergunta = pergunta.lower()

        # Consulta de gastos
        if "gastei" in pergunta and "aliment" in pergunta:
            return self.consultar_gastos("Alimentacao")

        # Recomendação de investimento
        elif "invest" in pergunta:
            return (
                "Para recomendar adequadamente, preciso saber seu perfil:\n"
                "Você é conservador, moderado ou arrojado?"
            )

        # Pergunta fora do escopo
        elif "tempo" in pergunta:
            return (
                "Sou especializado em finanças.\n"
                "Não possuo informações sobre previsão do tempo."
            )

        # Produto inexistente
        elif "xyz" in pergunta:
            return (
                "Não tenho informações disponíveis sobre o produto XYZ.\n"
                "Pode fornecer mais detalhes?"
            )

        else:
            return (
                "Não consegui identificar sua solicitação.\n"
                "Posso ajudar com:\n"
                "- Consulta de gastos\n"
                "- Recomendação de investimento\n"
                "- Planejamento financeiro"
            )


# ==========================
# EXECUÇÃO
# ==========================
if __name__ == "__main__":
    agente = AgenteFinanceiro()

    print("💬 Agente Financeiro iniciado.")
    print("Digite 'sair' para encerrar.\n")

    while True:
        pergunta = input("Você: ")

        if pergunta.lower() == "sair":
            print("Encerrando agente.")
            break

        resposta = agente.responder(pergunta)
        print("\nAgente:")
        print(resposta)
        print()

---

## Dicas Finais

1. **Comece pelo prompt:** Um bom system prompt é a base de um agente eficaz
2. **Use os dados mockados:** Eles garantem consistência e evitam problemas com dados sensíveis
3. **Foque na segurança:** No setor financeiro, evitar alucinações é crítico
4. **Teste cenários reais:** Simule perguntas que um cliente faria de verdade
5. **Seja direto no pitch:** 3 minutos passam rápido, vá ao ponto
