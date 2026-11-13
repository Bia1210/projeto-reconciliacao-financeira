# Projeto de Reconciliação Financeira (DRE vs. Fluxo de Caixa)

Pipeline analítico e automatizado desenvolvido em **Python**, **SQLite**, **Pandas**, **Power BI** e integrado a uma **IA local (Ollama / Llama 3.2)** para simulação, tratamento (ETL) e diagnóstico de saúde financeira de pequenas e médias empresas.

## 🚀 Funcionalidades do Projeto
- **Geração de Dados Sintéticos & ETL:** Simulação de 150 vendas com prazos de pagamento variados, taxas bancárias e status de inadimplência.
- **Armazenamento Local:** Estruturação dos dados utilizando um banco relacional SQLite (`gestao_financeira.db`).
- **Camada Analítica & Visual:** Gráficos comparativos gerados via Seaborn/Matplotlib e suporte a dashboards interativos no Power BI.
- **Inteligência Artificial Local (CFO AI):** Script autônomo conectado ao Ollama para gerar um relatório executivo com diagnósticos de gap de caixa e plano de ação corretivo.

## 🛠️ Tecnologias Utilizadas
- Python (Pandas, NumPy, Matplotlib, Seaborn)
- SQLite3
- Power BI
- Ollama (LLM Local - Llama 3.2:3b)
