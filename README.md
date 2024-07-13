## Objetivo: PicPay Simplificado

No PicPay Desafio Backend, você deve criar uma plataforma de pagamentos simplificada. Nela, deve ser possível cadastrar usuários, depositar e realizar transferências de dinheiro entre usuários. Além disso, deve haver dois tipos de usuários: comuns e lojistas. Ambos possuem uma carteira com dinheiro e podem realizar transferências entre si.

### Requisitos

A seguir estão algumas regras de negócio que são importantes para o funcionamento do PicPay Simplificado:

- Para ambos tipos de usuário, precisamos do `Nome Completo`, `CPF`, `e-mail` e `Senha`. CPF/CNPJ e e-mails devem ser
  únicos no sistema. Sendo assim, seu sistema deve permitir apenas um cadastro com o mesmo CPF ou endereço de e-mail;

- Usuários podem enviar dinheiro (efetuar transferência) para lojistas e entre usuários;

- Lojistas **só recebem** transferências, não enviam dinheiro para ninguém;

- Validar se o usuário tem saldo antes da transferência;

- Antes de finalizar a transferência, deve-se consultar um serviço autorizador externo, use este mock
  [https://util.devi.tools/api/v2/authorize](https://util.devi.tools/api/v2/authorize) para simular o serviço
  utilizando o verbo `GET`;

- A operação de transferência deve ser uma transação (ou seja, revertida em qualquer caso de inconsistência) e o
  dinheiro deve voltar para a carteira do usuário que envia;

- No recebimento de pagamento, o usuário ou lojista precisa receber notificação (envio de email, sms) enviada por um
  serviço de terceiro e eventualmente este serviço pode estar indisponível/instável. Use este mock
  [https://util.devi.tools/api/v1/notify)](https://util.devi.tools/api/v1/notify)) para simular o envio da notificação
  utilizando o verbo `POST`;

- Este serviço deve ser RESTFul.

### Endpoint de cadastro

Cadastro de usuários. A implementação deve seguir o modelo a abaixo.

```http request
POST /users
Content-Type: application/json

{
  "firstName": "Pedro",
  "lastName": "Rufino",
  "document": "159753456",
  "email": "pedro@example.com",
  "password": "mudar123",
  "userType": "COMMON",
  "balance": 10
}
```

### Endpoint de verificação de usuários

Verificações de usuários na API. A implementação deve seguir o modelo a abaixo.

```http request
GET /users
Content-Type: application/json
```

### Endpoint de transferência

Transferência entre dois usuários. A implementação deve seguir o modelo a abaixo.

```http request
POST /transactions
Content-Type: application/json

{
  "senderId": 2,
  "receiverId": 1,
  "value": 10
}
```

### Tecnologias Utilizadas
- Java 17
- SpringBoot 3.3.1
- Spring Boot DevTools
- Spring Data JPA
- Spring Web
- H2 Database
- Lombok
- Maven
