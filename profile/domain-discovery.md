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

## Mapeamento de Domínios e Subdomínios
Um domínio se refere a uma esfera de conhecimento ou atividade no mundo real que abrange um espaço de problema específico. Esse domínio possui sua própria linguagem, conceitos, regras e práticas que o tornam únicos. No contexto do Hackathon o nosso domínio é **Telemedicina**.

Por outro lado, um subdomínio é uma subdivisão ou área menor de conhecimento ou atividade dentro de um domínio mais amplo. Os subdomínios representam uma granularização desse espaço de problema e podem se concentrar em tópicos ou aspectos específicos dentro do domínio principal. Isso ajuda a organizar e categorizar o conhecimento de forma mais detalhada e específica. Desta forma, entendemos que o Domínio de Telemedicina possui os seguintes subdomínios:

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/subdominios.png?raw=true" alt="Subdomains">
</p>

### Core Domains
Os domínios principais **(Core Domains)** são aqueles que estão no cerne do negócio e geralmente são os mais complexos e específicos, dos quais temos **Agendamento de Consulta Médica**, **Prontuário Eletrônico** e **Teleconsulta**.

- **Agendamento de Consulta Médica:** Este subdomínio abrange todas as funcionalidades relacionadas ao gerenciamento de horários e consultas entre médicos e pacientes. Médicos podem cadastrar e editar seus horários disponíveis, aceitar ou recusar consultas agendadas pelos pacientes, enquanto os pacientes podem buscar médicos, visualizar suas agendas e agendar ou cancelar consultas conforme necessário.

- **Teleconsulta:** Focado na realização de consultas médicas online, este subdomínio inclui a criação automática de links para reuniões online quando uma consulta é agendada. No dia da consulta, tanto o médico quanto o paciente utilizam este link para realizar a teleconsulta, facilitando o atendimento médico à distância.

- **Prontuário Eletrônico:** Este subdomínio é dedicado ao armazenamento e gerenciamento de informações médicas dos pacientes. Permite aos pacientes acessar seus prontuários eletrônicos, fazer upload de documentos como exames e laudos médicos, e gerenciar o compartilhamento desses documentos com médicos, definindo acessos específicos e durações. 

### Supporting Domains

Os domínios de suporte **(Supporting Domains)** são aqueles que oferecem suporte direto às operações principais do negócio, mas não são a parte central do mesmo. Eles ajudam a impulsionar as vendas, a atrair clientes ou simplesmente garantir o funcionamento dos Core Domains. Considerando o contexto do Hackathon, temos 2 subdomínios: **Gestão de Paciente** e **Gestão de Médicos**.

- **Gestão de Médicos:** Facilita aos pacientes encontrar médicos disponíveis para consultas. Utiliza filtros como especialidade, distância e avaliação para que os pacientes possam escolher o médico que melhor atenda às suas necessidades, proporcionando uma experiência personalizada e eficiente. 

- **Gestão de Pacientes:** É responsável por todas as interações e informações relacionadas aos pacientes dentro do sistema. Isso inclui o gerenciamento dos dados pessoais dos pacientes, como informações de contato, preferências de comunicação entre outros. Os pacientes podem criar e atualizar seus perfis, visualizar e editar suas informações pessoais.

### Generic Domains

Os domínios genéricos **(Generic Domains)** são geralmente aqueles que não são exclusivos para o negócio e podem ser compartilhados com outros domínios de negócio. No contexto do Hackathon, podemos considerar os possíveis subdomínios: **Notificação** e **Autenticação & Autorização**.

- **Notificação:** É responsável por gerenciar e enviar comunicações e alertas para os usuários do sistema, tanto para médicos quanto para pacientes.

- **Autenticação & Autorização:** Responsável por garantir que médicos e pacientes possam acessar o sistema de forma segura. Médicos utilizam seu número de CRM e uma senha para login, enquanto pacientes usam e-mail, CPF e senha. Este subdomínio garante que apenas usuários autorizados acessem o sistema.

- **Video Chamada:** É responsável por toda infraestrutura e serviços de realização de chamadas de video utilizadas pelo subdomínio Teleconsulta.

## Dicionário de Linguagem Ubíqua
Segue abaixo um conjunto de palavras que compõem o dicionário de **linguagem ubíqua** ao contexto da **Health&Med**:

| Termo                        | Definição                                                                                                         |
|------------------------------|-------------------------------------------------------------------------------------------------------------------|
| **Paciente**                 | Usuário do sistema que busca serviços médicos, agenda consultas e gerencia seu prontuário eletrônico.              |
| **Médico**                   | Profissional de saúde registrado que oferece consultas, realiza atendimentos e gerencia sua agenda de consultas.   |
| **Consulta**                 | Interação programada entre um médico e um paciente, realizada por teleconsulta.                |
| **Agendamento de Consulta**  | Processo pelo qual um paciente marca uma consulta com um médico, selecionando data e hora disponíveis.             |
| **Teleconsulta**             | Consulta médica realizada remotamente por meio de uma plataforma online, usando um link gerado para reunião virtual. |
| **Prontuário Eletrônico**    | Documento digital que armazena informações médicas do paciente, incluindo exames, laudos e histórico de consultas. |
| **Autenticação**             | Processo de verificação da identidade do usuário para acesso ao sistema, utilizando credenciais como número de CRM e CPF. |
| **Notificação**              | Comunicação enviada aos usuários para informá-los sobre eventos importantes, como agendamentos e lembretes.        |
| **Cadastro de Horários Disponíveis** | Funcionalidade que permite aos médicos definir e atualizar seus horários disponíveis para consultas.               |
| **Aceite de Consulta**       | Ação do médico para confirmar sua disponibilidade e concordar com uma consulta agendada por um paciente.           |
| **Recusa de Consulta**       | Ação do médico para negar uma solicitação de consulta agendada por um paciente.                                     |
| **Cancelamento de Consulta** | Ação do paciente para anular uma consulta previamente agendada, podendo fornecer uma justificativa.                 |
| **Upload de Documentos**     | Processo pelo qual um paciente adiciona documentos, como exames e laudos, ao seu prontuário eletrônico.             |
| **Compartilhamento de Documentos** | Funcionalidade que permite ao paciente definir quais documentos do prontuário eletrônico podem ser acessados por médicos e por quanto tempo. |
| **Link de Reunião Online**   | URL gerada pelo sistema para acesso à teleconsulta, facilitando a reunião virtual entre médico e paciente.          |
