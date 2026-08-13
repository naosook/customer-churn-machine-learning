# Customer Churn Prediction

Projeto de Machine Learning desenvolvido em Python para identificar clientes com maior probabilidade de cancelamento de um serviço e apoiar estratégias de retenção.

O projeto utiliza a base pública **Telco Customer Churn**, disponibilizada através do [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn).

O desenvolvimento foi realizado utilizando Python, Jupyter Notebook e VS Code.

## Objetivo

Desenvolver um modelo capaz de estimar a probabilidade de churn dos clientes e identificar aqueles que apresentam maior risco de cancelamento.

A proposta é utilizar essas previsões para apoiar a priorização de ações de retenção.

## Tecnologias

Python

Pandas

NumPy

Scikit Learn

Matplotlib

Jupyter Notebook

VS Code

## Metodologia

O problema foi tratado como uma tarefa de classificação utilizando **Regressão Logística**.

As variáveis numéricas foram padronizadas com `StandardScaler` e as categóricas transformadas com `OneHotEncoder`.

O preprocessing foi implementado utilizando `Pipeline`, evitando o vazamento de informações entre os conjuntos de dados.

A base foi dividida em:

| Conjunto  | Quantidade |
| --------- | ---------: |
| Treino    |      4.507 |
| Validação |      1.127 |
| Teste     |      1.409 |
| Total     |      7.043 |

O conjunto de validação foi utilizado para decisões durante o desenvolvimento, incluindo a escolha do threshold, enquanto o conjunto de teste foi mantido separado para a avaliação final.

## Escolha do threshold

Durante a revisão do processo de avaliação, foi identificado que o threshold precisava ser definido utilizando um conjunto separado do teste.

O processo foi reorganizado para utilizar:

**Treino:** desenvolvimento do modelo

**Validação:** escolha do threshold

**Teste:** avaliação final

O threshold escolhido foi **0,38**, utilizando o F1 Score como critério de equilíbrio entre Precision e Recall.

## Resultados

| Métrica   | Resultado |
| --------- | --------: |
| Accuracy  |    77,50% |
| Precision |    56,24% |
| Recall    |    68,72% |
| F1 Score  |    61,85% |
| ROC AUC   |    84,25% |
| PR AUC    |    63,30% |
| Threshold |      0,38 |

O modelo identificou corretamente **257 dos 374 clientes que realizaram churn**, correspondendo a um recall de **68,72%**.

## Matriz de Confusão

![Matriz de Confusão](images/matriz%20de%20confusao.png)

A matriz mostra os acertos e erros do modelo na classificação dos clientes.

|                 | Previsto: Não Churn | Previsto: Churn |
| --------------- | ------------------: | --------------: |
| Real: Não Churn |                 835 |             200 |
| Real: Churn     |                 117 |             257 |

## Principais variáveis associadas ao churn

![Principais Variáveis Associadas ao Churn](images/principais%20variaveis%20associadas%20ao%20churn.png)

A análise dos coeficientes da Regressão Logística permitiu investigar quais variáveis apresentaram maior associação com a previsão de churn.

Entre as associações positivas, destacam-se:

`InternetService Fiber Optic`: 1,11

`TotalCharges`: 0,49

`MultipleLines Yes`: 0,38

Entre as associações negativas:

`Contract Two Year`: −1,47

`tenure`: −1,21

`Contract One Year`: −0,70

Esses resultados indicam associações do modelo e não relações causais.

## Análises adicionais

Durante o desenvolvimento também foram realizadas investigações sobre:

Multicolinearidade entre variáveis numéricas

VIF e correlações

Impacto de `TotalCharges`

Categorias relacionadas a `No internet service`

Testes de ablation

Essas análises foram utilizadas para avaliar a estabilidade do modelo e compreender melhor suas limitações.

## Limitações

O modelo apresenta algumas limitações:

`TotalCharges` apresentou alta correlação com `tenure`, exigindo cautela na interpretação dos coeficientes.

O threshold de 0,38 foi escolhido com base no F1 Score e não considera diretamente os custos financeiros de ações de retenção.

O modelo utiliza uma base histórica pública do Kaggle, sendo necessário avaliar a qualidade e representatividade dos dados em um cenário real.

Outros algoritmos poderiam ser avaliados para verificar possíveis ganhos de desempenho.

## Conclusão

O projeto demonstrou a aplicação de Machine Learning em um problema de retenção de clientes.

A Regressão Logística apresentou **ROC AUC de 84,25%**, **PR AUC de 63,30%** e **recall de 68,72%** no conjunto de teste.

Além da construção do modelo, o projeto buscou analisar a qualidade da avaliação, interpretar os resultados e investigar limitações relacionadas aos dados e às variáveis.

O desenvolvimento completo, incluindo código, análises e gráficos adicionais, está disponível neste repositório.
