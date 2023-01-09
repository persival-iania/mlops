O nosso Datalake e composto de de 4 camadas landing, bronze, silver e gold subdivididos em SUAT, TOR e KCOR

Para a camada landing os dados vão ficar de forma de raw, ou seja, vamos manter uma cópia fiel dos dados de de acordo com origem, na camada bronze faremos o armazenamento dos dados deltas, na silver teremos os dados delta e transformados ja na camada gold o dado estará pronto para o consumo pela companhia  

![image.png](/.attachments/image-90831555-4f82-4b70-a1e4-89657bd5c14b.png)

Nossa repositório ja está conectado com o Git utilizando conceito de master e branch.

![image.png](/.attachments/image-f64b0d3e-02f1-4966-87d0-5d5d43e1448a.png)


