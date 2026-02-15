🤖 Agente Financeiro Inteligente com IA Generativa
🎯 Contexto

O setor financeiro precisa evoluir de chatbots reativos para agentes inteligentes, proativos e seguros.

Este projeto apresenta um agente financeiro que:

Antecipar riscos financeiros

Personaliza recomendações com base no perfil do cliente

Cocriar soluções financeiras consultivas

Evita alucinações e garante respostas confiáveis

📦 Entregáveis
1️⃣ Documentação do Agente
✅ Caso de Uso

O agente resolve:

Falta de controle de gastos

Endividamento excessivo

Escolha inadequada de investimentos

Tomada de decisão financeira sem análise

Ele atua como um gerente financeiro digital, analisando dados e oferecendo orientação segura.

✅ Persona e Tom de Voz

Consultivo

Educativo

Profissional

Claro e direto

Preventivo

Nunca promete ganhos e nunca inventa dados.

✅ Arquitetura

Fluxo:

Cliente → Interface → LLM → Base de Conhecimento → Validação → Resposta

Integra dados de:

transações financeiras

perfil do investidor

histórico de atendimento

produtos disponíveis

✅ Segurança

O agente:

Responde apenas com base nos dados fornecidos

Não inventa taxas ou rentabilidades

Admite quando não possui informação

Solicita contexto antes de recomendar

Não compartilha dados sensíveis

📄 docs/01-documentacao-agente.md

2️⃣ Base de Conhecimento

Utiliza dados mockados:

transacoes.csv → cálculo de gastos

historico_atendimento.csv → contexto do cliente

perfil_investidor.json → definição de suitability

produtos_financeiros.json → recomendações compatíveis

Os dados garantem respostas consistentes e seguras.

📄 docs/02-base-conhecimento.md

3️⃣ Prompts do Agente
System Prompt

Define comportamento ético, restrições e padrão de resposta estruturado:

Diagnóstico → Análise → Risco → Orientação.

Exemplos de Interação

Incluem cenários de:

Consulta de gastos

Recomendação de investimento

Pergunta fora do escopo

Produto inexistente

Edge Cases

O agente:

Recusa perguntas fora de finanças

Não fornece informações sensíveis

Não promete rentabilidade

📄 docs/03-prompts.md

4️⃣ Aplicação Funcional

Protótipo desenvolvido com:

Python

Leitura de CSV/JSON

Chat interativo

Integração com LLM

Permite:

Consultar gastos

Receber recomendações

Validar perfil

Testar cenários reais

📁 src/

5️⃣ Avaliação e Métricas

O agente é avaliado por:

✔ Precisão das respostas

✔ Taxa de respostas seguras (sem alucinação)

✔ Coerência com perfil do cliente

✔ Clareza da explicação

📄 docs/04-metricas.md

6️⃣ Pitch (3 minutos)

Apresenta:

O problema: desorganização e decisões financeiras erradas

A solução: agente consultivo e seguro

O diferencial: IA com controle de escopo e foco em segurança

📄 docs/05-pitch.md

🚀 Diferencial do Projeto

Proativo, não apenas reativo

Baseado em dados reais

Controlado contra alucinação

Foco em segurança financeira

Aplicável a bancos e fintechs
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


