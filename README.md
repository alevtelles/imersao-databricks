## 🧱 Databricks Lakehouse - Pipeline de Ingestão e Governança de Dados

Este repositório contém a implementação de uma arquitetura Lakehouse utilizando Databricks, Apache Spark e Delta Lake, com foco em ingestão, transformação e governança de dados através do Unity Catalog e versionamento integrado ao GitHub.

### 🚀 Visão Geral

O projeto foi desenvolvido para demonstrar a construção de pipelines modernos de dados baseados em boas práticas de Engenharia de Dados, desde a ingestão de fontes externas até a disponibilização de dados analíticos e inteligentes.

A solução implementa um fluxo end-to-end, cobrindo:

- Ingestão de dados de APIs públicas (ex: preços spot do Bitcoin via Coinbase API);
- Estruturação de camadas Raw, Bronze, Silver e Gold dentro do Unity Catalog;
- Versionamento e governança de dados com Delta Lake;
- Automação de cargas via Jobs e agendamento (cron);
- Criação de camadas analíticas e suporte a agentes de IA para consumo em linguagem natural.

### 🎯 Objetivo

Estabelecer uma arquitetura Lakehouse padronizada e auditável, que permita:

- Centralizar dados provenientes de múltiplas origens (APIs, bancos, etc.);
- Garantir qualidade, rastreabilidade e versionamento em todas as camadas;
- Possibilitar análises e automações baseadas em dados confiáveis e governados;
- Viabilizar integrações com modelos de IA e agentes inteligentes para insights automatizados.


### 🗂️ Estrutura da Arquitetura

```

Sistema de Origem (API / DB)
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

```

Toda a estrutura é gerenciada pelo Unity Catalog, garantindo segurança, governança e controle de acesso em nível de catálogo, schema e tabela.

### Tecnologia

| Categoria                | Ferramenta / Serviço                         |
| ------------------------ | -------------------------------------------- |
| Plataforma de Dados      | **Databricks (Community / Free Edition)**    |
| Engine de Processamento  | **Apache Spark**                             |
| Formato de Armazenamento | **Delta Lake**                               |
| Linguagens               | **Python**, **SQL**                          |
| Governança               | **Unity Catalog**                            |
| Ingestão                 | **Requests (APIs)**, **Fivetran (opcional)** |
| Versionamento            | **Git e GitHub**                             |
| Armazenamento Simulado   | **Amazon S3 (simulado via Volumes)**         |


### 🧩 Pipeline Implementado — Exemplo: Ingestão Coinbase

A pipeline de ingestão (ingestao_bitcoin.py) executa o seguinte fluxo:

- Criação do diretório RAW no volume lakehouse/raw/coinbase/bitcoin_spot;
- Coleta de dados do endpoint https://api.coinbase.com/v2/prices/spot?currency=USD;
- Estruturação de DataFrame com metadados de coleta (ativo, moeda, timestamp UTC, origem);
- Escrita em formato JSON dentro do volume Raw;
- Validação da ingestão com leitura via Spark para contagem e verificação de schema;
- Agendamento via Databricks Job para execução recorrente.

### 🧠 Boas Práticas Adotadas

- Medallion Architecture (Bronze/Silver/Gold) como padrão estrutural;
- Separação entre coleta, transformação e consumo;
- Metadados de rastreabilidade (source_system, ingestion_ts_utc, source_endpoint);
- Versionamento Git integrado ao Databricks;
- Uso de Delta Tables para rastreabilidade e histórico de alterações;
- Agendamento com cron (Jobs) para ingestões contínuas.


### 📈 Resultados e Benefícios

- Pipelines modulares, versionadas e auditáveis;
- Redução de retrabalho e falhas operacionais em processos manuais;
- Base sólida para camadas analíticas e IA;
- Conformidade com princípios de Data Governance;
- Pronta integração com Dashboards, APIs e Agentes Inteligentes.

### 📂 Estrutura de Diretórios
```

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

### 👤 Autor

Engenheiro de Dados: Alexsander 

Contato: alevtelles@gmail.com

LinkedIn: https://www.linkedin.com/in/alexsander-valente/