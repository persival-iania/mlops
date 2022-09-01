![ccr.png](/.attachments/ccr-2b22bf34-55cc-4ec1-898e-058e4f44259c.png)                                ![terraform.png](/.attachments/terraform-c1363d8b-397f-4030-a388-1ece33a1fe7a.png)
# Introdução

Como política de implantação seguindo o modelo de Infraestrutura como um código ( IaaC ). Foi adotado o uso do terraform como plataforma de implantação dos recursos de nuvem do Lab-Dataplat.

## O Terraform

Seguindo a documentação do Terraform, temos:

> HashiCorp Terraform is an infrastructure as code tool that lets you define both cloud and on-prem resources in human-readable configuration files that you can version, reuse, and share. You can then use a consistent workflow to provision and manage all of your infrastructure throughout its lifecycle. Terraform can manage low-level components like compute, storage, and networking resources, as well as high-level components like DNS entries and SaaS features.
> --<cite>https://www.terraform.io/intro#what-is-terraform</cite>

## Por que terraform ?

Atualmente o terraform é uma das ferramentas de IaaC mais utilizadas no mundo:
- Github Stats: 
  - Fork: 7.4K
  - Star: 31.7K


Seguindo o portal [Bluelight](https://bluelight.co/blog/best-infrastructure-as-code-tools), temos a seguinte classificação:

| Plataform | Number | 
| --------- | ------- | 
| Terraform |     1   | 
| AWS Cloud Formation | 2 | 
| Azure Resource Manager | 3 | 
| Google Cloud Deployment Manager | 4
| Pulumi | 5 | 
| Ansible |6 | 
| Chef| 7 | 
| Puppet | 8 | 
| Crossplane | 9 | 
| Vagrant | 10 | 


## Infrastructure as a Code - IaaC

Para começar a entender o conceito de IaaC, primeiro é preciso tratar da cultura DevOps, que tomou conta das empresas mundo afora. Ao implantar cultura DevOps, as empresas buscam simplificar processos com a finalidade de alcançar os melhores resultados de forma mais ágil. Essa metodologia surgiu da necessidade de integrar os times de desenvolvimento e de operação, trazendo consigo um conjunto de estratégias aplicadas com a finalidade de solucionar problemas e otimizar os processos para desenvolver projetos com maior velocidade e qualidade. Trazendo o foco no cumprimento de tarefas, e no modelo de responsabilidade compartilhada dentro da equipe, a cultura DevOps tem a capacidade de aumentar os esforços na otimização de processos, além de desenvolver um fluxo de trabalho mais seguro, eficiente e rápido. E o conceito de Infrastructure as a Code (IaaC), tem muita relação com a cultura DevOps.

## Benefícios da IaaC
Agilidade: A capacidade de automação da IaaC acelera o processo de provisionamento de uma infraestrutura para desenvolver, testar e produzir aplicações. Permitindo a configuração de uma infraestrutura completa executando apenas um script. Assim possuindo os mesmos princípios seguidos na cultura DevOps no quesito da velocidade e consistência do ciclo de vida de entrega do projeto.

Consistência: Com a automatização de processos oriundos da IaaC, falhas e discrepâncias que seriam criadas por um processo manual são praticamente eliminadas. A infraestrutura como código tem a capacidade de evitar esses possíveis problemas, pois seus arquivos de configuração possuem apenas uma única fonte de informação, assim garantindo a possibilidade de realizar repetidas implantações de forma consistente e sem disparidade de informações.

Segurança: Assim como todos os serviços de cloud computing, a IaaC traz mais segurança para o ambiente de TI da sua empresa. As ferramentas de infraestrutura como código permitem a correção rápida de erros e a solução de problemas de forma automatizada, deixando assim uma infraestrutura mais segura e gerenciada pela empresa.

#IaaC no Projeto Dataplat
Está sendo criado via Terraform os recursos:
- Databricks
  - Cluster
  - Configurações
- Data Factory
  - Sources, Sink e Configurações
  - Private Endpoints
- Storage Account
  - Containers e Regra de Recycle Life
  - Private EndPoints
  - Configurações
  - Máquina Virtual 
- Synapse
  - Pool Built-In
  - Pool Dedicado

A seguir ilustração de código do Terraform:
![image.png](/.attachments/image-926994b2-27f9-47b1-8350-36c63a66f055.png)

# Automação do Desenvolvimento - Pipelines CI/CD
## Introdução de CI/CD
CI/CD designa respectivamente Continuous Integration e Continuous Delivery traduzindo: Integração Contínua e Entrega Contínua.

Ambas as siglas designam processos e técnicas modernas para tornar o processo de desenvolvimento, teste e entrega de ferramentas mais ágil e eficiente. 

**Continuous Integration, CI**

Integração Contínua ou CI, significa uma automação para que todas às vezes que haja uma mudança em código de aplicação, ela seja integrada, testada e implementada.

E todo esse processo acontecendo em um ambiente compartilhado, com todos os envolvidos no processo. 

Uma vez que é muito comum que aplicações sejam desenvolvidas por um time não somente por uma pessoa. 

Dessa forma com o CI, é possível que todas as mudanças sejam realizadas no “mesmo local”, permitindo a integração de mudanças no código de maneira mais rápida.

Por meio dessa técnica há a diminuição de conflitos e problemas quando diversos projetos acontecem simultaneamente.

Na construção da Pipeline de Build (CI) do Terraform, será gerado
um Artifact com o código selecionado no Repositório.

**Continuous Delivery, CD**

Entrega contínua ou CD, por sua vez, reúne a integração contínua e a testagem que podem ser agrupados em contêineres e depois colocado em produção.

Ou seja, ele ajunta esses códigos e testes realizados, e coloca-os em produção de forma automatizada. 

Mesmo que necessite da ação humana, ele se torna automatizado ao colocar tudo o que foi feito “no ar” de maneira integrada e completa. 
Na construção da Pipeline de Deploy (CD) do Terraform, será gerado
um Artifact com o arquivo de estado (tfstate) dos recursos criados.

## Aplicação no projeto Dataplat
O código do Iaac do Terraform está sendo versionado no Gitlab, Branch de Dataplat-Dev/Terraform. 
Está sendo usada uma abordagem de criação em 5 níveis:

- **Em ambiente de Desenvolvimento**
  - Criação dos recursos vazios básicos(ADB, ADF, Lake e Synapse)
  - Configuração dos recuros básicos (ADB, ADF, Lake e Synapse)
  - Conexão entre as ferramentas via Terraform
  - Junção das etapas anteriores com refinamento do código
  - Execução e validação de toda esteira. 
- **Em ambiente de Qualidade**
  - Adequação de ambiente QAS no código
  - Execução e validação de toda esteira 
- **Em ambiente de Produção**
  - Adequação de ambiente QAS no código
  - Execução e validação de toda esteira 

# Template do projeto CCR Dataplat

<Inseir descrição e imagem>


