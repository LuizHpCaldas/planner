# Projeto de Cadastro e Gerenciamento de Viagens

Este projeto tem como objetivo permitir que usuários possam cadastrar e gerenciar viagens, incluindo a confirmação de presença de convidados e a adição de atividades e links importantes relacionados à viagem.

## Funcionalidades

### Cadastro de Viagem

- O usuário pode cadastrar uma viagem informando:
  - Local de destino
  - Data de início
  - Data de término
  - E-mails dos convidados
  - Nome completo
  - Endereço de e-mail

### Confirmação da Viagem

- O criador da viagem recebe um e-mail para confirmar a nova viagem através de um link.
- Ao clicar no link, a viagem é confirmada.
- Os convidados recebem e-mails de confirmação de presença.
- O criador é redirecionado para a página da viagem.

### Confirmação de Presença dos Convidados

- Os convidados, ao clicarem no link de confirmação de presença, são redirecionados para a aplicação.
- Devem inserir seu nome (o e-mail já estará preenchido).
- Após isso, estarão confirmados na viagem.

### Página do Evento

- Os participantes da viagem podem adicionar links importantes, como:
  - Reserva do AirBnB
  - Locais para serem visitados
- O criador e os convidados podem adicionar atividades que irão ocorrer durante a viagem com:
  - Título
  - Data
  - Horário

### Convite de Novos Participantes

- Novos participantes podem ser convidados dentro da página do evento através do e-mail.
- Devem passar pelo fluxo de confirmação como qualquer outro convidado.

## Endpoints

- **Cadastro de Viagem**
  - `POST /trips`
- **Consulta de Viagem**
  - `GET /trips/{tripId}`

## Diagrama de Classe

![Diagrama de Classe]

```plaintext
+----------------+        +-----------------+        +----------------+
|     Trip       |        |     User        |        |    Activity    |
+----------------+        +-----------------+        +----------------+
| - id           |        | - id            |        | - id           |
| - destination  |        | - name          |        | - title        |
| - startDate    |        | - email         |        | - date         |
| - endDate      |        +-----------------+        | - time         |
+----------------+        |                 |        +----------------+
| + getId()      |        | + getId()       |        | + getId()      |
| + getName()    |        | + getName()     |        | + getTitle()   |
| + getEmail()   |        | + getEmail()    |        | + getDate()    |
+----------------+        +-----------------+        +----------------+
        |                         |                           |
        | 1                      1|                           |1
        |                         |                           |
        | *                       |                           |*
        |                         |                           |
+----------------+        +-----------------+        +----------------+
|   Invitation   |        | TripParticipant |        |    Link        |
+----------------+        +-----------------+        +----------------+
| - id           |        | - id            |        | - id           |
| - tripId       |        | - tripId        |        | - tripId       |
| - userId       |        | - userId        |        | - url          |
| - status       |        | - status        |        | - description  |
+----------------+        +-----------------+        +----------------+
| + getId()      |        | + getId()       |        | + getId()      |
| + getTripId()  |        | + getTripId()   |        | + getUrl()     |
| + getUserId()  |        | + getUserId()   |        | + getDescription|
| + getStatus()  |        | + getStatus()   |        +----------------+
+----------------+        +-----------------+
