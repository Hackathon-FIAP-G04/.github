# Desenho de Solução 📐

- [Introdução](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#introdu%C3%A7%C3%A3o)
- [Premissas](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#premissas)
- [Visão Macro da Solução](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#vis%C3%A3o-macro-da-solu%C3%A7%C3%A3o)
- [Visão Completa da Solução](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#vis%C3%A3o-completa-da-solu%C3%A7%C3%A3o)
- [Visão Detalhada](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#vis%C3%A3o-detalhada)
  - [Aplicações dos Usuários](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#aplica%C3%A7%C3%B5es-dos-usu%C3%A1rios)
  - [Autenticação de Usuário](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#autentica%C3%A7%C3%A3o-do-usu%C3%A1rio)
  - [Gestão de Médicos](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#gest%C3%A3o-de-m%C3%A9dicos)
  - [Gestão de Pacientes](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#gest%C3%A3o-de-pacientes)
  - [Agendamento de Consulta Médica](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#agendamento-de-consulta-m%C3%A9dica)
  - [Notificação](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#notifica%C3%A7%C3%A3o)
  - [Teleconsulta](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#teleconsulta)
  - [Prontuário Eletrônico](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#prontu%C3%A1rio-eletr%C3%B4nico)
- [Tecnologias](https://github.com/Hackathon-FIAP-G04/.github/blob/main/profile/solucao.md#tecnologias)

## Introdução
Este documento visa apresentar o desenho da solução ideal que atenderá aos requisitos funcionais e não funcionais especificados no problema do Hackathon. A solução proposta inclui funcionalidades essenciais como autenticação de usuários (médicos e pacientes), agendamento e gestão de consultas, notificação de usuários, Teleconsulta e Prontuário Eletrônico. 

## Premissas
Para garantir que a solução desenvolvida atenda às expectativas de desempenho, segurança e escalabilidade, as seguintes premissas arquiteturais foram adotadas:

- **Microserviços:** O sistema será dividido em microserviços independentes, cada um responsável por uma funcionalidade específica. Isso permitirá que cada serviço seja escalado de forma independente, conforme a demanda. Além de permitir a escalabilidade dos times de desenvolvimento por meio da divisão clara de responsabilidades e contextos.
  
- **Segurança:** A segurança dos dados será uma prioridade, seguindo as melhores práticas de segurança da informação, incluindo criptografia de dados em trânsito e em repouso, autenticação forte e controle de acesso baseado em funções (RBAC).

- **Alta Disponibilidade:** O sistema será projetado para garantir alta disponibilidade (24/7), com mecanismos de failover e balanceamento de carga para assegurar que o serviço permaneça disponível mesmo em casos de falhas de componentes individuai através da utilização de Kubernetes e arquitetura Serverless.

- **Escalabilidade Horizontal:** A arquitetura suportará a escalabilidade horizontal, permitindo adicionar mais instâncias de microserviços para lidar com aumentos na carga de trabalho, especialmente durante os horários de pico.

- **Nuvem:** A solução será implementada em uma infraestrutura de nuvem, aproveitando serviços gerenciados para banco de dados, balanceamento de carga, armazenamento e segurança. Isso permitirá uma gestão mais eficiente e a capacidade de escalar rapidamente conforme necessário.

## Visão Macro da Solução
<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/diagrama-contexto-macro.png" alt="Visão Macro">
</p>

## Visão Completa da Solução
Segue abaixo o desenho de solução completa, na qual será detalhada em seções posteriores.

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/solucao-completa.png" alt="Solução">
</p>

## Visão Detalhada
Nesta seção iremos detalhar cada parte do desenho de soluções, justificando as decisões e componentes utilizados.

### Aplicações dos Usuários

Com base na análise dos **atores** na dinâmica do Domain Storytelling, dividimos as visões dos usuários em duas aplicações distintas. Uma aplicação atende ao escopo do **Paciente**, enquanto a outra atende à visão do **Médico**. Ambos os usuários poderão interagir com a **Plataforma Health&Med** de duas maneiras: por meio de um **portal web**, acessível através de navegadores de internet, ou através de **aplicativos móveis** disponíveis para **iOS** e **Android**.

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/aplicacoes-do-usuario.png" alt="Aplicações dos Usuários">
</p>

Segue abaixo os componentes referentes as aplicações dos usuários:

**(1) - Aplicação Web Médico:** Refere-se ao **Portal Web** destinado ao uso do **Médico**. Por ser uma aplicação de página única **(SPA)** desenvolvida em **React**, escolhemos a simplicidade de hospedagem oferecida pelo serviço estático do **Amazon S3**. No entanto, para fornecer o serviço globalmente, seria vantajoso utilizar o serviço de **CDN** do **AWS CloudFront**.

**(2) - Aplicativo do Médico:** Refere-se à versão móvel da aplicação voltada para o Médico, disponível tanto para iOS quanto para Android.

**(3) - API Gateway Médico:** Gateway dedicado a atender as aplicações **Web** e **Mobile** do **Médico**.

**(4) - BFF Médico:** Camada intermediária entre o **frontend** e os serviços **backend**, criada para atender as aplicações **Web** e **Mobile** do **Médico**. O BFF é responsável por fazer agregação dos dados utilizando o padrão **API Composition** dos serviços de domínio.

**(5) - Aplicação Web Paciente:** Refere-se ao **Portal Web** destinado ao uso do **Paciente**. Por ser uma aplicação de página única **(SPA)** desenvolvida em **React**, escolhemos a simplicidade de hospedagem oferecida pelo serviço estático do **Amazon S3**. No entanto, para fornecer o serviço globalmente, seria vantajoso utilizar o serviço de **CDN** do **AWS CloudFront**.

**(6) - Aplicativo do Paciente:** Refere-se à versão móvel da aplicação voltada para o **Paciente**, disponível tanto para **iOS** quanto para **Android**.

**(7) - API Gateway Paciente:** Gateway dedicado a atender as aplicações **Web** e **Mobile** do **Paciente**.

**(8) - BFF Paciente:** Camada intermediária entre o **frontend** e os serviços **backend**, criada para atender as aplicações **Web** e **Mobile** do **Paciente**. O BFF é responsável por fazer agregação dos dados utilizando o padrão **API Composition** dos serviços de domínio.

**(9) - Serviços de Domínio:** Refere-se ao conjunto de microsserviços de domínios: **Gestão de Pacientes**, **Gestão de Médicos**, **Prontuário Eletrônico**, **Agendamento de Consulta Médica**, **Serviço de Video Chamada** e **Serviço de Notificação**.



### Autenticação do Usuário

Para atender aos requisitos de autenticação de usuários, optamos por utilizar o serviço de identidade da **AWS** chamado **Amazon Cognito**. Utilizamos dois user pools: o **healthmed-doctors-user-pool** para os médicos e o **healthmed-patients-user-pool** para os pacientes.

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/autenticacao-de-usuario.png" alt="Autenticação do Usuário">
</p>

**(1) - Amazon Cognito** oferece uma solução robusta para gerenciar a autenticação, autorização e usuários, proporcionando várias vantagens:

* Segurança Avançada: Amazon Cognito implementa várias camadas de segurança, incluindo autenticação multifatorial (MFA), verificação de e-mail e número de telefone, além de detecção de comportamento suspeito.

* Escalabilidade: O serviço é altamente escalável, suportando milhões de usuários e garantindo que o sistema possa crescer conforme a demanda aumenta sem comprometer o desempenho.

* Integração com Outras Ferramentas da AWS: Amazon Cognito se integra facilmente com outros serviços da AWS, como AWS Lambda e Amazon API Gateway facilitando a criação de soluções completas e coesas.

* Suporte a Padrões de Autenticação: O serviço suporta padrões de autenticação como OAuth 2.0, SAML 2.0, e OpenID Connect, permitindo a integração com provedores de identidade de terceiros, como Google, Facebook e Apple.

* Personalização e Flexibilidade: Cognito permite personalizar as telas de login e outros fluxos de autenticação para melhor atender às necessidades e à identidade visual da aplicação.

* Gerenciamento de Sessões e Tokens: O serviço lida com a geração e a renovação de tokens de acesso e de atualização, facilitando o gerenciamento de sessões e a segurança da aplicação.


### Gestão de Médicos

Para representar o subdomínio **Gestão de Médicos**, optamos pela criação de um microsserviço para expor as seguintes funcionalidades:
* Cadastrar Médico
* Alterar dados do Médico
* Visualizar dados do Médico
* Pesquisar Médico

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/gestao-de-medico-solucao.png" alt="Gestão de Médicos">
</p>

**(1) - Serviço de Gestão de Médico:** API destinada a fornecer operações relacionadas à entidade Médico. Esta API está sendo provisionada em **Kubernetes**, utilizando o serviço **Amazon Elastic Kubernetes Service (EKS)**.

**(2) - Cache:** Para atender aos requisitos de desempenho e escalabilidade, adicionamos uma **camada de cache** usando **Redis** através do serviço **Amazon ElastiCache** para armazenar os dados do médico, considerando que esses dados são pouco mutáveis.

**(3) - Banco de Dados:** Para o armazenamento de dados do médico, escolhemos utilizar o **Atlas MongoDB**, pois o **MongoDB** oferece recursos de consultas geoespaciais, atendendo a um dos requisitos do Hackathon.


### Gestão de Pacientes

Para representar o subdomínio **Gestão de Pacientes**, optamos pela criação de um microsserviço para expor as seguintes funcionalidades:
* Cadastrar Paciente
* Alterar dados do Paciente
* Visualizar dados do Paciente

<p align="center">
  <img width="80%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/gestao-de-paciente-solucao.png" alt="Gestão de Pacientes">
</p>

**(1) - Serviço de Gestão de Paciente:** API destinada a fornecer operações relacionadas à entidade Paciente. Esta API está sendo provisionada em **Kubernetes**, utilizando o serviço **Amazon Elastic Kubernetes Service (EKS)**.

**(2) - Banco de Dados:** Para o armazenamento dos dados do Paciente, optamos por utilizar o **Atlas MongoDB**, pois a estrutura de dados do Paciente segue um modelo de **Aggregate**, que se adapta perfeitamente ao banco de dados orientado a documentos.

### Agendamento de Consulta Médica

Para atender aos requisitos de agendamento de consultas médicas, implementamos um mecanismo que gera horários disponíveis na agenda do médico com base nas configurações de horário para cada dia da semana. Esse mecanismo funciona da seguinte forma:

* Configuração de Horários: Cada médico define seus horários de atendimento para cada dia da semana.

* Geração de Slots: Uma rotina automatizada é executada diariamente, criando os slots de agenda disponíveis com base nas configurações definidas.

* Antecedência de Agendamento: Esse sistema garante que os pacientes possam agendar consultas com até 30 dias de antecedência.

Essa abordagem assegura que a agenda dos médicos seja atualizada continuamente e de forma precisa, permitindo um processo de agendamento eficiente e confiável.

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/agendamento-de-consulta-solucao.png" alt="Agendamento de Consulta Médica">
</p>

**(1) - Serviço de Agendamento de Consulta:** API de abstrai os serviços de agendamento de consulta médica que pode ser utilizado por **Médico** e **Paciente**.

**(2) - Banco de Dados:** Optamos pela utilização do MongoDB para armazenamento de dados de consulta médica.

**(3) - Planejador de Agenda Mensal:** Rotina automatizada que geram diariamente os slots nas agendas dos médicos baseado nas configurações de horário disponíveis.

**(4) - Fila de Solicitação de Criação de Agenda:** Optamos pela utilização de mensageria para ganhar escala usando o serviço SQS. 

**(5) - Criador de Agenda:** Lambda que cria os slots nas agendas dos médicos.

**(6) - Fila de Status de Consulta Alterado:** Fila que recebe todas as alterações de estados sofridos por uma consulta médica como: **Consulta Aceita**, **Consulta Recusada**, **Consulta Cancelada** e **Consulta Concluída** para envio de notificação.


### Notificação

Visando trazer melhor experiência para os usuários da plataforma Health&Med, incluímos um recurso de notificação por email para as mudanças de status de uma consulta médica, como ilustra a imagem abaixo:

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/notificacao-solucao.png" alt="Gestão de Médicos">
</p>

**(1) - Fila de Status de Consulta Alterado:** Fila que recebe todas as alterações de estados sofridos por uma consulta médica como: **Consulta Aceita**, **Consulta Recusada**, **Consulta Cancelada** e **Consulta Concluída** para envio de notificação.

**(2) - Notificador de Status de Consulta:** Optamos pela utilização de um recurso Serverless, pois entendemos que com AWS Lambda, você só paga pelo tempo de computação que realmente utiliza, sem necessidade de manter servidores sempre ativos. Isso pode resultar em economias significativas, especialmente para aplicações com cargas de trabalho variáveis ou esporádicas como este.

**(3) - Serviço de Gestão de Médico:** API destinada a fornecer operações relacionadas à entidade Médico. Esta API está sendo provisionada em **Kubernetes**, utilizando o serviço **Amazon Elastic Kubernetes Service (EKS)**.

**(1) - Serviço de Gestão de Paciente:** API destinada a fornecer operações relacionadas à entidade Paciente. Esta API está sendo provisionada em **Kubernetes**, utilizando o serviço **Amazon Elastic Kubernetes Service (EKS)**.

**(5) - Amazon Simple Email Service (SES):** Serviço externo de envio de Email da AWS.

**(6) - Fila de Notificações com Falha de Envio:** Implementação de um mecanismo de Deadletter Queue para envio dos emails.

**(7) - Reprocessador de Notificações:** Serviço de reprocessamento de mensagens com erro.


### Teleconsulta

Para atender o escopo de realização de video chamadas entre Médico e Paciente optamos pela utilização de um serviço externo da plataforma Zoom como mostra a imagem abaixo:

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/video-chamada-solucao.png" alt="Gestão de Médicos">
</p>

**(1) - Serviço de Geração de Token:** API destinada a geração de token para conexão em uma video chamada. Esta API está sendo provisionada em **Kubernetes**, utilizando o serviço **Amazon Elastic Kubernetes Service (EKS)**.

**(2) - Zoom:** Serviço externo de video chamada.

**(3) - Aplicações Cliente:** **Front End** que realiza conexão no **Zoom** por meio de **SDK** utilizando o token gerado.

### Prontuário Eletrônico

Para desenvolver uma solução de prontuário eletrônico onde pacientes podem fazer upload de arquivos, o design deve contemplar tanto os aspectos de **segurança** e **privacidade** quanto a **interoperabilidade**. Entendemos que para atender esses aspectos a solução de **Blockchain** é super indicada.

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/prontuario-eletronico-solucao.png" alt="Prontuário Eletrônico">
</p>

**(1) - Serviço de Prontuário Eletrônico:** API que gera URLs seguras para upload de arquivos, gerencia a criação de metadados para a busca de documentos e registra as ações na Blockchain..

**(2) - Controlador de Chaves de Criptografia:** API de gerenciamento de chaves de criptografia para garantir que os dados armazenados no S3 estejam protegidos utilizando o serviço AWS Key Management Service (KMS).

**(3) - Aplicações Cliente:** Aplicação Cliente que faz upload e download do documento.

**(4) - Amazon S3:**  Armazenamento dos Documentos de forma segura utilizando o Amazon S3.

**(5) - Fila de Documentos Adicionados:** Fila que recebe os eventos após um upload de documento.

**(6) - Processador de Documento Adicionado:** Lambda que após a inclusão de um documento, gera os metadados de busca e o registro na Blockchain.

**(7) - Serviço de Blockchain:** A utilização de Blockchain para gerenciar transações e registros de metadados garante maior integridade e imutabilidade dos registros, proporcionando, assim, maior segurança.

**(8) - Banco de Metadados:** Visando possibilitar consultas de documentos, optamos por gerar um banco de dados de metadados utilizando DynamoDB.

### Tecnologias

Para a solução, foram utilizadas as seguintes tecnologias:

* **.NET 8.0** para o desenvolvimento das APIs dos microsserviços
* **Kubernetes** para gerenciar os recursos da API
* **Helm** para gerar os artefatos Kubernetes
* **MongoDB** como base de dados das APIs
* **GeoJson** como recurso para consulta dos médicos a partir da localização
* **SonarQube** para analisar a qualidade do código
* **EKS** como infraestrutura de cluster Kubernetes na Cloud
* **Amazon API Gateway** para gerenciar o acesso às APIs
* **Cognito** como pool de usuários que acessam a API
* **Atlas MongoDB** como recurso para gerar as bases de dados na Cloud
* **Terraform** para gerenciar e gerar os recursos na Cloud
*  **Amazon Simple Email Service (SES)** como serviço de envio de Email
*  **AWS Lambda** para componentes de arquitetura Serverless
*  **AWS Key Management Service** para gerenciamento de chaves de criptografia
*  **Amazon S3** para armazenamento de documentos e hospedagem de arquivo estático
*  **Amazon Managed Blockchain** como serviço de Blockchain para registro das transações de documentos
*  **AWS Simple Queue Service (SQS)** como serviço de fila
*  **DynamoDB** para armazenamento de metadados dos documentos
*  **AWS Elasticache** como sserviço de cache do tipo Redis
  
### Repositórios do MVP

A seguir estão os repositórios criados para desenvolver a aplicação MVP:

* [healthmed-doctor](https://github.com/Hackathon-FIAP-G04/healthmed-doctor) - API de gerenciamento de Médicos
* [healthmed-appointment](https://github.com/Hackathon-FIAP-G04/healthmed-appointment) - API para gerencimento de agendamentos
* [terraform](https://github.com/Hackathon-FIAP-G04/terraform) - Estrutura do Terraform para VPC, cluster EKS, Api Gateway e Cognito
* [data](https://github.com/Hackathon-FIAP-G04/data) - Estrutura do Terraform para as bases de dados criadas no Atlas MongoDB
