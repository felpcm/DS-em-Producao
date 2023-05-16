# Previsão de vendas para a Rossmann Drugstore

![rossmann](img/rossmann.jpg)

# 1 - INTRODUÇÃO
## 1.1 - Sobre a Rossmann Drugstore

A Rossmann é uma das maiores cadeias de farmácias da Europa, com aproximadamente de 56.200 funcionários e mais de 4.000 lojas. Em 2019, a Rossmann faturou mais de 10 bilhões de Euros em diversos países.

Em 2021, as vendas aumentaram 8,1% para 11,1 bilhões de euros. Há um total de 4.361 filiais da Rossmann, sendo 2.231 na Alemanha. O número atual de filiais estrangeiras é: Polônia (1580), Hungria (mais de 230), República Tcheca (mais de 150), Turquia (mais de 120), Albânia (15), Kosovo (6) e Espanha (5).

## 1.2  - Questão e entendimento do negócio

Atualmente, os gerentes de loja da Rossmann têm a tarefa de prever suas vendas diárias com até seis semanas de antecedência. A demanda partiu do CFO da empresa, pois a rede pretende fazer uma série de reformas e alterações no visual de suas unidades a fim de renovar e melhorar a imagem de sua empresa, agregando valor a mesma.

As vendas da loja são influenciadas por muitos fatores, incluindo promoções, concorrência, feriados escolares e estaduais, sazonalidade e localidade. Com milhares de gerentes individuais prevendo vendas com base em suas circunstâncias únicas, a precisão dos resultados pode variar bastante, assim gerando um cenário desafiador para a empresa. Assim, o papel do cientista de dados se torna fundamental para esse processo se tornar mais eficiente e confiável.

## 1.3 - Dados utilizados

