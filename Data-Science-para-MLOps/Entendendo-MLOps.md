# Etapas do ciclo de Machine Learning e **MLOps**

# 1.  Experimento de ciência de dados

Esta é a etapa em que o cientista de dados atua em um ciclo semelhante ao CRISP-DM que comentamos anteriormente, com base no CRISP-DM

<IMG  src="https://www.datascience-pm.com/wp-content/uploads/2021/02/CRISP-DM.png"  alt="CRISP DM"/>


Para mais informações sobre o CRISP-DM veja: [https://www.datascience-pm.com/crisp-dm-2/]()


Em linhas gerais, o cientista de dados nesta etapa faz:
- Entende o problema ou oportunidade que a empresa quer resolver através de **Data Science**
- Com base na área de domínio do experimento identifica os dados que podem ser usados no experimento
- Efetua EDA (Exploratory Data Analysis ou Análise Exploratória de Dados), onde analisa todos os dados que podem efetivamente contribuir no modelo a ser gerado, ou seja, vai fazer a **Seleção de Features** que irão alimentar os modelos
- Com as conclusões obtidas do EDA e as **features** que podem ser usadas nos modelos, vai submeter estes dados a diversos modelos matemáticos e procurar o que tem a melhor resposta.
- Efetua o treino e teste dos modelos, através de dos métodos de **Machine Learning** 
- Valida os modelos através das métricas matemáticas de avaliação e performance e escolhe o modelo com as melhores métricas
- Efetua o deploy do modelo

Normalmente o ciclo é recursivo, pois os modelos vão evoluindo.

# 2. Experimento vs MLOps

Cientistas de dados durante a fase de experimentos não tem necessidade de seguirem à risca métodos de engenharia de software, pois o foco é na análise de dados através de métodos estatísticos e matemáticos, porém para efeito de esteira, temos alguns componentes adicionais.

- **Feature Store** que é um database otimizado para armazenamento das *Features* que vão alimentar os modelos porque **Modelos Matémáticos consomem dados tratados estatisticamente e na sua grande maioria precisam ser normalizados ou transformados matematicamente para que os modelos os entendam**
- **Registro das métricas dos experimentos** conforme comentamos anteriormente, o cientista de dados faz diversos experimentos com diversos modelos, coleta as métricas de avaliação dos modelos e em MLOps gravamos todas as métricas de cada experimento
- **Model Registry** é um repositório que vai governar e versionar os modelos, dados de treino, parâmetros, os **"artifacts"** além de permitir que o modelo seja servido para inferência de forma batch ou on-line como uma API ou um container. 

<B style="font-weight:normal"  id="docs-internal-guid-31451edb-7fff-52de-65fc-0baa459b81d6"><IMG  width="723px;"  height="478px;"  src="https://lh4.googleusercontent.com/Qjq0Tdt_3LWi1_ldq03DHP7FEfC5dLOUBCwjGPIo-liPULYxhE2WbNRPQld4GC67ILbunDlUUXz86mKwu-vZVFP8HrNhioHkQf-kAhLf1qbtbMhoaZ3bENZu5dn5SZxkGNHac1P_UVuYlc_EkthHL3L4OB9WTQZosqfu-TVWuDRbAHE70FN6yhBEdp-3-fcX=nw"  alt="Linha do tempo"/></B>

# 3. Adequando um experimento para aderência ao ciclo MLOps

Sendo MLOps uma *esteira** e segue um fluxo de processos, o experimento precisa ser desmembrado nas seguintes etapas:

- **Criação da Feature Store** as features identificadas na fase de EDA pelo cientista passam por um processo de **Feature Engineering* e são persistidas em **Feature Tables**
- **Model Training and Testing** o treino e teste dos modelos é feito a partir da **Feature Store** e as métricas são coletadas
- **Model Evaluation** cientista analisa as métricas de avaliação dos modelos e seleciona o **melhor modelo** para deploy
- **Model Registry** engenheiro de Machine Learning registra o modelo e prepara-o para ser servido para inferências
- **Model Serving** engenheiro de Machine Learning providencia o **Deploy** do modelo que pode ser servido de forma batch ou on-line.
- **Model Monitoring** as métricas de performance do modelo precisam ser acompanhadas para verificar se o modelo necessita ser re-treinado.


# 4. Arquitetura MLOps baseada em **MLFLow**

<B style="font-weight:normal"  id="docs-internal-guid-034922d5-7fff-c249-ec0c-dab0e2e87026"><IMG  width="960px;"  height="504px;"  src="https://lh6.googleusercontent.com/OZdoaxYvMQiu_cLNguQZxIL9hZnj5lOKvS2w2Vhp89wl2NCECxScqvm2VB6hNhTxcUOmRupJlkB8kxSCCfvJD-9HyZJyStTaTfCIWVAXp9qSacJB-7pwtKNkbW-wolKUIugE0JgaYVlPq0hIUA_t6UFZlgLywjJXnt2jny08DicyRbQyVcbRGa2ODHSM2k--=nw"/></B>

**MLFLow** é um framework *open source* criado pela *Databricks* que no nosso caso já é totalmente gerenciado na Azure e permite a toda a governança do ciclo **MLOPs** em todas as etapas, mais informações em [https://mlflow.org/docs/latest/index.html]()

# 5. MLFlow gerenciado pelo Azure Databricks

A versão do MLFlow que iremos utilizar já está totalmente gerenciada dentro do Azure Databricks, o que nos permite:

- Acompanhamento: Permite que você acompanhe experimentos para registrar e comparar parâmetros e resultados:
- Modelos: Permitem que você gerencie e implante modelos de uma variedade de bibliotecas de - ML para uma variedade de plataformas de serviço e inferência de modelos.
- Projetos: Permite que você empacote o código ML em um formulário reutilizável e reproduzível para compartilhar com outros cientistas de dados ou transferir para produção.
- Registro de Modelos: permite centralizar um repositório de modelos para gerenciar transições completas de fase do ciclo de vida dos modelos: do preparo à produção, com recursos para controle de versão e anotação.
- Serviço de Modelo: permite hospedar Modelos de MLflow como pontos de extremidade REST.

Veja: https://learn.microsoft.com/pt-br/azure/databricks/mlflow/

# 6. Como fica todo um fluxo de MLOps dentro de uma squad de dados?

![Captura de Tela 2022-12-14 às 19.28.30.png](/.attachments/Captura%20de%20Tela%202022-12-14%20às%2019.28.30-dae6ba6d-86b7-4634-8440-114bbcca9974.png)


