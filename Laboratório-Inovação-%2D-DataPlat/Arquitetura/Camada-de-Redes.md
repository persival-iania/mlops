![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-818fcbce-2d28-4401-a3bf-e95133ab7c0d.png)

Esse manual visa elucidar pontos referente as camadas de rede. Entre os principais pontos abordados estão: VNET, SUBNET, VPN, inbound e outbound para liberação no Firewall.

# Vnet


A Vnet foi dividida em 3 ambientes, Desenvolvimento, Qualidade e Produção. Contudo, por recomendação do time de TI CCR foi alterado para desenvolvimento e produção.

As conexões ocorrerão diramente no Oracle Active Data Guard do site seguindo pré requisitos do CDC.  Devido dificuldade e cuidado com link poderá haver um segundo cenário temporário. Nele é usado a Sub-PRD com uma única Vnet para os três ambientes. A seguir figura que ajudará no entendimento:

_Figura 1 - Estrutura de VNET recomendada. Conectada por VPN da CCR._
![01-Camadas de Rede Permanente.jpg](/.attachments/01-Camadas%20de%20Rede%20Permanente-0948397e-b384-4d81-9795-de0c53274db3.jpg)

_Figura 2 - Estrutura temporária para agilizar primeira ingestão:_
![01-Camadas de Rede.jpg](/.attachments/01-Camadas%20de%20Rede-aeba8586-4106-4dab-b721-857a57c5aac2.jpg)


# Subnet
As subnets foram préviamente definidas, mas serão detalhadas conforme evolução das definições dos cenários. Mascaramento das subnets devem permancecer os mesmos.
## Sub-Dev
As subnets foram divididas da seguinte forma:
![image.png](/.attachments/image-ec4998d6-3a9f-41d5-8048-89b4f01c8b65.png)

## Sub-PRD
![image.png](/.attachments/image-a7bcf20a-44e2-4b20-b2f4-f46be0d0ad3c.png)

Em anexo planilha produtos das imagens supracitadas:
[CamadasDeRede.xlsx](/.attachments/CamadasDeRede-4f4c3e64-1621-42f0-9125-cb8b8a98624b.xlsx)

A conexão ocorrerá por VPN em cada site de rodovias por limitações de conexão.

**_OBS: Poderão haver alterações no processo e padrões tendo em vista estarmos em fase de desenvolvimento._** 