# Customer Churn Prediction

Projeto de Machine Learning desenvolvido em Python para identificar clientes com maior probabilidade de cancelamento de um serviço.

O objetivo é utilizar dados históricos de clientes para identificar padrões associados ao churn e gerar uma classificação de risco que possa apoiar estratégias de retenção.

## Sobre o projeto

O projeto utiliza a base pública Telco Customer Churn, obtida no Kaggle, contendo informações sobre clientes de uma empresa de telecomunicações.

A partir dessas informações, foi desenvolvido um modelo de classificação capaz de estimar a probabilidade de um cliente realizar churn.

O projeto foi desenvolvido utilizando Python, Jupyter Notebook e VS Code.

A abordagem escolhida foi uma Regressão Logística, permitindo não apenas realizar previsões, mas também analisar os coeficientes do modelo e investigar quais variáveis estão mais associadas à previsão de churn.

## Objetivo

O objetivo principal é identificar clientes com maior probabilidade de cancelamento antes que o churn aconteça.

A partir dessa identificação, uma empresa poderia priorizar clientes para ações de retenção, como contato personalizado, ofertas ou outras estratégias comerciais.

O projeto foi estruturado considerando o problema como uma classificação de risco, e não apenas como uma previsão binária.

## Dataset

O dataset utilizado foi o Telco Customer Churn, disponibilizado publicamente através do [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn).

A base possui 7.043 clientes e apresenta aproximadamente 26,5% de clientes classificados como churn.

As variáveis incluem informações relacionadas a características dos clientes, serviços contratados, tipo de contrato, forma de pagamento, tempo de relacionamento e valores cobrados.

## Tecnologias utilizadas

Python

Pandas

NumPy

Scikit Learn

Matplotlib

Jupyter Notebook

VS Code

## Etapas do projeto

### 1. Exploração dos dados

Inicialmente foram analisadas as características da base, suas variáveis e a distribuição da variável alvo.

Também foi analisada a proporção entre clientes que permaneceram e clientes que realizaram churn.

### 2. Preparação dos dados

As variáveis foram separadas entre características numéricas e categóricas.

As variáveis numéricas foram processadas utilizando `StandardScaler`.

As variáveis categóricas foram transformadas utilizando `OneHotEncoder`, com `drop='first'` e `handle_unknown='ignore'`.

O preprocessing foi implementado dentro de um Pipeline, evitando que informações dos conjuntos de validação e teste fossem utilizadas durante o ajuste do preprocessing.

### 3. Divisão dos dados

O conjunto de dados foi dividido em três partes:

| Conjunto  | Quantidade |
| --------- | ---------: |
| Treino    |      4.507 |
| Validação |      1.127 |
| Teste     |      1.409 |
| Total     |      7.043 |

O conjunto de treino foi utilizado para desenvolver o modelo.

O conjunto de validação foi utilizado para decisões relacionadas ao modelo, incluindo a escolha do threshold.

O conjunto de teste permaneceu separado para a avaliação final.

Essa estrutura permitiu manter uma avaliação final independente das decisões realizadas durante o desenvolvimento.

## Modelo

O modelo utilizado foi uma Regressão Logística.

A escolha foi baseada principalmente na possibilidade de combinar capacidade preditiva com interpretabilidade.

Além de classificar os clientes, o modelo permite analisar seus coeficientes para compreender quais variáveis possuem maior associação com a previsão de churn.

## Escolha do threshold

Durante o desenvolvimento foi realizada uma revisão do processo de avaliação do modelo.

Foi identificado que a escolha do threshold precisava ser realizada utilizando um conjunto separado do teste.

Para evitar que o conjunto utilizado para a avaliação final influenciasse uma decisão do modelo, o processo foi reorganizado utilizando três conjuntos:

Treino para desenvolvimento do modelo.

Validação para escolha do threshold.

Teste para avaliação final.

O threshold escolhido na validação foi:

**0,38**

A escolha foi realizada buscando o melhor equilíbrio entre Precision e Recall por meio do F1 score.

## Resultados finais

Após a definição do threshold, o modelo foi avaliado no conjunto de teste.

| Métrica   | Resultado |
| --------- | --------: |
| Accuracy  |    77,50% |
| Precision |    56,24% |
| Recall    |    68,72% |
| F1 Score  |    61,85% |
| ROC AUC   |    84,25% |
| PR AUC    |    63,30% |
| Threshold |      0,38 |

