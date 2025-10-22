## [🧱 Databricks Lakehouse — Pipeline de Ingestão e Governança de Dados](https://github.com/alevtelles/pipeline-de-ingestao-de-dados)
[![GitHub repo size](https://img.shields.io/github/repo-size/alevtelles/pipeline-de-ingestao-de-dados)](https://github.com/alevtelles/pipeline-de-ingestao-de-dados)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

Este repositório contém a implementação de uma arquitetura **Lakehouse** utilizando **Databricks**, **Apache Spark** e **Delta Lake**, com foco em **ingestão, transformação e governança de dados** através do **Unity Catalog** e versionamento integrado ao **GitHub**.

---

## 🚀 Visão Geral

Este projeto apresenta uma implementação prática de arquitetura Lakehouse moderna, voltada à ingestão e governança de dados corporativos.

O objetivo é demonstrar o ciclo completo de engenharia de dados — desde a ingestão de APIs até a curadoria e disponibilização dos dados para consumo analítico e aplicações de Inteligência Artificial — aplicando boas práticas de versionamento, qualidade e rastreabilidade.

O pipeline cobre:

- Ingestão de dados de APIs públicas (ex: **Coinbase** para preço spot do Bitcoin);
- Estruturação das camadas **Raw**, **Bronze**, **Silver** e **Gold** no **Unity Catalog**;
- Automação de cargas via **Jobs** e agendamento (cron);
- Criação de camadas analíticas com **Spark** e **Delta Lake**;
- Integração com agentes de IA e dashboards de consumo.

---

## 🎯 Objetivo

Estabelecer uma arquitetura Lakehouse **padronizada e auditável**, que permita:

- Centralizar dados provenientes de múltiplas origens (APIs, bancos, etc.);
- Garantir **qualidade, rastreabilidade e versionamento** em todas as camadas;
- Possibilitar análises e automações baseadas em **dados governados e confiáveis**;
- Integrar com **modelos de IA e agentes inteligentes** para insights automatizados.

---

## 🗂️ Estrutura da Arquitetura

```text
Sistema de Origem (API / Banco de Dados)
        ↓
Camada Raw (dados brutos)
        ↓
Camada Bronze (dados limpos e padronizados)
        ↓
Camada Silver (modelagem e métricas de negócio)
        ↓
Camada Gold (curadoria e consumo analítico)
        ↓
Agente de IA / BI / Dashboards
````

A gestão de segurança e governança é feita pelo **Unity Catalog**, garantindo controle granular de acesso e lineage entre as camadas.

---

## ⚙️ Tecnologias e Ferramentas

| Categoria                | Ferramenta / Serviço                         |
| ------------------------ | -------------------------------------------- |
| Plataforma de Dados      | **Databricks (Community / Free Edition)**    |
| Engine de Processamento  | **Apache Spark 3.x**                         |
| Formato de Armazenamento | **Delta Lake**                               |
| Linguagens               | **Python**, **SQL**                          |
| Governança               | **Unity Catalog**                            |
| Ingestão                 | **Requests (APIs)**, **Fivetran** (opcional) |
| Versionamento            | **Git e GitHub**                             |
| Armazenamento Simulado   | **Amazon S3 (via Volumes Databricks)**       |

---

## 🧩 Pipeline Implementado — Ingestão da API da Coinbase

O script `notebooks/ingestao_bitcoin.py` implementa o fluxo de ingestão do preço spot do Bitcoin via API pública da Coinbase.

### Etapas do Pipeline:

1. Criação do diretório RAW no volume `/Volumes/lakehouse/raw/coinbase/coinbase/bitcoin_spot`;
2. Coleta de dados do endpoint `https://api.coinbase.com/v2/prices/spot?currency=USD`;
3. Estruturação do DataFrame com metadados:

   * `ativo`, `preco`, `moeda`
   * `horario_coleta`, `source_system`, `source_endpoint`, `ingestion_ts_utc`
4. Escrita em formato **JSON (lines=True)** dentro da camada **Raw**;
5. Validação da ingestão com leitura via **Spark** e contagem de registros;
6. Agendamento de execução recorrente via **Databricks Jobs (cron)**.

---

## 🧠 Boas Práticas Adotadas

* Aplicação da **Medallion Architecture (Bronze → Silver → Gold)**;
* Separação entre **coleta**, **transformação** e **consumo**;
* Inclusão de **metadados de rastreabilidade**:

  * `source_system`, `ingestion_ts_utc`, `source_endpoint`;
* **Versionamento GitHub** integrado ao Databricks;
* Uso de **Delta Tables** para versionamento temporal e histórico de alterações;
* **Agendamento automático** de ingestões via cron ou Jobs;
* Governança com **Unity Catalog** (controle por catálogo, schema e tabela).

---

## 📈 Resultados e Benefícios

* Pipelines **modulares, versionadas e auditáveis**;
* Redução de falhas e retrabalho em processos manuais;
* Base sólida para camadas **analíticas e de IA**;
* Conformidade com boas práticas de **Data Governance**;
* Integração facilitada com **dashboards**, **APIs** e **agentes inteligentes**.

---

## ⚡ Execução e Setup

### Pré-requisitos

* Conta gratuita no **Databricks Community Edition**;
* Conta no **GitHub** com acesso ao repositório;
* Conhecimento básico em **Python** e **SQL**.

### Passos para executar

1. Clone este repositório:

   ```bash
   git clone https://github.com/alevtelles/pipeline-de-ingestao-de-dados.git
   ```
2. Importe os notebooks no **Databricks Workspace**.
3. Configure o **Unity Catalog** e os **Volumes** conforme indicado nos notebooks.
4. Execute o notebook `ingestao_bitcoin.py`.
5. Valide a ingestão consultando os dados com:

   ```python
   df = spark.read.json("/Volumes/lakehouse/raw/coinbase/coinbase/bitcoin_spot")
   df.display()
   ```
6. Agende a execução periódica via **Jobs** no Databricks.

---

## 📂 Estrutura de Diretórios

```text
├── notebooks/
│   ├── ingestao_bitcoin.py
│   ├── transformacoes_silver.sql
│   ├── agregacoes_gold.sql
│
├── docs/
│   ├── arquitetura.md
│   ├── configuracao_unity_catalog.md
│
├── volumes/
│   └── lakehouse/
│       ├── raw/
│       ├── bronze/
│       ├── silver/
│       └── gold/
│
└── README.md
```

---

## 👤 Autor

**Engenheiro de Dados:** Alexsander Valente
**GitHub:** [https://github.com/alevtelles](https://github.com/alevtelles)
**LinkedIn:** [https://linkedin.com/in/alexsandervalente](https://linkedin.com/in/alexsandervalente)



