## Visão Geral da Solução

### Visão Macro da Solução
<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/diagrama-contexto-macro.png" alt="Diagrama de Contexto">
</p>

### Aplicações dos Usuários

Com base na análise dos **atores** na dinâmica do Domain Storytelling, dividimos as visões dos usuários em duas aplicações distintas. Uma aplicação atende ao escopo do **Paciente**, enquanto a outra atende à visão do **Médico**. Ambos os usuários poderão interagir com a **Plataforma Health&Med** de duas maneiras: por meio de um **portal web**, acessível através de navegadores de internet, ou através de **aplicativos móveis** disponíveis para **iOS** e **Android**.

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/aplicacoes-do-usuario.png" alt="Diagrama de Contexto">
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

**Amazon Cognito** oferece uma solução robusta para gerenciar a autenticação, autorização e usuários, proporcionando várias vantagens:

* Segurança Avançada: Amazon Cognito implementa várias camadas de segurança, incluindo autenticação multifatorial (MFA), verificação de e-mail e número de telefone, além de detecção de comportamento suspeito.

* Escalabilidade: O serviço é altamente escalável, suportando milhões de usuários e garantindo que o sistema possa crescer conforme a demanda aumenta sem comprometer o desempenho.

* Integração com Outras Ferramentas da AWS: Amazon Cognito se integra facilmente com outros serviços da AWS, como AWS Lambda e Amazon API Gateway facilitando a criação de soluções completas e coesas.

* Suporte a Padrões de Autenticação: O serviço suporta padrões de autenticação como OAuth 2.0, SAML 2.0, e OpenID Connect, permitindo a integração com provedores de identidade de terceiros, como Google, Facebook e Apple.

* Personalização e Flexibilidade: Cognito permite personalizar as telas de login e outros fluxos de autenticação para melhor atender às necessidades e à identidade visual da aplicação.

* Gerenciamento de Sessões e Tokens: O serviço lida com a geração e a renovação de tokens de acesso e de atualização, facilitando o gerenciamento de sessões e a segurança da aplicação.

<p align="center">
  <img width="100%" src="https://github.com/Hackathon-FIAP-G04/.github/blob/main/images/aplicacoes-do-usuario.png" alt="Diagrama de Contexto">
</p>

### Gestão de Médicos


### Gestão de Pacientes