O modelo sinalizou 457 clientes no conjunto de teste, correspondendo a 32,43% dessa base.

## Matriz de confusão

![Matriz de Confusão](images/matriz%20de%20confusao.png)

A matriz de confusão obtida no conjunto de teste foi:

|                 | Previsto: Não Churn | Previsto: Churn |
| --------------- | ------------------: | --------------: |
| Real: Não Churn |                 835 |             200 |
| Real: Churn     |                 117 |             257 |

O modelo identificou corretamente 257 dos 374 clientes que realmente realizaram churn.

Isso corresponde a um recall de aproximadamente 68,72%.

Entre os clientes classificados pelo modelo como potenciais casos de churn, 257 realmente realizaram churn, resultando em uma precision de aproximadamente 56,24%.

## Curva ROC

ADICIONE AQUI A IMAGEM "curva roc"

A curva ROC apresentou AUC de 0,8425 no conjunto de teste.

Esse resultado indica uma boa capacidade de discriminação entre clientes que realizaram churn e clientes que permaneceram.

O desempenho está significativamente acima de um classificador aleatório, representado pela referência de AUC igual a 0,50.

## Curva Precision Recall

ADICIONE AQUI A IMAGEM "curva precision recall"

A curva Precision Recall apresentou PR AUC de 0,6330.

A prevalência de churn no conjunto de teste é aproximadamente 26,5%, funcionando como referência para a baseline da curva Precision Recall.

O resultado demonstra que o modelo apresenta capacidade de identificar clientes com churn acima do desempenho esperado de uma classificação baseada apenas na prevalência da classe positiva.

## Distribuição das probabilidades

ADICIONE AQUI A IMAGEM "probabilidades de churn"

A distribuição das probabilidades permite observar como o modelo diferencia clientes que realizaram churn daqueles que permaneceram.

Clientes classificados como Não Churn apresentam maior concentração em probabilidades mais baixas, enquanto os clientes que realizaram churn apresentam maior concentração em probabilidades elevadas.

O threshold de 0,38 foi utilizado como ponto de corte para transformar a probabilidade prevista em uma classificação.

## Classificação de risco dos clientes

ADICIONE AQUI A IMAGEM "distribuicao dos clientes por nivel de risco"

A partir das probabilidades previstas, os clientes foram segmentados em três níveis de risco: Baixo, Médio e Alto.

Do total da base analisada, 866 clientes foram classificados como risco Baixo, 334 como risco Médio e 209 como risco Alto.

ADICIONE AQUI A IMAGEM "clientes de alto risco por tempo de relacionamento"

Ao analisar os clientes classificados como Alto Risco em relação ao tempo de relacionamento com a empresa, observa-se maior concentração entre os clientes mais recentes: 158 clientes de alto risco possuem entre 0 e 6 meses de relacionamento, seguidos por 63 clientes entre 13 e 24 meses, 53 clientes entre 7 e 12 meses e 44 clientes com 25 meses ou mais.

Esse padrão sugere que os primeiros meses de relacionamento representam um período crítico para ações de retenção.

## Principais variáveis associadas ao churn

![Principais Variáveis Associadas ao Churn](images/principais%20variaveis%20associadas%20ao%20churn.png)

A análise dos coeficientes da Regressão Logística permite identificar variáveis que apresentam maior associação com a previsão de churn.

Entre os maiores coeficientes positivos estão:

`InternetService Fiber Optic`: 1,11

`TotalCharges`: 0,49

`MultipleLines Yes`: 0,38

`StreamingTV Yes`: 0,38

`StreamingMovies Yes`: 0,32

`PaymentMethod Electronic Check`: 0,30

`PaperlessBilling Yes`: 0,29

Entre os maiores coeficientes negativos estão:

`Contract Two Year`: −1,47

`tenure`: −1,21

`Contract One Year`: −0,70

`PhoneService Yes`: −0,49

`OnlineSecurity Yes`: −0,37

`TechSupport Yes`: −0,34

`MonthlyCharges`: −0,34

`Dependents Yes`: −0,25

Os resultados sugerem uma associação importante entre contratos mais longos, maior tempo de relacionamento e menor probabilidade prevista de churn.

Por outro lado, clientes com serviço de internet Fiber Optic apresentam uma associação positiva relevante com a previsão de churn no modelo.

É importante destacar que os coeficientes representam associações utilizadas pelo modelo e não relações causais.

## Análise de multicolinearidade

