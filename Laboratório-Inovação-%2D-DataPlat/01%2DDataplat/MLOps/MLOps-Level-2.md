![DALL·E 2023-02-06 23.23.34 - Robots learning at school  digital art.png](/.attachments/DALL·E%202023-02-06%2023.23.34%20-%20Robots%20learning%20at%20school%20%20digital%20art-f8a29807-6f6f-485b-ae16-e84fb95c84fe.png)

# Nível de Maturidade MLOps

Reconhecemos 3 níveis de maturidade aqui na CCR:

- *Level 0* **Manual Pipelines** todas as etapas do ciclo são executadas, porém manualmente
- *Level 1* **Continuous Trainning** pipeline evolui para treinamento dos modelos de forma contínua
- *Level 2* **Continuous Deployment** pipeline evolui para CI/CD+ Continuous Training


# Level 0:  Manual Pipelines

<B style="font-weight:normal"  id="docs-internal-guid-2191a15a-7fff-fcac-a560-ab2fc816c325"><IMG  width="895px;"  height="361px;"  src="https://lh5.googleusercontent.com/43kY2uvIxCZS7LJWpMyOG4DNQ-rEb8s8rOCtbp0VdJ1OXfRQJVQfL5MXo62ngkuAAM9FLfUMD2C_rezH07JNU9OhLL13JOAiBiVgczZpNB37Vx8_nKESVqZeO4YpcYxVMLMWUoWcw5ZWIcLB4xFVuReI_Ee3n_YhztyZd1uBlWlBK1ime8QCzVrZtfCaOVZ1=nw"/></B>

Fonte de referência no Medium: https://towardsdatascience.com/mlops-level-0-manual-pipelines-7278b9949e59


# Level 1:  Continuous Trainning

<B style="font-weight:normal"  id="docs-internal-guid-45ea7c10-7fff-1445-31bd-5ace1ca8b736"><IMG  width="775px;"  height="434px;"  src="https://lh5.googleusercontent.com/Ltbw-JuDrXYhItvo2r2ES8qHjGfysu6E7Y2iYkVdmvns5lQWXdiVQeiEiC4u0IqcPRpf517He5v52Th52ZmbllA9aTrBxI4ceSFAiXmzsa-UutR1NtoJ6nyP4UQrOznAT2ENyZ2NkcQj6CsCAQ0NRctFGnKd41-MJqlpHZKI0cGaj2agFQI66NNvh5MwmOQe=nw"/></B>


Fonte de referência no Medium: https://towardsdatascience.com/mlops-level-1-continuous-training-b2a633e27d47

# Level 2:  Continuous Deployment 
### CI/CD + Continuous training

<B style="font-weight:normal"  id="docs-internal-guid-b38f8c24-7fff-593b-83fd-0a2532b87b04"><IMG  width="832px;"  height="434px;"  src="https://lh3.googleusercontent.com/_bhMJpTmKEPK_ae1POUfjC8iJYQ2aDqsSiLfsGUkUUPS9PY7nLBOVqmvl8SvMzL8iJBwGrJGkiHI-bK6gnoMlxG9luSOD_81JGC4QgQERplkB39BYdFtRmJCi6vEw0KX1h8Imm7FsVwm5DD4vGHZkdtzAEAskwI81-RDBMu6m_34AnE2Nliy86U9n6jWrLBL=nw"/></B>

Fonte de referência no Medium: https://towardsdatascience.com/mlops-level-2-ci-cd-continous-training-b9b64042368


# Funcionalidades novas MLOps Nível 2


O nível 2 do MLOps permite atualizações rápidas e confiáveis para pipelines em produção, bem como outros ambientes, usando CI/CD automatizado. 

A automação do pipeline por um sistema automatizado de CI/CD permite a implementação rápida de novas ideias e experimentos, ao mesmo tempo em que constrói, testa e implanta automaticamente os novos artefatos e componentes do pipeline no ambiente de destino apropriado

# Características do MLOps nível 2

Os componentes que compõem o nível 2 do MLOps são muito semelhantes aos do nível 1 do MLOps. A diferença está na adição de

- Testar e Construir serviços (Integração Contínua).
- Serviços de implantação (implantação contínua).
- Orquestração de pipeline.
- O pipeline pode ser dividido em 6 etapas:

## Desenvolvimento e experimentação. 

1. É aqui que diferentes algoritmos e técnicas de modelagem são experimentados e cada etapa do experimento é orquestrada. A saída final do estágio 1 é o código-fonte das etapas do pipeline que é enviado para um repositório de código.

1. Integração Contínua de pipeline. Depois que o código é enviado para um repositório de código, ele aciona um pipeline de teste e cria os componentes necessários (pacotes, artefatos etc.) que precisam ser implantados em um estágio posterior.

1. Entrega contínua de pipeline. Os artefatos produzidos no estágio 2 são implantados no ambiente de destino. A saída deste estágio é um pipeline implantado com a nova implementação do modelo do estágio 1.

1. Acionamento automatizado. A execução do pipeline na produção é acionada automaticamente com base em um cronograma ou em resposta a um acionador de evento. A saída final deste estágio é um modelo treinado que é enviado para um registro de modelo.

1. Entrega Contínua do modelo. O modelo treinado final é implantado como um serviço no qual os aplicativos podem obter previsões do modelo. A saída final deste estágio é um serviço de predição de modelo implantado.

1. Monitoramento de modelo. O modelo em produção é monitorado ao vivo por meio da coleta de estatísticas do desempenho do modelo. Quando o modelo se desvia ou se deteriora de um limite aceitável, esse estágio deve acionar uma execução do pipeline em produção para treinar novamente o modelo usando novos dados ou executar um novo pipeline de experimento.