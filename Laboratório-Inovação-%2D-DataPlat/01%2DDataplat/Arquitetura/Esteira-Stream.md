**![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-818fcbce-2d28-4401-a3bf-e95133ab7c0d.png)**

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

**- Stream AnaLytics**
**- Azure Function (App Function)**


Uma das ferramentas utilizadas é o Stream Analytics, que foi escolhido por sua facilidade de manutenção e implementação dos Pipelines.

A seguir imagem de arquitetura para Near Realtime e Realtime:

![image.png](/.attachments/image-0f4c9bee-9db0-43a5-a4d3-6b6fa5e7e1ec.png)