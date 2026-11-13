# Documentação Técnica: Dashboard de Reconciliação Financeira

## 1. Visão Geral do Projeto
O objetivo principal deste projeto no **Power BI** foi criar uma estrutura de reconciliação financeira entre o faturamento bruto (competência/DRE) e o fluxo financeiro real (caixa líquido), abrangendo o período de **Julho a Setembro de 2026**.

---

## 2. Modelo de Dados e Métricas (Fórmulas DAX)

Para garantir precisão e desempenho no painel, todas as métricas foram construídas utilizando medidas explícitas em **DAX (Data Analysis Expressions)**.

### **2.1. Faturamento Total**
Soma de todos os valores brutos faturados no período analisado.

```dax
Faturamento Total = 
SUM('Caixa Líquido'[valor_bruto])
```
* **Formatação:** Moeda (`R$`) com 2 casas decimais.
* **Propósito:** Estabelecer a base de receita total (regime de competência).

---

### **2.2. Caixa Líquido**
Soma do valor efetivamente líquido que ingressou nas contas da empresa.

```dax
Caixa Líquido = 
SUM('Caixa Líquido'[valor_liquido])
```
* **Formatação:** Moeda (`R$`) com 2 casas decimais.
* **Propósito:** Medir a entrada real de recursos financeiros.

---

### **2.3. Gap de Caixa (Divergência)**
Calcula a diferença absoluta entre o valor faturado e o valor recebido em caixa.

```dax
Gap de Caixa = 
[Faturamento Total] - [Caixa Líquido]
```
* **Formatação:** Moeda (`R$`) com 2 casas decimais.
* **Propósito:** Identificar o montante retido por inadimplência, taxas, descontos ou prazos de recebimento.

---

### **2.4. Taxa de Perda %**
Métrica percentual que avalia o impacto proporcional do Gap de Caixa em relação ao Faturamento Total.

```dax
Taxa de Perda % = 
DIVIDE(
    [Gap de Caixa], 
    [Faturamento Total], 
    0
)
```
* **Formatação:** Percentual (`%`) com 2 casas decimais.
* **Propósito:** Fornecer um indicador relativo de eficiência de conversão (usando a função `DIVIDE` para evitar erros de divisão por zero).

---

## 3. Estrutura Visual e Arquitetura da Interface

O dashboard foi projetado seguindo as melhores práticas de UX/UI para Business Intelligence:

### **A. Cartões de KPI (Destaque Superior)**
* **Componentes:** 4 cartões posicionados em linha no topo.
* **Métricas:** `Faturamento Total`, `Caixa Líquido`, `Gap de Caixa` e `Taxa de Perda %`.
* **Ajustes Realizados:** Aumento de fonte nos rótulos de categoria e nos valores de chamada para garantir leitura rápida.

### **B. Filtro Dinâmico (Segmentação de Dados)**
* **Campo Utilizado:** `categoria` (`Consultoria em IA`, `Licenciamento de Software`, `Serviços de TI`).
* **Comportamento:** Filtra simultaneamente todos os cartões e o gráfico de linha em tempo real.
* **Ajustes Realizados:** Aumento do tamanho do texto no painel *Valores* para melhor usabilidade.

### **C. Gráfico de Evolução Temporal (Gráfico de Linhas)**
* **Eixo X:** Hierarquia temporal baseada em `data_emissao` (`Ano`, `Trimestre`, `Mês`, `Dia`).
* **Ação Executada:** Utilizado o recurso de *Drill-down / Expandir tudo um nível na hierarquia* para visualização detalhada mês a mês.
* **Eixo Y Primário:** `Faturamento Total`
* **Eixo Y Secundário:** `Caixa Líquido`
* **Ajustes Realizados:** Formatação personalizada dos eixos e ampliação do título principal em `Geral > Título`.

---

## 4. Resultados Consolidados no Projeto

| Métrica | Valor Consolidado | % do Faturamento |
| :--- | :---: | :---: |
| **Faturamento Total** | **R$ 128,00 Mi** | 100,00% |
| **Caixa Líquido** | **R$ 102,50 Mi** | 80,08% |
| **Gap de Caixa** | **R$ 25,50 Mi** | 19,92% |
| **Taxa de Perda %** | **19,92%** | — |

---

## 5. Boas Práticas e Recomendações Técnicas
1. **Pincel de Formatação:** Utilizado para padronizar fontes, cores e espaçamentos entre os visuais.
2. **Uso de Medidas vs. Colunas Calculadas:** Todas as agregações foram feitas via medidas DAX dinâmicas, otimizando o uso de memória do modelo VertiPaq.
3. **Organização da Hierarquia:** A expansão temporal permite análises em diferentes níveis agregados sem a necessidade de múltiplos gráficos.