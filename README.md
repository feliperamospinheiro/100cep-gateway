<h1 align="center">MVP de Engenharia de Dados</h1>

<p align="center">
  <a href="https://shields.io/">
    <img src="https://img.shields.io/badge/Status-Concluído-green.svg" alt="Status">
  </a>
    <a href="https://en.wikipedia.org/wiki/Data_engineering">
    <img src="https://img.shields.io/badge/Engenharia%20de%20Dados-Data%20Engineering-blue" alt="Engenharia de Dados">
  </a>
  <a href="https://www.databricks.com/">
    <img src="https://img.shields.io/badge/Databricks-Data%20Platform-red?logo=databricks&logoColor=white" alt="Databricks">
  </a>
  <a href="https://spark.apache.org/">
    <img src="https://img.shields.io/badge/Apache%20Spark-Spark-orange?logo=apachespark&logoColor=white" alt="Apache Spark">
  </a>
  <a href="https://www.postgresql.org/docs/">
    <img src="https://img.shields.io/badge/SQL-Query%20Language-yellow?logo=postgresql&logoColor=white" alt="SQL">
  </a>
  <a href="https://pandas.pydata.org/docs/">
    <img src="https://img.shields.io/badge/Pandas-Data%20Analysis-purple?logo=pandas&logoColor=white" alt="Pandas">
  </a>
  <a href="https://seaborn.pydata.org/">
    <img src="https://img.shields.io/badge/Seaborn-Data%20Visualization-lightblue" alt="Seaborn">
  </a>
  <a href="https://geopandas.org/en/stable/">
    <img src="https://img.shields.io/badge/GeoPandas-Geospatial%20Data-brown" alt="GeoPandas">
  </a>
</p>
<p align="center">
  <em>Projeto de sprint da Pós-graduação em Data Science & Analytics (PUC-Rio) focado em engenharia de dados e arquitetura Lakehouse.</em>
</p>

***

<h2 align="center">Visão geral</h2>

Projeto desenvolvido como parte da **sprint de Engenharia de Dados** do programa de **Pós-graduação em Data Science \& Analytics da PUC-Rio**, pensado para compor o portfólio com um caso completo de pipeline analítico em ambiente de Data Lakehouse.
O MVP simula o pipeline transacional da **100cep Gateway**, cobrindo ingestão, processamento, conciliação e chargebacks, com foco em boas práticas de modelagem, governança e observabilidade de dados.

**Este repositório demonstra:**

- Arquitetura **Lakehouse** com camadas **Bronze → Silver → Gold**.
- Construção de um **esquema estrela** para análise de risco, antifraude e receita.
- Documentação técnica (catálogo, ETL, análises, autoavaliação) em formato pronto para portfólio. 

**Organização do repositório:**

```
📁 100cep-gateway
├── 📁 .databricks
│   └── 📁 pipeline
│       ├── 📁 html # contém os arquivos databricks em formato .html
│       └── 📁 notebooks # contém os arquivos databricks em formato .ipynb
├── 📁 datasets 
│   ├── 📁 ai_dataset # contém o dataset gerado pelo modelo OpenAI 5.0
│   └── 📁 olist_dataset # contém os datasets Brazilian E-Commerce Public Dataset by Olist
├── 📁 dbdiagram # código realizado no dbdiagram.io
├── 📁 docs # documentos relevantes para o MVP
├──  📁 images
│    ├── 📁 databricks # evidências do databricks
│    ├── 📁 dbdiagram # schema do dbdiagram.io
│    └── 📁 logo # logo da 100cep Gateway
```


***

<h2 align="center">100cep Gateway</h2>

<p align="center">
  <img src="docs/images/logo/100cep-gateway.png" alt="Logo 100cep Gateway" width="100%">
</p>

A **100cep Gateway** é uma empresa fictícia de infraestrutura de pagamentos *borderless*, criada como cenário de negócio para este MVP de Engenharia de Dados.

O foco da 100cep não é apenas “processar pagamentos”, mas **entender o risco, o comportamento de chargebacks e a saúde da operação transacional** em métodos de pagamento, regiões e perfis de clientes.

No contexto deste projeto, a 100cep Gateway é posicionada como uma plataforma que:

- intermedia pagamentos de e-commerce entre clientes, sellers e provedores financeiros;
- monitora indicadores críticos como taxas de aprovação, faturamento e principalmente **taxas de chargeback**;
- utiliza dados históricos de pedidos, pagamentos, logística e reclamações para orientar decisões de risco, antifraude e estratégia comercial.

O nome **“100cep”** reforça a ideia de uma operação sem fronteiras — sem cidade, estado ou país limitando o fluxo de pagamentos — e justifica a presença de dimensões de geolocalização e análises por região e método de pagamento na camada analítica.


***

<h2 align="center">Contexto acadêmico e objetivos</h2>

Este projeto foi desenvolvido no contexto da pós-graduação em **Data Science \& Analytics (PUC-Rio)**, com foco em engenharia de dados aplicada.

**Objetivos principais:**

- **Pipeline transacional**
Simular o fluxo de uma adquirente/gateway, ingerindo e organizando dados de pedidos, pagamentos, itens, clientes e sellers.
- **Visões analíticas de risco**
Criar camadas analíticas para monitorar chargebacks, GMV, ticket médio e métricas por método de pagamento, seller e localização.
- **Portfólio técnico**
Entregar código + documentação, evidenciando decisões de arquitetura, qualidade de dados e modelagem dimensional.

***
<h2 align="center">Stack técnica</h2>

