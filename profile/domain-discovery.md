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