Para a resolução do problema de negócio foram disponibilizados dados históricos de vendas de 1.115 lojas Rossmann na plataforma [Kaggle](https://www.kaggle.com/c/rossmann-store-sales). O histórico é referente aos dados destas lojas do ano de 2015 até 2017. Vale ressaltar que algumas lojas no conjunto de dados foram temporariamente fechadas para reforma.

As seguintes features são encontradas no dataset:

| Atributos | Descrição |
| ------ | ------- |
| Id | Identificador da transação |
| Store | Identificador único para cada loja |
| Sales | Total de vendas no dia (target) |
| Customers | Número de clientes no dia |
| Open | Indica se a loja está aberta ou fechada ( 0 = fechada, 1 = aberta) |
| StateHoliday | Indica feriado estadual, normalmente as lojas fecham nos feriados |
| SchoolHoliday | Indica feriado escolar |
| StoreType | Tipo da loja |
| Assortment | Nível de variedade de produtos da loja |
| CompetitionDistance | Distância em metros do concorrente mais próximo |
| CompetitionOpenSince | Indica mês e ano que o concorrente mais próximo abriu |
| Promo | Descreve se está ocorrendo alguma promoção na loja |
| Promo2 | Descreve se houve extensão do prazo final da promoção |
| Promo2Since | Descreve mês e ano que a loja iniciou a Promo2 |
| PromoInterval | Descreve os intervalos consecutivos em que a Promo2 é iniciada |

# 2 - METODOLOGIA

## 2.1 - Planejamento da Solução

Para o desenvolvimento do projeto foi utilizada um processo cíclico chamado CRISP-DS (Cross-Industry Standard Process - Data Science). A ideia principal é percorrer as fases do processo, para que você tenha, de forma ágil, um produto mínimo viável a agregar ao negócio. Depois de percorrer o primeiro ciclo, você pode iterar novamente, encontrar novos insights, criar novas features, melhorar o modelo, ajustar parâmetros, a fim de a precisão e entregar mais valor. O ciclo pode ser repetido quantas vezes forem necessárias até atingir o objetivo final do time de negócio.

***Etapas do método CRISP-DS***
![CRISP-DS](img/crisp-ds.jpg)


## 2.2 - Desenvolvimento da Solução

Seguindo a metodologia CRISP-DS a seguinte sequência de tarefas foram realizadas no desenvolvimentos do projeto:

***Passo 01 - Descrição dos dados:***

Esta etapa consiste em conhecer os dados (dataset) e suas dimensões. É verificado também quais os tipos de variáveis estão presentes no dataset (numéricas, categóricas, temporais) e também os dados faltantes e suas motivações, pois estes podem inviabilizar a continuidade projeto. Foi feito também uma análise descritiva dos dados para mensurar média, moda, mediana, desvio padrão, range, para assim ter uma noção de grandeza e limites dos dados. Com todas essas informações é possível aplicar as técnicas corretas para manipular os dados a fim de que o desenvolvimento flua.

Em linhas gerais, foram identificados e substituídos as linhas com dados faltantes, foi feito um check para saber o tipo dado era correto para cada uma das colunas e depois foi resumido todo o conteúdo do dados em uma tabela utilizando técnicas da estatística descritiva.

***Passo 02 - Feature Engineering:***

Nesta etapa a ideia principal é derivar features a partir do conjunto original de variáveis, assim, teremos as variáveis disponíveis para estudo durante a etapa de Análise Exploratória de Dados. Para isso, foi criado um mapa que serve como um roteiro para mostrar quais variáveis precisamos derivar para fazer determinadas análises através de uma lista empírica de hipóteses. Então a lista é analisada para validar ou descartar de cada uma dessas hipóteses, gerando, assim, insights para o projeto.

Vale ressaltar quais são os três elementos que constituem o mapa mental de hipósteses:
- FENÔMENO -> Aquilo que está sendo medido ou modelado (ex.: vendas)
- AGENTES -> Entidades que impactam o fenômeno (ex.: clientes, lojas, produtos)
- ATRIBUTOS DO AGENTE -> São os atributos que descrevem o agente (ex.: para o agente "cliente" temos os atributos idade, escolaridade, salário, etc.)

***Mapa Mental de Hipóteses***
![MAPA MENTAL DE HIPÓTESES](img/MindMapHypothesis.png)

***Passo 03 - Filtragem das Variáveis:***

O propósito desta fase consistiu em realizar uma filtragem criteriosa das linhas e excluir as colunas que não possuem relevância para o modelo em questão ou que estão além do escopo do negócio. Um exemplo disso seria a exclusão dos dias em que as lojas não estavam operando e/ou não registraram vendas, pois tais informações não contribuiriam para a análise e o entendimento dos dados.

***Passo 04 - Análise Exploratória dos Dados:***

O objetivo primordial desta etapa foi conduzir uma exploração minuciosa dos dados, a fim de descobrir insights relevantes e compreender melhor a importância das variáveis no processo de aprendizado do modelo. Para alcançar esse objetivo, foram realizadas análises em diferentes níveis: análise individual das variáveis (análise univariada), análise das relações entre cada variável e a variável de resposta (análise bivariada) e análise conjunta das variáveis (análise multivariada).

Para cada tipo de análise, utilizaram-se diversas técnicas e ferramentas estatísticas. Histogramas foram empregados para examinar a distribuição das variáveis, enquanto boxplots foram utilizados para analisar o intervalo e detectar possíveis valores atípicos. A matriz de confusão foi empregada para medir a correlação entre as variáveis, assim como o método de Kramer's V e outros métodos apropriados. Além disso, nesta fase, as hipóteses estabelecidas na etapa anterior foram testadas e confirmadas ou refutadas.

Adicionalmente, as features (variáveis) foram ordenadas de acordo com sua relevância para o modelo, proporcionando uma compreensão mais clara de quais características têm um impacto mais significativo nos resultados finais.

***Matriz de Confusão***
![Matriz de Confusão](img/matriz-confusao.png)

***Passo 05 - Preparação dos dados:***

Nesta etapa, o objetivo principal foi selecionar os atributos mais relevantes para o treinamento do modelo. Para alcançar esse objetivo, foi empregado o algoritmo Boruta, uma técnica amplamente utilizada em ciência de dados. O algoritmo Boruta realizou a seleção das variáveis, destacando aquelas que apresentaram maior relevância para o fenômeno em estudo.

O algoritmo Boruta é uma abordagem baseada em técnicas de Random Forest, que avalia a importância das variáveis através de um processo iterativo. Ele compara o desempenho das variáveis originais com versões aleatórias (chamadas de sombras) e identifica quais variáveis possuem um desempenho estatisticamente superior. Dessa forma, o Boruta pode ajudar a identificar as variáveis mais relevantes, fornecendo insights sobre quais características têm maior influência nos resultados do modelo.

No entanto, é importante ressaltar que, em alguns casos, certas features criadas manualmente durante a etapa de Feature Engineering podem ter sido consideradas relevantes, mesmo que o algoritmo Boruta não as tenha selecionado. Portanto, essas features foram incluídas manualmente, reconhecendo seu potencial contributivo para o modelo, mesmo que não tenham sido destacadas pelo algoritmo Boruta.

***Passo 07 - Modelagem de Machine Learning:***

Na modelagem foram realizados os treinamentos dos modelos de machine learning selecionados para o problema em questão:

- Average Model
- Linear Regression
- Linear Regression Regularized (Lasso)
- Random Forest Regressor
- XGBoost Regressor

 Na primeira parte da etapa foi realizado a avaliação simples do modelo (Single Performance) e na segunda parte foi aplicado o método de Cross Validation (Real Performance). O método de validação cruzada consiste em separar os dados de teste em dois conjuntos: conjunto de teste e o menor de validação, após treinar e medir o desempenho do modelo esses dois conjuntos são redimensionados de forma a testar e validar o modelo em todas as porções dos dados.

Single Performance:
| Model Name |	MAE |	MAPE |	RMSE |
|  --- | --- | --- | --- |
|	Random Forest Regressor |	679.598831 |	0.099913 |	1011.119437 |
|	Average Model |	1354.800353 |	0.206400 | 1835.135542 |
|	Linear Regression |	1867.089774 |	0.292694 |	2671.049215 |
|	Linear Regression - Lasso |	1891.704881 |	0.289106 |	2744.451737 |
|	XGboost Regressor |	6685.509529 |	0.949034 |	7337.089204 |

Real Performance:
| Model Name |	MAE CV |	MAPE CV |	RMSE CV |
|  --- | --- | --- | --- |
|	Linear Regression |	2081.73 +/- 295.63 |	0.3 +/- 0.02 |	2952.52 +/- 468.37 |
|	Lasso |	2116.38 +/- 341.5 |	0.29 +/- 0.01 |	3057.75 +/- 504.26 |
|	Random Forest Regressor |	836.61 +/- 217.1 |	0.12 +/- 0.02 |	1254.3 +/- 316.17 |
|	XGBoost Regressor |	7053.23 +/- 594.13 |	0.95 +/- 0.0 |	7724.0 +/- 695.19 |

Dentre os modelos testados, apesar de parecer contraditório, a escolha do modelo XGBoost foi baseado, entre outros fatores menores, no tempo de processamento do algoritmo, que é muito menor que o Random Forest, significando redução de custos de processamento e cloud. Além de que na etapa de Hyperparameter Fine Tuning será possível fazer ajustes significativos para melhora da performance.


Na fase de modelagem, foram conduzidos treinamentos dos modelos de machine learning selecionados para resolver o problema em questão. Dentre os modelos utilizados estavam o Average Model, Linear Regression, Linear Regression Regularizada (Lasso), Random Forest Regressor e XGBoost Regressor.

Inicialmente, foi realizada uma avaliação simples do desempenho dos modelos, conhecida como "Single Performance". Em seguida, foi aplicado o método de Cross Validation (Validação Cruzada) para obter uma avaliação mais robusta, também chamada de "Real Performance".

A técnica de Cross Validation é amplamente utilizada em problemas de ciência de dados, especialmente em casos de séries temporais. Ela consiste em dividir os dados em conjuntos de treinamento, teste e validação. No entanto, ao contrário da divisão tradicional em conjunto de treinamento e teste, a validação cruzada envolve a criação de múltiplos conjuntos de treinamento e teste, permitindo que cada porção dos dados seja usada como conjunto de teste em algum momento.

Essa abordagem é particularmente importante em problemas de séries temporais, onde a ordem dos dados é relevante. A validação cruzada nos permite avaliar o desempenho do modelo em diferentes períodos de tempo, o que ajuda a verificar se o modelo é capaz de generalizar bem e fazer previsões precisas em diferentes momentos.

Na tabela de "Single Performance", podemos observar as métricas de desempenho (MAE, MAPE e RMSE) para cada modelo individualmente. Já na tabela de "Cross Validation Performance", são apresentadas as métricas resultantes da aplicação do método de validação cruzada, com intervalos de confiança, representando a variabilidade do desempenho do modelo em diferentes divisões dos dados.

Single Performance:
| Model Name |	MAE	MAPE |	RMSE |
|	Random Forest Regressor |	679.598831 |	0.099913 |	1011.119437 |
|	Average Model |	1354.800353 |	0.206400 | 1835.135542 |
|	Linear Regression |	1867.089774	0.292694	2671.049215 |
|	Linear Regression - Lasso |	1891.704881 |	0.289106 |	2744.451737 |
|	XGboost Regressor |	6685.509529 |	0.949034 |	7337.089204 |

Cross Validation Performance
| Model Name |	MAE CV |	MAPE CV |	RMSE CV |
|	Linear Regression |	2081.73 +/- 295.63 |	0.3 +/- 0.02 |	2952.52 +/- 468.37 |
|	Lasso |	2116.38 +/- 341.5 |	0.29 +/- 0.01 |	3057.75 +/- 504.26 |
|	Random Forest Regressor |	836.61 +/- 217.1 |	0.12 +/- 0.02 |	1254.3 +/- 316.17 |
|	XGBoost Regressor |	7053.23 +/- 594.13 |	0.95 +/- 0.0 |	7724.0 +/- 695.19 |

Com base nas métricas de desempenho e considerando outros fatores, como o tempo de processamento, foi tomada a decisão de escolher o modelo XGBoost. Apesar do tempo de processamento menor em comparação ao Random Forest, o XGBoost apresentou um desempenho aceitável e a possibilidade de ajustes significativos na etapa de Hyperparameter Fine Tuning para melhorar ainda mais sua performance. Além disso, a escolha do XGBoost também levou em consideração a redução de custos de processamento e armazenamento em nuvem.

# 3 - INSIGHTS E RESULTADOS

# 4 -  CONCLUSÃO
