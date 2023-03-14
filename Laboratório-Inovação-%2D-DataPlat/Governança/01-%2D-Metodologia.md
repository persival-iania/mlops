A metodologia aplicada se fez em majoritariamente baseada no DAMA, com algumas adaptações de modelos do Gartner e Mircrosift. Foram divididas em 3 partes macros:
- **Estratégico**:
  - Prioridades e visão: Mapeamento dos principais problemas e dores relacionados a dados
  - Papéis e responsabilidades: Definição do time, que ocuparão os papéis (CDO, Data Owner, Data Steward, E outros )
  - Definição dos Comitês: Levantamento do time que irá participar das discussões da área de Negócio, Técnico e EGD
  - Escopo MVP (EGD): Definição de quais áreas e recursos serão envolvidos no ciclo ou onda.
 - **Tático**
   - Plano de ação (Data Steward): Planejamento de como a governança de dados estratégica será aplicada seguindo priorizações e pilares como: Qualidade, MDM, Arquitetura, Data Mapping, Privacidade e Segurança.
- **Operacional**
  - Implantação das políticas de GD
  - Acompanhamento de monitoria
A seguir uma imagem que poderá elucidar melhor os pontos supracitados:

#![Items.png](/.attachments/Items-18b9c6fd-4cf7-4e13-963c-110dda63b474.png)

**Detalhamento do Escopo Estratégicos**
1.	Comunicar e formalizar o papel do Data Owner e Data Steward
2.	Definição do escopo e até onde temos valor agregado
3.	Mapear os problemas referentes aos dados, as principais, gaps de definição
4.	Identificar a importância e a criticidade do dado para o negócio
5.	Identificar as origens dos dados
6.	Identificar se o dado é processado/transformado
7.	Identificar quem utiliza os dados, qual área e qual propósito



**Detalhamento do Escopo Tático**
O framework escolhido é da DAMA, que divide o programa de governança nas seguintes diretrizes:

•	**Qualidade**: Trata-se de planejar e projetar o saneamento do dado, provendo qualidade ao mesmo, para que este dado possa gerar informações confiáveis para suportar a tomada de decisão. O objetivo é planejar, implementar e controlar atividades que apliquem técnicas de gerência de qualidade de dados para medir, avaliar, melhorar e garantir a adequação dos dados ao seu uso pretendido.(BARBIERI, 2013)

•	**Privacidade e Segurança**: É necessário planejar e projetar uma estrutura capaz de garantir a privacidade, confidencialidade e acesso apropriado ao dado.

•	**MDM**: rata-se de projetar uma estrutura que promova uma “Central Única da Verdade”, garantindo um versão consistente e confiável do dado, onde possa ser distribuído (ou compartilhado) para outros contextos.
Os dados mestres constituem os principais dados da empresa. São dados sobre entidades de negócios vitais que dão contexto às transações. Esses dados de acordo com DATA Governance Glossary “descrevem as entidades centrais de uma empresa e são utilizados por vários sistemas de processos de negócios e de TI. Exemplos desses dados são as partes, por exemplo, (clientes, funcionários, fornecedores, parceiros), lugares, por exemplo, (locais, territórios de vendas, escritórios), e as coisas (contas, produtos, bens, conjuntos de documentos) ”.
A gestão de dados mestres é o controle sobre os valores de dados mestres para viabilizar o uso contextual, consistentes, compartilhados entre os sistemas, deforma acurada, temporal e relevante para as entidades essenciais do negócio. (DMBOK, 2012).

•	**Arquitetura**: rata-se de entender quais os requisitos do seu projeto de dados, ou seja, entender quais os dados que são necessários, de onde eles vêm e por onde terão de passar até chegar ao seu dashboard. É definir o caminho deste dado.

