<B style="font-weight:normal"  id="docs-internal-guid-31451edb-7fff-52de-65fc-0baa459b81d6"><IMG  width="723px;"  height="478px;"  src="https://lh4.googleusercontent.com/Qjq0Tdt_3LWi1_ldq03DHP7FEfC5dLOUBCwjGPIo-liPULYxhE2WbNRPQld4GC67ILbunDlUUXz86mKwu-vZVFP8HrNhioHkQf-kAhLf1qbtbMhoaZ3bENZu5dn5SZxkGNHac1P_UVuYlc_EkthHL3L4OB9WTQZosqfu-TVWuDRbAHE70FN6yhBEdp-3-fcX=nw"  alt="Linha do tempo"/></B>

# Etapas do ciclo de Machine Learning e #MLOps#

# 1.  Experimento de ciência de dados

Esta é a etapa em que o cientista de dados atua em um ciclo semelhante ao CRISP-DM que comentamos na parte dos conceitos

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

- Feature Store que é um database otimizado para armazenamento das *Features* que vão alimentar os modelos porque **Modelos Matémáticos consomem dados tratados estatisticamente e na sua grande maioria precisam ser normalizados ou transformados matematicamente para que os modelos os entendam**
- 