## Visão Geral da Solução

### Visão Macro da Solução
<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/diagrama-contexto-macro.png" alt="Diagrama de Contexto">
</p>

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


### Serviço de Video Chamada

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

**(6) - Processador de Documento Adicionado:**

**(7) - Serviço de Blockchain:**

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
