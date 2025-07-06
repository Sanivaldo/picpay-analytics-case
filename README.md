# PicPay – Case Técnico: Receita Financeira

Este repositório apresenta a solução desenvolvida para o case técnico de Analytics Engineer proposto pelo PicPay. O objetivo é aplicar regras de negócio sobre transações financeiras e calcular as receitas provenientes de:

* P2P (pagamentos entre usuários via cartão de crédito)
* BILLS (pagamento de boletos, com ou sem parcelamento)

A solução foi desenvolvida em Azure, utilizando Azure Data Lake Storage Gen2 para armazenamento e Azure Databricks para processamento distribuído com PySpark. O pipeline foi estruturado com base em uma arquitetura em camadas (Bronze, Silver, Gold), organizando a ingestão, transformação e modelagem analítica dos dados.

---

## Tecnologias e Ferramentas

* Azure Data Lake Storage Gen2
* Azure Databricks (com PySpark)
* Delta Lake
* Azure Storage Explorer (upload e validação)
* Power BI (opcional)

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

## Como Executar

1. Suba o notebook `picpay_analytics_case_receitas.ipynb` em um ambiente Databricks com permissão de leitura e escrita no ADLS Gen2.
2. Certifique-se de configurar as credenciais (preferencialmente via `dbutils.secrets`).
3. Execute cada etapa sequencialmente: Bronze → Silver → Gold.
4. Verifique os dados exportados em Delta e `.csv` na camada `analytics`.

---

## Resultado Final

A tabela `transactions_installments` contém todas as transações BILLS parceladas, com cálculo das parcelas, juros, amortização e saldo restante, aplicando a lógica da Tabela Price em PySpark puro.

Essa abordagem elimina dependências externas, é escalável, e reflete práticas modernas de engenharia de dados em ambientes de nuvem.

---

## Autor

Samuel Calado
Engenheiro de Dados | Analista de Dados Sênior
[linkedin.com/in/samuelcalado](https://www.linkedin.com/in/samuelcalado)

---
