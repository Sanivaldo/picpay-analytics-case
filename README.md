# PicPay – Case Técnico: Finance Analytics - Case receitas

Este repositório apresenta a solução desenvolvida para o case técnico de Finance Analytics - Case receitas proposto pelo PicPay. O objetivo é aplicar regras de negócio sobre transações financeiras e calcular as receitas provenientes de:

* P2P (pagamentos entre usuários via cartão de crédito)
* BILLS (pagamento de boletos, com ou sem parcelamento)

A solução foi desenvolvida em Azure, utilizando Azure Data Lake Storage Gen2 para armazenamento e Azure Databricks para processamento distribuído com PySpark. O pipeline foi estruturado com base em uma arquitetura em camadas (Bronze, Silver, Gold), organizando a ingestão, transformação e modelagem analítica dos dados.

---

## Tecnologias e Ferramentas

A solução foi construída utilizando recursos da plataforma Microsoft Azure, com foco nas boas práticas de engenharia de dados:

- **Azure Data Lake Storage Gen2**: armazenamento em camadas (raw, processed, analytics) com organização baseada em propósito e granularidade.
- **Azure Databricks**: processamento distribuído com PySpark, controle de acesso via Secret Scope e persistência otimizada com Delta Lake.
- **Delta Lake**: gerenciamento de dados processados com versionamento, consistência transacional e desempenho em larga escala.
- **Azure Storage Explorer**: upload e verificação dos dados brutos (CSV) no container de origem (camada raw).
- **Azure Synapse Analytics (SQL Serverless)**: leitura e envio dos dados pra o Pool SQL`OPENROWSET`, o que permitiria a integração com ferramentas de visualização como Power BI e Tableau.

---

## Estrutura do Pipeline

* **Bronze**: ingestão do arquivo `transactions.csv` com os dados brutos no formato original (CSV).
* **Silver**: aplicação de regras de negócio, limpeza e normalização dos dados.
* **Gold**: geração da tabela de parcelas baseadas na Tabela Price, utilizando juros compostos.

Todos os dados processados foram armazenados em formato Delta no Data Lake, e exportados em `.csv` para entrega final.

---

## Estrutura de Pastas no ADLS

```
/raw/picpay_analytics_case_receitas/transactions.csv
/processed/picpay_analytics_case_receitas/transactions_silver
/analytics/picpay_analytics_case_receitas/transactions_installments
/analytics/picpay_analytics_case_receitas/entrega_csv/installments
```

---

## Resultado Final

A tabela `transactions_installments` contém todas as transações BILLS parceladas, com cálculo das parcelas, juros, amortização e saldo restante, aplicando a lógica da Tabela Price em PySpark.


---

## Autor

Samuel Calado
Engenheiro de Dados | Analista de Dados Sênior
[linkedin.com/in/samuelcalado](https://www.linkedin.com/in/samuelcalado)

---
