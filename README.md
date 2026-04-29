# Case Técnico Operations | RevOps Pipeline 2026

Este repositório contém a resolução de um case de Revenue Operations (RevOps) focado na auditoria, limpeza e análise estratégica de dados extraídos de um CRM (Salesforce). O projeto transforma uma base de dados bruta e inconsistente em ativos prontos para a tomada de decisão executiva.

## 📋 Abordagem do Problema

A análise foi dividida em três pilares fundamentais para garantir a integridade dos resultados:

### 1. Auditoria e Saneamento de Dados
A base original continha 413 registros, mas apresentava inconsistências de escopo e qualidade.
- **Filtro de Escopo:** Remoção de 108 linhas referentes a modelos de negócio fora do foco analítico (*Flex/Renewal*, *Retainer* e *Passthrough*).
- **Unidade de Análise:** Ajuste da granularidade de "linhas de produto" para "oportunidade única", evitando a duplicidade de valores em cálculos de Win Rate e Ticket Médio.

### 2. Tratamento de Inconsistências (Data Cleaning)
Utilizando Python/Pandas, foram aplicadas correções sistemáticas:
- **Padronização Taxonômica:** Correção de erros de digitação e variações em campos categóricos (Ex: "Clossed Won" → "Closed Won"; "São Paulo" e "SP" unificados).
- **Recálculo Financeiro:** Identificação de divergências onde o valor total da oportunidade (*Amount*) não batia com a soma dos itens. A "fonte da verdade" foi estabelecida como a soma dos produtos.
- **Limpeza de Caracteres:** Tratamento de erros de codificação (UTF-8) que corrompiam nomes de leads e escritórios.

### 3. Análise Estratégica e Insights
Com os dados limpos, foram gerados indicadores de performance (KPIs) para o ano de 2026, focando em sazonalidade, performance por canal e saúde do pipeline.

---

## 🚀 Entregas Realizadas

1.  **Notebook de Processamento (`Case_TEC_RevOps.ipynb`):** Script completo com toda a lógica de ETL (Extração, Transformação e Carga).
2.  **Base de Dados Corrigida (`opps_corrigido.xlsx`):** Arquivo final saneado com 203 oportunidades únicas e 305 linhas de produtos.
3.  **Relatório de Auditoria (`relatorio_erros.html`):** Documento técnico listando todas as correções efetuadas (Stage, Office, Source e Amount).
4.  **Dashboard Executivo (`analise.html`):** Relatório visual com os principais insights de negócio.

---

## 📈 Resumo dos Resultados (Highlights 2026)

* **Receita Fechada (Closed Won):** R$ 27,19 Milhões.
* **Pipeline Aberto:** R$ 72,90 Milhões em oportunidades ativas.
* **Canal Estrela:** O canal de **Customer Success** provou ser o mais eficiente, concentrando **64,3% da receita** e o maior win rate (**42,4%**).
* **Sazonalidade:** Fevereiro foi o mês de pico, com R$ 9,87 milhões em vendas convertidas.
* **Ticket Médio:** Projetos do tipo *Competitive* possuem o maior valor médio (aprox. R$ 816 mil), embora tenham volume menor.

---

## 🛠️ Recomendações de RevOps

Para evitar o reaparecimento dos problemas de dados encontrados, recomenda-se:
1.  **Validação de CRM:** Implementar campos de seleção (dropdown) em vez de texto livre para *Stage*, *Lead Office* e *Lead Source*.
2.  **Automação de Cálculos:** Travar o campo *Amount* para ser sempre a soma automática dos produtos vinculados.
3.  **Governança:** Estabelecer uma rotina semanal de limpeza de "Aging" para oportunidades estagnadas nos estágios de *Pitched* e *Negotiation*.
