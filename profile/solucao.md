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
  <img width="80%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/agendamento-de-consulta-solucao.png" alt="Agendamento de Consulta Médica">
</p>

### Serviço de Video Chamada

Para atender o escopo de realização de video chamadas entre Médico e Paciente optamos pela utilização de um serviço externo da plataforma Zoom como mostra a imagem abaixo:

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/video-chamada-solucao.png" alt="Gestão de Médicos">
</p>

**(1) - Serviço de Geração de Token:** API destinada a geração de token para conexão em uma video chamada. Esta API está sendo provisionada em **Kubernetes**, utilizando o serviço **Amazon Elastic Kubernetes Service (EKS)**.

**(2) - Zoom:** Serviço externo de video chamada.

**(3) - Aplicações Cliente:** **Front End** que realiza conexão no **Zoom** por meio de **SDK** utilizando o token gerado.

