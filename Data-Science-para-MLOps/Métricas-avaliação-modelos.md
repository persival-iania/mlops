#Principais métricas usadas para avaliação de Modelos

#**CLASSIFICAÇÃO**

Existem várias métricas comuns usadas para avaliar modelos de classificação de aprendizado de máquina. Algumas das mais comuns incluem:

- Acurácia: A acurácia é a proporção de previsões corretas feitas pelo modelo em relação ao total de previsões feitas. Ela é fácil de entender e interpretar, mas pode ser enganosa se a classe alvo tiver uma distribuição desbalanceada.

- Matriz de Confusão: Uma matriz de confusão mostra a quantidade de previsões corretas e incorretas feitas pelo modelo para cada classe. Ela fornece uma visão detalhada do desempenho do modelo, mas pode ser difícil de interpretar para problemas de classificação com muitas classes.

- Precisão: A precisão é a proporção de previsões corretas positivas em relação ao total de previsões positivas. Ele mede quão bem o modelo identifica verdadeiros positivos.

- Recall ou Sensibilidade: O recall é a proporção de previsões corretas positivas em relação ao total de verdadeiros positivos. Ele mede quão bem o modelo encontra todos os exemplos positivos.

- F1-Score: O F1-Score é a média harmônica entre precisão e recall. Ele é útil quando precisão e recall são ambos importantes e equilibrar entre eles é importante.

- AUC-ROC: AUC-ROC é a área sob a curva ROC. Ele mede a capacidade do modelo de discriminar entre classes.

- Log Loss: Log Loss é a medida de quão bem o modelo prevê as probabilidades das classes. É usado quando o modelo tem a capacidade de produzir probabilidades de classificação.

Cada uma dessas métricas tem suas próprias vantagens e desvantagens, e a escolha de qual usar dependerá do problema específico e do que é importante para o seu objetivo.



#**REGRESSÃO**


- Erro Quadrático Médio (MSE - Mean Squared Error): MSE é a média dos erros ao quadrado entre as previsões do modelo e os valores reais. Ele é fácil de calcular e interpretar, mas pode ser sensível a outliers.

- Erro Absoluto Médio (MAE - Mean Absolute Error): MAE é a média dos erros absolutos entre as previsões do modelo e os valores reais. Ele é menos sensível a outliers do que o MSE.

- Raíz do Erro Quadrático Médio (RMSE - Root Mean Squared Error): RMSE é a raiz quadrada do MSE. Ele tem as mesmas propriedades que o MSE, mas as unidades de medida são os mesmos que os dados de treinamento.

- R-Quadrado (R² - Coefficient of determination): R² é uma medida de quão bem o modelo se ajusta aos dados. Ele varia entre 0 e 1, onde 1 indica um ajuste perfeito.

- Mediana do Erro Absoluto (MedAE - Median Absolute Error): MedAE é a mediana dos erros absolutos entre as previsões do modelo e os valores reais. Ele é menos sensível a outliers do que o MAE.

- Resíduos: os resíduos são a diferença entre os valores previstos e os valores observados. É possível plotar esses resíduos para verificar se eles seguem uma distribuição normal e se eles são homocedásticos.


#**FORECAST**

Modelos de forecast possuem muitas métricas semelhantes aos modelos de regressão, porém com algumas métricas adicionais

- Erro Quadrático Médio (MSE - Mean Squared Error): MSE é a média dos erros ao quadrado entre as previsões do modelo e os valores reais. Ele é fácil de calcular e interpretar, mas pode ser sensível a outliers.

- Erro Absoluto Médio (MAE - Mean Absolute Error): MAE é a média dos erros absolutos entre as previsões do modelo e os valores reais. Ele é menos sensível a outliers do que o MSE.

- Raíz do Erro Quadrático Médio (RMSE - Root Mean Squared Error): RMSE é a raiz quadrada do MSE. Ele tem as mesmas propriedades que o MSE, mas as unidades de medida são os mesmos que os dados de treinamento.

- Mediana do Erro Absoluto (MedAE - Median Absolute Error): MedAE é a mediana dos erros absolutos entre as previsões do modelo e os valores reais. Ele é menos sensível a outliers do que o MAE.

- Symmetric mean absolute percentage error (SMAPE): Ele mede a porcentagem de erro absoluto médio relativo, é utilizado para séries temporais.

- Coeficiente de Determinação (R² - Coefficient of determination): R² é uma medida de quão bem o modelo se ajusta aos dados. Ele varia entre 0 e 1, onde 1 indica um ajuste perfeito.

- logarithmic loss (logloss) : mede a precisão das probabilidades, utilizado quando o modelo produz probabilidades de previsão, geralmente utilizado em problemas de classificação binaria

- Índice de Previsão (PI - Prediction Interval): O PI é uma medida de incerteza na previsão do modelo, geralmente expressa como uma faixa de previsão (por exemplo, 95% de confiança). Ele é útil para avaliar a robustez do modelo e para tomar decisões com base na incerteza.

- Índice de Acurácia (AC - Accuracy): O AC é a proporção de previsões corretas do modelo em relação ao total de previsões. Ele é útil para avaliar a precisão geral do modelo, mas pode ser enganoso se houver desequilíbrio de classes nos dados.

- Índice de Previsão de Classe (CP - Class Prediction Index): O CP é a proporção de previsões corretas para cada classe específica. Ele é útil para avaliar a precisão do modelo para cada classe e para identificar quais classes o modelo tem dificuldade em prever.

Cada uma dessas métricas tem suas próprias vantagens e desvantagens, e a escolha de qual usar dependerá do problema específico e do que é importante para o seu objetivo. Algumas métricas são mais adequadas para problemas de séries temporais, enquanto outras são mais adequadas para problemas de classificação ou regressão. Em alguns casos, pode ser útil usar mais de uma métrica para obter uma visão mais completa do desempenho do modelo.



#**CLUSTERING**


- Medida de Silhueta: A medida de silhueta é uma medida de quanto similar um ponto é aos outros pontos dentro de sua própria classe versus aos pontos em outra classe. Ela varia entre -1 e 1, onde valores maiores são melhores.

- Coeficiente de Davies-Bouldin: O coeficiente de Davies-Bouldin mede a similaridade entre cada classe e suas vizinhas mais próximas. Ele varia entre 0 e infinito, onde valores menores são melhores.

- Coeficiente de V-measure: O coeficiente de V-measure é uma medida harmônica entre precisão e recall para avaliar o desempenho de agrupamento. Ele varia entre 0 e 1, onde valores maiores são melhores.

- Índice de Rand: O índice de Rand é uma medida de similaridade entre duas estruturas de agrupamento, geralmente entre a estrutura de agrupamento gerada pelo algoritmo e a estrutura de agrupamento verdadeira. Ele varia entre 0 e 1, onde valores maiores são melhores.

- Método de Elbow: O método de elbow é um método gráfico para determinar o número ótimo de clusters a serem usados. Ele se base no gráfico do erro quadrático total versus o número de clusters.

- Índice Calinski-Harabasz: O índice Calinski-Harabasz é uma métrica que mede a relação entre a variância dentro de um cluster e a variância entre clusters. Quanto maior for o valor do índice, melhor é o agrupamento.



