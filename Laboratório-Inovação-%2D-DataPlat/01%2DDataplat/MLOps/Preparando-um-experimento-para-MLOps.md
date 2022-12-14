# MLOps no Databricks

O Databricks tem um ambiente integrado de aprendizado de máquina de ponta a ponta que incorpora serviços gerenciados para rastreamento de experimentos, treinamento de modelos, desenvolvimento e gerenciamento de recursos e serviço de recursos e modelos. O diagrama mostra como os recursos do Databricks são mapeados para as etapas do processo de desenvolvimento e implantação do modelo.


<IMG  src="https://docs.databricks.com/_images/ml-diagram.png"  alt="Machine learning diagram"/>


Acesso direto à documentação do Databricks https://docs.databricks.com/machine-learning/index.html

Dentro do Databricks você pode:

- Treinar modelos manualmente ou com AutoML
- Rastrear parâmetros e modelos de treinamento usando experimentos com rastreamento MLflow
- Criar tabelas de recursos e acesse-as para treinamento e inferência de modelos
- Compartilhar, gerenciar e servir modelos usando o Model Registry

Você também tem acesso a todos os recursos do espaço de trabalho Databricks, como notebooks, clusters, trabalhos, dados, tabelas Delta, segurança e controles administrativos e assim por diante. Para obter mais informações, consulte o guia Databricks Data Science & Engineering.

Para aplicativos de aprendizado de máquina, Databricks recomenda usar um cluster executando *Databricks Runtime para Machine Learning*

# 1. Fluxo do processo no Databricks

<IMG src="https://lh5.googleusercontent.com/beqfvHrp3j213jliv7rLaOhRS9LY3q58Y9OcsoHGEUpa5W55nSZeRJ5IhlypgaFzrXU2tk3qSQrPzU1nwPgtR17k6fupB_cXQ0E4r4SxNJ6tiSGYWINNMZkv6Hru5tLzg8s1DVUBYxPv_1J4P41ZAAxMIM20gH5udpbm6Fk75Fix1sHWsOz0fU8UOOL2fw"  width="602"  height="255" style="margin-left:0px;margin-top:0px"/></SPAN></SPAN></B>


## 2. Atividades por função

<B style="font-weight:normal"  id="docs-internal-guid-3c095194-7fff-26e4-02ad-1e1fa8ea1578"><IMG  width="922px;"  height="510px;"  src="https://lh3.googleusercontent.com/uw9WapEgiD0hNQV-L5EblroRsviuflUstaChKfOn2qcsXQT6kOYKVkW4ldChnQ2vM-XjD1ueCw6y1GF2kXsqKz3b69y-zB3yhova_xvuZvL6oZsSsgRCPVkcrHxGreEXRgM68MZqV_LeCy2ucDeisYDCeUQmgDqfLbnSxqKP3XaP2V5-eCj8GsQ5xN0q4x6-a4I=nw"/></B>

### 2.1 Data Scientist
<B style="font-weight:normal"  id="docs-internal-guid-7e4c014b-7fff-c587-c0a7-79a3783a72bd"><IMG  width="95px;"  height="95px;"  src="https://lh6.googleusercontent.com/j5maxgCaGOtAE7jOfBjGQiRkf2Nt3C6_4q4DzyB1-erWrMBcM9qu0dJ7Fp61F4QZb5L7GPvSy71THw3FhDGSNzL5h9XB85lcW0X8uuVRfgACzuZ06SezxQxP2uQ5TzpLYm4IcUSare0MeHFL3B4kfzRcBA=nw"/></B>

- **Data Acquisition** Acessa as *Delta Tables* e/ou outras fontes de dadso para análise
- **Exploratory Data Analysis** para analisar os dados 
- **Feature Selection** elenca as features que vai submenter aos modelos  
- ***Model Training and Testing**  MLFlow permite toda a gestão dos experimentos 
- *** Produtos finais gerados ** notebooks Python, features e Model.


### 2.2 ML Engineer
<B style="font-weight:normal"  id="docs-internal-guid-59ec01df-7fff-49d7-100d-b211dcc2620f"><IMG  width="107px;"  height="102px;"  src="https://lh3.googleusercontent.com/erArDPjAc2KZDWhPg7bEBEtZuthKbernt73O4FvnJlMuDfPvx8ZO1qhGZIvwxA-itxnXbkRp--tTDK9663dCygZvs18QM6vFR9FzWrOesZUHeapBjL0w-Ugi9C0tZf3BQrMNtFGxNwcSgausLmcNDLKVPg=nw"/></B>


- **Feature Store** atua em paralelo com o Data Scientist para organizar as feature tables
- **Model Registry** faz a gestão dos modelos
- **Model Serving** efetua o deploy de forma que os modelos sejam servidos para inferência
- **Model Monitoring** acompanha a performance dos modelos em produção
- **ML Best Practices** auxilia os Data Scientists com as melhores práticas em MLOps

### 2.3 Data Engineers e Back-end developers

<B style="font-weight:normal"  id="docs-internal-guid-b2f1e3de-7fff-2ec9-4669-12a3cc33c02b"><IMG  width="108px;"  height="76px;"  src="https://lh5.googleusercontent.com/xHhXZu7d4aVXzlR1DE6BkzBUWa-39wwy82MXlps32JFF7BgWf1naPpo9gonzW5i09k9JwDRT2tCdEiqiPEmhx2OTr8itEaKTTnyYojXreLKDQuUBE3h23v6TqYIcSChFHWLZMUlQXIACSXqqptG5MoJJnA=nw"/></B>

- Consomem os modelos como serviços
- *Batch* efetua predições *batch* através da integração com Data Factory ou em fluxos de trabalho em Python
- *on-line* predições através de chamadas REST acionando modelos como APIs, Dockers ou Containers.



# 3. Adaptando um experimento "Data Science Tradicional" para esteira MLOps 

Conforme mencionamos anteriormente, em tempo de EDA e experimento, não é necessário que os Data Scientist sigam todas as técnicas e métodos da engenharia de software, porém uma vez que o experimento precise entrar em uma esteira de MLOps, será necessário efetuar o *"split"* dos notebooks em partes:

1. Data Prep
2. EDA
3. Featurization 
4. Model Training and Testing
5. Model Evaluation
6. Prediction
7. Monitoring

Desta maneira temos como efetuar a orquestração de todo o ciclo MLOps em qualquer um dos níveis de MLOPs (0, 1 e 2, há um tópico explicando cada um deles na Wiki)


# 3.1 Exemplos de notebooks para cada etapa

- Data prep https://adb-622288559698745.5.azuredatabricks.net/?o=622288559698745#notebook/3141394032348943/command/3141394032348944
- Featurization: https://adb-622288559698745.5.azuredatabricks.net/?o=622288559698745#notebook/3125591493654637/command/3125591493654638
- Model Training and Testing: https://adb-622288559698745.5.azuredatabricks.net/?o=622288559698745#notebook/1104689511647348/command/1104689511647349
- Model Evaluation: https://adb-622288559698745.5.azuredatabricks.net/?o=622288559698745#notebook/1736787210932943/command/1736787210932944
- Prediction *batch inference*: https://adb-622288559698745.5.azuredatabricks.net/?o=622288559698745#notebook/3317141850075417/command/3317141850075418



