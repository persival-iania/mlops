#ML está em todo lugar, mas frequentemente falha em produção 

![Captura de Tela 2023-01-24 às 17.39.45.png](/.attachments/Captura%20de%20Tela%202023-01-24%20às%2017.39.45-92f3b266-45b6-4a79-a165-6ec12d876928.png)

Fonte:
https://www.datanami.com/2020/10/01/most-data-science-projects-fail-but-yours-doesnt-have-to/

#Por que projetos de ML falham em produção?
### Resposta: Negligenciar a manutenção: Falta de retreinamento e testes

![Captura de Tela 2023-01-24 às 17.41.17.png](/.attachments/Captura%20de%20Tela%202023-01-24%20às%2017.41.17-8c24b3a5-7f45-43a0-83b4-afb69e749c06.png)

Fonte:
https://databricks.com/blog/2019/09/18/productionizing-machine-learning-from-deployment-to-drift-detection.html


#Vamos nos concentrar em duas questões:

![Captura de Tela 2023-01-24 às 21.21.51.png](/.attachments/Captura%20de%20Tela%202023-01-24%20às%2021.21.51-0eb06ec3-e548-4696-b413-2730688abda2.png)


#Ciclo de vida de MLOps

<IMG  src="https://learn.microsoft.com/en-us/azure/architecture/example-scenario/mlops/media/data-sciene-lifecycle-model-flow.png"  alt="data science lifecycle model process flow"/>

#A implantação do modelo nunca é o fim do processo
##**É o início da medição e monitoramento do modelo**

As distribuições de dados e os tipos de recursos podem mudar ao longo do tempo devido a:

![Captura de Tela 2023-01-24 às 21.26.57.png](/.attachments/Captura%20de%20Tela%202023-01-24%20às%2021.26.57-2f2b5d79-2f29-42ff-83cf-654d98cd31e6.png)

#**Os modelos se degradam com o tempo** 

#**Desafio: Identificar o quanto antes**


#DRIFTs mais comuns

![Captura de Tela 2023-01-24 às 21.28.42.png](/.attachments/Captura%20de%20Tela%202023-01-24%20às%2021.28.42-8e784302-d17d-489c-b74c-46e47e25a358.png)


#Feature, Label, and Prediction Drift

<B style="font-weight:normal"  id="docs-internal-guid-054e26d5-7fff-abbb-2577-4d39d3206cf5"><IMG  width="377px;"  height="172px;"  src="https://lh3.googleusercontent.com/dWvtd8E2yZDsryyy51BsMUaN_Tu8368aihycs3BFv5nBCHGbeUQRjNJI6lssliMs_EXUScBGHL7gdrPP2aD5bT21dSN21aN8wcpS-hJQUXT_IixG7R1tBK_RFO52pud-e560cZF_e1nI5y4Ajyc-wsg42Bi3rIHrun3Vz4aFlkgQHy4wZFl65fZfeS9EoguTUsJFKYLcgA=nw"/></B>

<B style="font-weight:normal"  id="docs-internal-guid-12006264-7fff-e341-e801-99ec033b9d43"><IMG  width="443px;"  height="182px;"  src="https://lh4.googleusercontent.com/qi2Bx-kuQb89iCWqV88QIH-bwQSQcmOKjr8r2YNRixCehevOakEqootv5YmgqXkbQv3s8bYpzn3EpyP02FOBCkpZ0E-yid8Ig3eaVQC3fEg-6lSvv73_DNk_t_9tJJPnqVj3eZqolg7fuRrDkc4CgxrDahe-kgWQMvCKYcCodlhwyy--eLraNcc-0yNtNRUKdxmabsfyZA=nw"/></B>

Referências
https://dataz4s.com/statistics/chi-square-test/
https://towardsdatascience.com/machine-learning-in-production-why-you-should-care-about-data-and-concept-drift-d96d0bc907fb

#**Concept drift**

<B style="font-weight:normal"  id="docs-internal-guid-690c4529-7fff-e745-0674-0da8d55b6501"><IMG  width="701px;"  height="305px;"  src="https://lh6.googleusercontent.com/COSoXi6naxqVhW6mEeWfK1LDfxfMEl4lK1doIJuMx1iw78N0Fvvp1jTr-x6HNwG47O_v-thSmgXS4qJstOvpUa1awb5c1DQZz8f1O3doq_1ZpxQp7DgBCMHJZxdRfIWMOD7dz56QyqMdiYWJQYxedRAnamDBr6HwvHXEH-UXArfiwbhSpEa-MIaxTxVAyu0w8vNbBdjouw=nw"/></B>

Source: 
Krawczyk and Cano 2018. Online Ensemble Learning for Drifting and Noisy Data Streams

#** Ações a serem tomadas por tipo de DRIFT**

![Captura de Tela 2023-01-24 às 21.32.55.png](/.attachments/Captura%20de%20Tela%202023-01-24%20às%2021.32.55-07953c0d-103e-4584-be2a-f57bcecbc09f.png)