Durante a análise do modelo foi investigada a presença de multicolinearidade entre variáveis numéricas.

Os valores de VIF encontrados foram:

| Variável       |  VIF |
| -------------- | ---: |
| tenure         | 6,47 |
| MonthlyCharges | 3,39 |
| TotalCharges   | 8,21 |

Também foi analisada a correlação entre as variáveis.

| Variáveis                     | Correlação |
| ----------------------------- | ---------: |
| tenure × TotalCharges         |      0,830 |
| MonthlyCharges × TotalCharges |      0,654 |
| tenure × MonthlyCharges       |      0,257 |

A variável `TotalCharges` apresentou VIF de 8,21 e correlação de 0,830 com `tenure`, indicando uma relação forte entre essas variáveis.

## Teste de ablation: TotalCharges

Para investigar o impacto da multicolinearidade, foi realizado um teste removendo `TotalCharges` do modelo.

O modelo sem `TotalCharges` apresentou:

| Métrica   | Resultado |
| --------- | --------: |
| Accuracy  |    0,7970 |
| Precision |    0,6375 |
| Recall    |    0,5455 |
| F1 Score  |    0,5879 |
| ROC AUC   |    0,8393 |

A diferença de ROC AUC em relação ao modelo utilizado foi pequena.

Com base nessa investigação, `TotalCharges` foi mantida no modelo por sua utilidade preditiva, mas sua interpretação individual deve ser realizada com cautela devido à multicolinearidade.

## Teste de ablation: No Internet Service

Também foi investigada a presença de informações redundantes relacionadas à categoria `No internet service`.

Foram removidas as variáveis:

`OnlineSecurity`

`OnlineBackup`

`DeviceProtection`

`TechSupport`

`StreamingTV`

`StreamingMovies`

O resultado foi comparado com o modelo completo na validação.

| Modelo                  | ROC AUC | PR AUC | Precision | Recall | F1 Score |
| ----------------------- | ------: | -----: | --------: | -----: | -------: |
| Modelo completo         |  0,8482 | 0,6664 |    0,6077 | 0,6890 |   0,6458 |
| Sem No internet service |  0,8467 | 0,6640 |    0,6006 | 0,6689 |   0,6329 |

A diferença de desempenho foi pequena.

A investigação foi mantida como parte da análise metodológica do projeto, principalmente para evitar interpretações isoladas e inadequadas dessas categorias.

## Limitações

O modelo apresenta algumas limitações que devem ser consideradas.

### Multicolinearidade

`TotalCharges` apresentou VIF de 8,21 e correlação de 0,830 com `tenure`.

A variável foi mantida devido ao seu comportamento preditivo, mas seus coeficientes devem ser interpretados com cautela.

### Categorias relacionadas a No Internet Service

As variáveis relacionadas a serviços adicionais possuem categorias `No internet service`, que carregam informações relacionadas à ausência de serviço de internet.

Foi realizado um teste de ablation para investigar o impacto dessas variáveis.

### Threshold

O threshold de 0,38 foi escolhido com base no F1 score.

Essa escolha não considera diretamente os custos reais de uma ação de retenção ou o valor financeiro de cada cliente.

Em um cenário empresarial real, uma matriz de custos poderia ser utilizada para definir um threshold orientado ao impacto financeiro.

### Modelo

Foi utilizada uma Regressão Logística.

Outros modelos de Machine Learning, como Random Forest ou modelos de boosting, poderiam ser avaliados em trabalhos futuros para verificar se existe ganho adicional de desempenho.

### Dados

O modelo foi desenvolvido utilizando uma base histórica pública do Kaggle.

Em um cenário real, seria necessário avaliar a qualidade, atualização e representatividade dos dados disponíveis para a empresa.

## Conclusão

O projeto demonstrou a aplicação de Machine Learning para um problema de retenção de clientes.

A Regressão Logística apresentou ROC AUC de 84,25% e PR AUC de 63,30% no conjunto de teste.

Com threshold de 0,38, o modelo alcançou recall de 68,72%, identificando 257 dos 374 clientes que realizaram churn no conjunto de teste.

Além da avaliação preditiva, o projeto incluiu investigações sobre multicolinearidade, VIF, correlação e redundância entre variáveis.

O principal objetivo não foi apenas construir um modelo com uma métrica elevada, mas desenvolver um processo de análise que considerasse a qualidade da avaliação, a interpretação dos resultados e as limitações da abordagem.
