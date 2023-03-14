![Logo-grupo-ccr-Editado-v3.png](/.attachments/Logo-grupo-ccr-Editado-v3-c966143a-ebc6-4b44-9548-395e41aac6ab.png)
# Objetivo

Realizar a monitoramento das potências das subestações, aumentando a eficiência na atuação com o aumento da demanda.


- Implementar as práticas de manutenção sob condição para reduzir, de maneira pró ativa, os custos com manutenções corretivas na rede elétrica das subestações;
- Monitorar, de maneira proativa, o consumo de energia das subestações da linha 08 e 09;
- Dar subsídios para uma atuação mais rápida e ágil das equipes de manutenção.

# Critério de Aceitação
- Monitorar o consumo de energia das subestações da linha 08 e 09;

- Deverá ter um dashboard online com informações de consumo por subestação;

- A coleta de informações poderá ser individualmente por subestação, por meio de microcontroladores específicos para essa finalidade;

#Fases

- Criação de épicos e estórias para o projeto no Jira;
- Levantamento das fontes de dados e requisitos das informações;
- Levantamento de requisitos para ingestão de dados;
- Processamento das regras de negócio;
- Desenvolvimento da camada Informacional;
- Análise dos dados;
- Construção da camada  de visualização (interface);
- Desenvolvimento da camada de Documentação;

#Arquitetura


A comunicação com as subestações poderá ocorrer por meio de telefonia móvel.

_Figura 1 - Arquitetura proposta, primeira versão._
![image.png](/.attachments/image-b2496187-2213-4172-9226-e8f3fddaa63d.png)

_Figura 2 - Atualização da arquitetura com time Dataplat._
![Arquitetura_All-V3-Monitoria de Potência.jpg](/.attachments/Arquitetura_All-V3-Monitoria%20de%20Potência-d9d34b08-7f5b-4951-829d-4a5e1c088175.jpg)

_Feigura 3 - Particionamento dos Arquivos e ciclo dos dados._
![Arquitetura_All-V3-Stream Iot.jpg](/.attachments/Arquitetura_All-V3-Stream%20Iot-93b963c0-a20a-44bd-bb62-8f7fb4725d0a.jpg)

# Indicadores
Medir a eficácia e eficiência dos dados apurados nos primeiros meses de solução;
Medir a geração do valor apurado com os dados gerados pela solução;
Apurar a economia de custos na compra de ativos ao se antecipar ao reparo na manutenção;
Quantificar medidas proativas que geraram valor ao negócio.

#Entregáveis:
* Dashboards online com interface para análise dos dados;
* Relatório para consulta na camada informacional;
* Proposta para arquitetura do projeto;
* Entrega da Documentação;
* AS IS e TO BE;
* Entregar OKRs.

# Latência RealTime
Com o objetivo de menor latência e simplicidade do código, foi realizada uma POC com testes em algumas ferramentas como Stream Analytics. Os testes mostraram um tempo médio de 13 segundos, abaixo dos 20 segundos esperados.

