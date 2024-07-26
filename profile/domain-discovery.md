# Domain Discovery 💡

- [Visão Geral do Problema](#)
- [Análise do Cenário Atual](#)
  - [Atores](#)
  - [Cenários](#)
    - [Autenticação do Médico](#)
    - [Preparação e Retirada do Pedido](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#prepara%C3%A7%C3%A3o-e-retirada-do-pedido)
    - [Revisar Informações do Cardápio](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#revisar-informa%C3%A7%C3%B5es-do-card%C3%A1pio) 
- [Mapeamento de Domínios e Subdomínios](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#mapeamento-de-dom%C3%ADnios-e-subdom%C3%ADnios)
  - [Core Domains](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#core-domains)
  - [Supporting Domains](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#supporting-domains)
  - [Generic Domains](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#generic-domains)
- [Análise de Subdomínios no Cenário TO-BE](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#an%C3%A1lise-de-subdom%C3%ADnios-no-cen%C3%A1rio-to-be)
- [Análise Estratégica dos Subdomínios](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#an%C3%A1lise-estrat%C3%A9gica-dos-subdom%C3%ADnios)
- [Visão Geral da Solução](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#vis%C3%A3o-geral-da-solu%C3%A7%C3%A3o)
  - [Módulo de Autoatendimento](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#m%C3%B3dulo-de-autoatendimento)
  - [Módulo de Acompanhamento de Pedido](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#m%C3%B3dulo-de-acompanhamento-de-pedido)
  - [Módulo de Gestão de Cardápio](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#m%C3%B3dulo-de-gest%C3%A3o-de-card%C3%A1pio)
- [Dicionário de Linguagem Ubíqua](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#dicion%C3%A1rio-de-linguagem-ub%C3%ADqua)
- [Event Storming](https://github.com/FIAP-G04/.github/blob/main/profile/Domain-Discovery.md#event-storming)

## Visão Geral do Problema
<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/health&med.png" alt="Health&Med">
</p>

A **Health&Med**, uma startup inovadora no setor de saúde, está desenvolvendo um novo sistema que irá revolucionar a Telemedicina no país. Atualmente, a startup oferece a possibilidade de agendamento de consultas e realização de consultas
online (Telemedicina) por meio de sistemas terceiros como **Google Agenda** e **Google Meetings**.

Recentemente, a empresa recebeu um aporte e decidiu investir no desenvolvimento de um sistema proprietário, visando proporcionar um serviço de maior qualidade, segurança dos dados dos pacientes e redução de custos. O objetivo é criar um sistema robusto, escalável e seguro que permita o
gerenciamento eficiente desses agendamentos e consultas.

Além de conter as funcionalidades de agendamento e realização de consultas online, o sistema terá o diferencial de uma nova funcionalidade: o Prontuário Eletrônico. O Prontuário Eletrônico permitirá o armazenamento e compartilhamento de documentos, exames, cartão de vacinas, e outros registros
médicos entre as partes envolvidas, garantindo maior assertividade nos diagnósticos.

## Decomposição do Problema na Visão de Domain Storytelling

Nesta seção, através da aplicação da metodologia do Domain Storytelling, iremos explorar os requisitos funcionais e os atores centrais que desempenham papéis fundamentais nas narrativas compartilhadas no Hackathon.

### Atores
Partindo como base o documento de requisitos fornecido na abertura do Hackathon, 3 atores foram identificadosl:

| Atores | Descrição |
|--------|-----------|
| Paciente | Usuário que busca consultas médicas e utiliza os serviços de telemedicina da Health&Med. Pode agendar consultas, acessar seu prontuário eletrônico, fazer upload de documentos médicos e compartilhar informações com médicos. |
| Médico | Profissional de saúde registrado na plataforma da Health&Med. Pode gerenciar sua agenda de consultas, aceitar ou recusar consultas, realizar teleconsultas e acessar prontuários eletrônicos compartilhados pelos pacientes. |
| Sistema | Plataforma tecnológica da **Health&Med** utilizada como meio de interação entre Paciente e Médico. |

## Mapeamento de Domínios e Subdomínios
Um domínio se refere a uma esfera de conhecimento ou atividade no mundo real que abrange um espaço de problema específico. Esse domínio possui sua própria linguagem, conceitos, regras e práticas que o tornam únicos. No contexto do Hackathon o nosso domínio é **Telemedicina**.

Por outro lado, um subdomínio é uma subdivisão ou área menor de conhecimento ou atividade dentro de um domínio mais amplo. Os subdomínios representam uma granularização desse espaço de problema e podem se concentrar em tópicos ou aspectos específicos dentro do domínio principal. Isso ajuda a organizar e categorizar o conhecimento de forma mais detalhada e específica. Desta forma, entendemos que o Domínio da Lanchonete Fast Food possui os seguintes subdomínios:

<p align="center">
  <img width="90%" src="https://github.com/FIAP-G04/.github/blob/main/images/subdominios-as-is.png" alt="Subdomínios AS-IS">
</p>

### Core Domains
Os domínios principais **(Core Domains)** são aqueles que estão no cerne do negócio e geralmente são os mais complexos e específicos, dos quais temos **Agendamento de Consulta** e **Prontuário Eletrônico**.

- **Gestão de Cardápio:** Responsável por definir os produtos oferecidos na lanchonete fast food, além de seus preços, ingredientes, categorias, promoções e variações. Faz parte do Core Domain, visto que é de extrema importância para o funcionamento eficiente da lanchonete.

- **Gerenciamento de Pedidos:** Este subdomínio lida com a criação, preparação, acompanhamento, montagem e retirada dos pedidos dos clientes. Este é um **Core Domain**, pois lida diretamente com a funcionalidade central do negócio, ou seja, a criação e gestão de pedidos dos clientes. Devido a sua complexidade, poderíamos subdivídi-lo em 3 subdomínios: 

### Supporting Domains

Os domínios de suporte **(Supporting Domains)** são aqueles que oferecem suporte direto às operações principais do negócio, mas não são a parte central do mesmo. Eles ajudam a impulsionar as vendas, a atrair clientes ou simplesmente garantir o funcionamento dos Core Domains. Considerando o contexto do Hackathon, temos 2 subdomínios: **Gestão de Paciente** e **Gestão de Médicos**.

- **Gestão de Estoque:** Gerencia o estoque de ingredientes, as quantidades disponíveis e as encomendas de ingredientes. Embora seja um domínio importante, ele está mais voltado para dar suporte às operações principais, como garantir que os ingredientes estejam disponíveis para os pedidos. Portanto, pode ser considerado um **Supporting Domai**n. Se fossemos detalhar esse subdomínio, provavelmente teríamos mais atores envolvidos no contexto. Além disso poderíamos subdividir esse subdomínio em **3** outros **subdomínios**:

- **Marketing & Promoções:** Este subdomínio gerencia campanhas de marketing, promoções, cupons e programas de fidelidade. Ele é responsável por um conjunto ações que visam a atração de clientes e a maximização das vendas.

### Generic Domains

Os domínios genéricos **(Generic Domains)** são geralmente aqueles que não são exclusivos para o negócio e podem ser compartilhados com outros domínios de negócio. No contexto do Hackathon, podemos considerar os possíveis subdomínios: **Notificação**, **Video Chamada** e **Autenticação & Autorização**.

- **Atendimento ao Cliente:** Responsável pela gestão de reclamações, feedback do cliente e a satisfação do cliente, que por sua vez, são considerados aspectos comuns em todos os tipos de negócio.

- **Pagamento:** Responsável pelos processos de pagamento, faturamento e transações financeiras. Embora seja de extrema importância para a lanchonete fast food, é uma funcionalidade comum a muitos tipos de negócios.

- **Financeiro:** A gestão financeira tem papel fundamental para a saúde e sustentabilidade de qualquer negócio, e a lanchonete não é exceção. Através deste subdomínio, a empresa pode acompanhar seus custos, margens de lucro, impostos e outras informações financeiras críticas para tomada de decisão.

- **Recursos Humanos:** Este subdomínio desempenha um papel fundamental na gestão da equipe que trabalha na lanchonete, assegurando que haja pessoal adequado para todas as tarefas diárias. Sua responsabilidade principal consiste em garantir que a lanchonete esteja em conformidade com todas as regulamentações trabalhistas, proporcionando um ambiente de trabalho seguro e produtivo para seus funcionários. Isso é alcançado por meio do recrutamento e capacitação de profissionais apropriados.

