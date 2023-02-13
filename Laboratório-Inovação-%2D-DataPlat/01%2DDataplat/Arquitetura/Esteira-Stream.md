**![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-818fcbce-2d28-4401-a3bf-e95133ab7c0d.png)**


#Conceito de Stream

Nesse documento, estão descritas quais ferramentas compõem a esteira **Near Real Time** e **Real time**.  São esteiras para atender à necessidade monitoramento de IoT, input de dados Stream e CDC. São duas esteiras em uma, Real Time e Near Real Time.  A seguir algumas diferenças entre elas para melhor entendimento.

**Real Time** 
Quando você precisa de informações processadas imediatamente (Como monitoria de Iot com latência de poucos segundos). 

**Near Real Time**
Quando a velocidade é importante, mas você não precisa dela imediatamente (como produzir inteligência operacional). Esse processamento é quando a velocidade é importante, mas o tempo de processamento em minutos é aceitável em vez de segundos.

Ferramentas utulizadas:

**- IoTHub**: A IoT (Internet das Coisas) é uma rede de dispositivos físicos que se conectam e trocam dados com outros dispositivos e serviços pela Internet ou por outra rede. Atualmente, há mais de 10 bilhões de dispositivos conectados no mundo, e todos os anos são adicionados ainda mais dispositivos. Qualquer coisa que ter sensores inseridos e os softwares necessários pode ser conectada pela Internet.

O Hub IoT pode ser dimensionado para milhões de dispositivos conectados simultaneamente, além de milhões de eventos por segundo para dar suporte a suas cargas de trabalho de IoT.
O Hub IoT do Azure é um serviço gerenciado hospedado na nuvem que atua como um hub central de mensagens para comunicação entre um aplicativo de IoT e os dispositivos anexados a ele. Você pode conectar milhões de dispositivos e suas soluções de back-end de maneira confiável e segura. Quase todos os dispositivos podem ser conectados a um hub IoT.

_Figura 1- A imagem a seguir aponta um exemplo de configuração e aplicação para um IoT. Uma placa para configurada para acesso ao IotHub envia mensagens que poderá ter gatilhos de alertas , seja para e-mail da CCR seja para mensagens como no Teams._
![image_0.png](/.attachments/image_0-457304ce-8668-411b-9625-5c63a0258885.png)

**- Azure Stream AnaLytics**: O Azure Stream Analytics é um mecanismo de processamento de fluxo totalmente gerenciado que foi projetado para analisar e processar grandes volumes de dados de streaming com latências de sub-milissegundos. Padrões e relações podem ser identificados em dados originados de uma variedade de fontes de entrada, incluindo aplicativos, dispositivos, sensores, sequências de cliques e feeds de mídias sociais. Esses padrões podem ser usados para disparar ações e iniciar fluxos de trabalho, como criação de alertas, informações de feed para uma ferramenta de relatórios ou para armazenar dados transformados para uso posterior. O Stream Analytics também está disponível no runtime do Azure IoT Edge, permitindo o processamento direto de dados em dispositivos IoT.

Os cenários a seguir são exemplos de quando você pode usar o Azure Stream Analytics:

- Pipeline de ETL de streaming para o Armazenamento do Azure no formato Parquet
Aplicativos controlados por eventos com o Banco de Dados SQL do Azure e o Azure Cosmos DB
- Analisar fluxos e logs de telemetria em tempo real de aplicativos e dispositivos IoT
- Painel em tempo real com o Power BI
- Detecção de anomalias para detectar picos, quedas e alterações positivas e negativas lentas nos valores do sensor
- Análise geoespacial para gerenciamento de frotas e veículos sem motoristas
- Monitoramento remoto e manutenção preditiva de ativos de alto valor
- Análise de sequência de cliques para determinar o comportamento do cliente

**- Azure Function (App Function)**: O Azure Functions é um serviço de nuvem disponível sob demanda que fornece toda a infraestrutura e os recursos continuamente atualizados necessários para executar os aplicativos. Você se concentra no código que mais importa para você, na linguagem mais produtiva para você, e o Functions manipula o restante.

#O porquê da escolha no ambiente CCR
O Stream Analytics foi escolhido por sua facilidade de manutenção e implementação dos Pipelines em relação a outras ferramentas como o Databricks. Seu custo será observado para garantia de escolha de melhor custo e benefício. 

Existem na CCR muitos projetos de Iot. A seguir alguns deles:

- Escada Rolante
- Elevadores
- Monitoria 
- Subestações de trens

Esses projetos estão detalhados em uma página específica da Wiki. Para saber mais acesse: Link

#Diagrama de Arquitetura

A seguir imagem de arquitetura para Near Realtime e Realtime:

![image.png](/.attachments/image-0f4c9bee-9db0-43a5-a4d3-6b6fa5e7e1ec.png)