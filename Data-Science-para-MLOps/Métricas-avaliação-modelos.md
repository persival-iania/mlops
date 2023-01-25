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



#Regressão

* Erro médio absoluto (MAE): é a média dos erros absolutos entre as previsões e os valores reais. Ele fornece uma medida da magnitude do erro, mas não considera a direção do erro. Imagine que você está tentando prever o preço de uma casa e seu modelo prevê um valor de $500.000 quando o preço real é $450.000. O erro absoluto seria $50.000. Se você fizer isso para várias casas, o MAE seria a média dos erros absolutos desses casos.

* Erro médio quadrático (MSE): é a média dos erros ao quadrado entre as previsões e os valores reais. Ele fornece uma medida da magnitude do erro, dando mais peso para erros maiores. Ele é frequentemente usado para avaliar a qualidade de um modelo de regressão. Imagine que você está jogando uma bola para uma cesta e seu modelo prevê que a bola vai cair a 1 metro à esquerda da cesta, mas na verdade ela cai a 1 metro à direita da cesta. O erro quadrático seria 1^2 = 1. Se você fizer isso para várias bolas, o MSE seria a média dos erros quadráticos desses casos.

* Raiz do erro médio quadrático (RMSE): é a raiz quadrada do MSE. Ele fornece a mesma informação que o MSE, mas ao invés de estar no espaço de erros ao quadrado, ele está no espaço de erros. Imagine que você está medindo a distância entre dois pontos e o seu modelo prevê que a distância é de 1 metro, mas na verdade é de 1,41 metros. O RMSE seria a raiz quadrada de 1,41^2 = 1,41 metros.

* Coeficiente de determinação (R²): é uma medida de quão bem o modelo se ajusta aos dados. Ele varia entre 0 e 1, onde 1 indica que o modelo explica completamente a variabilidade dos dados e 0 indica que o modelo não explica a variabilidade dos dados. Imagine que você está tentando prever o preço de uma casa com base em sua área. Se o seu modelo prevê o preço com precisão, então R² seria próximo de 1. Se o seu modelo não tem nenhuma relação com o preço da casa, então R² seria próximo de 0.