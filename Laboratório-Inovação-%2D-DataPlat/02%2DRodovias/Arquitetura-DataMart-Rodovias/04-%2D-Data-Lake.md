(/.attachments/Captura%20de%20Tela%202023-01-09%20às%2012.39.06-3bcee43f-57c1-43eb-875e-645c6075ddf9.png)O a estrutura do Datalake é composta de 4 camadas landing, bronze, silver e gold subdivididos em SUAT, TOR e KCOR e com um arquivo de configuração para cada objeto\tabela dentro dele. 

![Captura de Tela 2023-01-09 às 12.39.06.png](/.attachments/Captura%20de%20Tela%202023-01-09%20às%2012.39.06-0b560f91-bab2-4a1b-8fe2-501d40764630.png)

Para a camada landing os dados vão ficar de forma de raw, ou seja, vamos manter uma cópia fiel dos dados de de acordo com origem, na camada bronze faremos o armazenamento dos dados deltas, na silver teremos os dados delta e transformados ja na camada gold o dado estará pronto para o consumo pela companhia  

![image.png](/.attachments/image-90831555-4f82-4b70-a1e4-89657bd5c14b.png)





