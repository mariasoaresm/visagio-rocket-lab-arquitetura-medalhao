#  Desafio Engenharia de Dados - Visagio Rocket Lab
### Arquitetura Medalhão com PySpark & Databricks

Este repositório contém a solução desenvolvida por **Maria Eduarda Soares Machado** para o desafio técnico da Visagio. O projeto foca na construção de um pipeline de dados robusto, seguindo as melhores práticas de Lakehouse.

---

## Arquitetura do Projeto (Medallion)

O pipeline foi dividido em três camadas lógicas para garantir a qualidade e a linhagem dos dados:

* **🥉 Camada Bronze (Landing):** Ingestão de dados brutos a partir de arquivos CSV (Olist) e consumo da **API do Banco Central** para cotação do Dólar via requisições REST com parâmetros dinâmicos.
* **🥈 Camada Silver (Processing):** Limpeza e padronização. Realizei a **Deduplicação Sênior** utilizando `Window Functions` para garantir a idempotência, além de traduções de status e cálculos de *lead time* (logística).
* **🥇 Camada Gold (Business):** Tabelas agregadas prontas para consumo de BI, destacando os **Top 5 Estados** em faturamento e as **Top 5 Categorias** mais vendidas.

---

## 🛠️ Tecnologias e Ferramentas

* **Linguagem:** Python (PySpark)
* **Plataforma:** Databricks (Azure/AWS/GCP)
* **Orquestração:** Databricks Workflows (Agendamento diário às 13:00)
* **Armazenamento:** Delta Lake

---

## 🌟 Destaques Técnicos

### 1. Deduplicação de Dados
Para garantir que a Silver contenha apenas os registros mais recentes, utilizei a técnica de `row_number()` particionada por ID, garantindo integridade mesmo em cargas repetidas.

### 2. Automação (Jobs)
O pipeline está totalmente orquestrado. Configurei um **Workflow** que encadeia os notebooks Bronze -> Silver -> Gold, com agendamento automático conforme os requisitos do desafio.

### 3. Integração com API
Desenvolvi um módulo de captura de dados externos (Cotação PTAX) com tratamento de erros e conversão de tipos Spark.

---

## 👤 Autora
**Maria Eduarda Soares Machado**