- **Plataforma de dados:** Databricks (Spark, Delta Lake, Unity Catalog).
- **Linguagem:** Python e SQL.
- **Processamento:** Apache Spark (SQL / DataFrames) e Pandas para análises pontuais.
- **Modelagem:** Arquitetura Medallion (Bronze, Silver, Gold) e esquema estrela.
- **Visualização:** Seaborn, Matplotlib e Geopandas.

***

<h2 align="center">Dataset</h2>

Os dados são baseados no **Brazilian E-Commerce Public Dataset by Olist**, amplamente utilizado em estudos de ciência e engenharia de dados.
O projeto também utiliza um dataset sintético de chargebacks para simular risco e fraude, sem qualquer dado sensível real.

**Fluxo de ingestão:**

1. Download dos arquivos CSV a partir do Kaggle.
2. Upload para **Unity Catalog Volumes** no Databricks, compondo a área de *staging* antes da Bronze.

> ⚠ Nenhum dado pessoal identificável (PII) real é utilizado.

> ⚠ Escopo 100% educacional e de portfólio.

Fluxo de ingestão: `.databricks/pipeline/notebooks/02_download.ipynb`

***

<h2 align="center">Arquitetura e modelagem</h2>

O projeto adota um modelo **Lakehouse** em Databricks, estruturado na arquitetura **Medallion** (Bronze, Silver, Gold), com governança via Unity Catalog.

### 🥉 Bronze · dados brutos

- CSVs armazenados em Delta quase “como chegaram”.
- Foco em auditabilidade e possibilidade de reprocessamento.
- Leitura dos CSV a partir do Volume do Unity Catalog.
- Persistência em tabelas Delta `*_raw`.
- Normalização básica de nomes de tabelas.


### 🥈 Silver · dados tratados

- Padronização de tipos e normalização de chaves.
- Tratamento de nulos e deduplicação.
- Criação de tabelas temáticas (pedidos, pagamentos, clientes, itens).
- Criação de relacionamentos entre pedidos, pagamentos, itens, clientes e sellers.


### 🥇 Gold · modelo analítico

- Dimensões: clientes, vendedores, pagamentos, data, geolocalização, chargebacks.
- Fato: `fato_transacoes`, consolidando pedidos, valores, status e vínculo com chargebacks.
- Modelagem dos dados em Star Schema, conforme indicado na imagem abaixo criada no site dbdiagram.io.

Regras detalhadas de transformação: `docs/documentacao_etl.md`.

Código do diagrama: `dbdiagram/dbdiagram_schema`

<p align="center">
  <img src="docs/images/dbdiagram/star_schema.jpg" alt="Logo 100cep Gateway" width="100%">
</p>

***

<h2 align="center">Catálogo de dados</h2>

O projeto inclui um **Data Catalog** documentando:

- Nome e tipo de cada coluna.
- Domínio esperado, faixas de valores e categorias.
- Descrição funcional e camada de origem.

Arquivo de referência: `docs/catalogo.md`.

***

<h2 align="center">Como executar</h2>

> Ajuste nomes de catálogo/schema e caminhos conforme o seu workspace Databricks.

1. **Configurar ambiente**
    - Criar o catálogo `100cep_gateway` (ou adaptar nos scripts).
    - Configurar Unity Catalog e Volumes para staging.
2. **Rodar os scripts em ordem**
    - `.databricks/pipeline/notebooks/01_preparacao.ipynb`
    - `.databricks/pipeline/notebooks/02_download.ipynb`
    - `.databricks/pipeline/notebooks/03_bronze.ipynb`
    - `.databricks/pipeline/notebooks/04_silver.ipynb`
    - `.databricks/pipeline/notebooks/05_gold.ipynb`
    - `.databricks/pipeline/notebooks/06/qualidade.ipynb`
    - `.databricks/pipeline/notebooks/07_perguntas.ipynb`
    - `.databricks/pipeline/notebooks/08_catalogo.ipynb`

3. **Explorar análises**
    - Abrir `.databricks/pipeline/notebooks/07_perguntas.ipynb` e notebooks analíticos para visualizar KPIs e responder às perguntas de negócio.

***

<h2 align="center">Perguntas de negócio</h2>

A camada Gold foi desenhada para responder perguntas típicas de risco, antifraude e receita em um gateway de pagamentos.

1. **Qual o método de pagamento mais utilizado pelos clientes da 100cep Gateway?**  
2. **Qual o histórico de faturamento do ano de 2017?**  
3. **Qual a proporção de pedidos com e sem solicitação de chargeback?**
4. **Quais métodos de pagamento apresentam maior risco de chargeback?** 
5. **Quais estados apresentam as maiores taxas de chargeback?**  

Detalhes das análises: `.databricks/pipeline/notebooks/07_perguntas.ipynb`

***

<h2 align="center">Autoavaliação</h2>

Como parte da sprint, o projeto inclui uma **autoavaliação** com reflexões técnicas e acadêmicas.

- O que foi cumprido dentro do escopo da sprint.
- Principais desafios (performance, modelagem, ferramentas).
- Próximos passos;

Arquivo: `docs/autoavalicao.md`.

***

<h2 align="center">Autor</h2>

**Felipe Pinheiro** 

[![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:felipervmospinheiro@gmail.com) [![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/feliperamospinheiro)

***

<h2 align="center">Créditos</h2>

Dataset: *[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)* — Olist \& André Sionek.

DOI: *[10.34740/kaggle/dsv/195341](https://doi.org/10.34740/kaggle/dsv/195341)* — Licença *[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)*.

<div align="center">⁂</div>