•	**Desenvolvimento dos dados**: Trata-se de analisar os requisitos dos dados, implantar o seu modelo de dados, definir como será a manutenção destes modelos de dados, projetar estruturas de bancos de dados para suportar suas necessidades, projetar como será o versionamento e integração de dados e modelo de dados, projetar planos de testes, projetar planos de migração entre outras atividades.
Consiste na análise, projeto, implementação, implantação, e manutenção de soluções de dados para maximizar o valor de recursos de dados para a organização. (DMBOK, 2012).

•	**Meta Dados**: Primeiro você precisa saber o que é metadado, correto? Pois bem, metadado é o dado a respeito de outro dado, ou seja, são informações que complementam um dado. Por exemplo: 2 maçãs (dado), Foto destas mesmas 2 maçãs (Metadado). Portanto, o metadado tem a mesma importância do dado e o gerenciamento de metadados segue as mesmas atividades do gerenciamento de dados.
Os meta-dados descrevem a estrutura e significados a respeito de dados e, assim contribuem para que seu uso seja eficiente ou ineficiente, oferecendo contexto aos dados relacionados, ou seja informações que gerem conhecimento (TURBAN; ET. ALL, 2009).

•	**DW,BI e Lake**: rata-se de planejar e projetar modelos de dados que permitam a geração de informações para tomada de decisão sob várias perspectivas (dimensões).
A gestão do Data Warehousing e Business Intelligence consiste na coleta, integração e apresentação dos dados para fins de análise de negócios e tomadas de decisão, composto por atividades de apoio a todas as fases do ciclo de vida de suporte à decisão que fornece contexto, move e transforma os dados de fontes para um destino comum de armazenamento dos dados e subsidie meios de acesso, manipulação e geração de relatórios a partir deste destino comum (DAMA DMBOK, 2012).

Segundo o DMBOK (2012) a gestão do Data Warehousing e Business Intelligence tem como os seguintes objetivos: fornecer o armazenamento atuais e históricos integrado organizado por áreas temáticas; garantir credibilidade, qualidade, estabilidade, alto desempenho e ambiente para aquisição, gestão e acesso a dados, e para todos os recursos de acesso adequados; proporcionar um ambiente de acesso fácil de usar, flexível e abrangente, entre outros.
Gerenciamento da documentação e conteúdo: Trata-se de planejar e projetar a implantação e a gestão a dados não estruturados, ou seja, que estão fora de um banco de dados. É importante que seja definido um plano para armazenamento, proteção e acesso a estes dados.
O objetivo é planejar, implementar e controlar atividades para armazenar, proteger e acessar dados encontrados em arquivos eletrônicos e registros físicos (texto, gráficos, imagens, áudio e vídeo), ou seja, o foco em dados não estruturados, não armazenados em sistemas relacionais (DMBOK, 2012)

•	**Documentacão e Conteúdo**: Trata-se de planejar e projetar a implantação e a gestão a dados não estruturados, ou seja, que estão fora de um banco de dados. É importante que seja definido um plano para armazenamento, proteção e acesso a estes dados.
O objetivo é planejar, implementar e controlar atividades para armazenar, proteger e acessar dados encontrados em arquivos eletrônicos e registros físicos (texto, gráficos, imagens, áudio e vídeo), ou seja, o foco em dados não estruturados, não armazenados em sistemas relacionais (DMBOK, 2012)
•	**Operações de Database**: rata-se do planejamento, controle, manutenção e suporte ao ativo dado, durante todo o seu ciclo de vida, ou seja, desde sua aquisição, passando por sua exibição, até a eliminação desse dado. Vale ressaltar que um planejamento de Recuperação de desastre é de extrema importância para qualquer projeto.

**Por onde devemos começar?**

- Os domínios prioritários estão sendo definidos.

- A sugestão é que sejam entre 2 a 4 domínios no primeiro ciclo

- Definição do Comitê de Governança de Dados

- Para cada domínio escolhido é necessário a definição do Data Owner

- Definição do Data Steward por parte do Data Owner (*)

OBS: Ainda precisa ser homologado pelo time de segurança da CCR.

