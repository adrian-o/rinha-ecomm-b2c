# Rinha de Backend Ecoomm B2C
Criado para simular uma rinha de backend interna no time de Ecomm B2C da Vivo, a fim de experimentarmos novas tecnologias além das que já usamos internamente e trazermos ao time um senso de comunidade.

A rinha é uma brincadeira com fins de aprendizado e foi completamente inspirada na versão aberta da Rinha de Backend realizada na Rede Social X: https://github.com/zanfranceschi/rinha-de-backend-2024-q1

A fim de mantermos o espírito da brincadeira mas trazermos para dentro da nossa estrutura, mudaremos a API a ser desenvolvida e testada. A seguir, vamos definir as diretrizes do desafio.

## A API que precisa ser desenvolvida
Para deixarmos a rinha em um desafio mais "ECOMM", a ideia é construirmos as seguintes APIs 

- GET /user/{id}  -> Recupera um usuário
- POST /user      -> Cria um usuário
- POST /product   -> Cria um produto
- GET  /cart/{id} -> Recupera um carrinho
- POST /cart      -> Cria um carrinho já com todos os produtos inseridos no body
- PUT  /cart      -> Atualiza o carrinho com um novo produto

### Entidades
Seguem dados das entidades que devem ser mapeados para a API:
#### User
-  Id Integer (required)
-  Name String (150) (required)
-  Birthday Date (required)
-  Username String (50) (required)
-  Password String (60) Bcrypt hash (required)

#### Product
-  Id Integer (required)
-  Name String (150) (required)
-  StockQuantity Integer (required)
-  Price Numeric (required)

#### Cart
-  Id Integer (required)
-  User (required)
-  Products (required)
    - Quantity Integer (required)
    - Price Numeric (required)
      
### Regras para GETs
- 200 para entidade encontrada
- 404 para entidade não encontrada
- Todos os dados da entidade devem ser retornados no body da response

### Regras para POSTs
- 201 para dados inseridos com sucesso
- 400 para dados incorretos 
- 422 para dados incompletos

### Regras para PUTs
- 201 para dados inseridos com sucesso
- 400 para atualização de campos que não devem ser alterados

## REGRAS GERAIS
- A aplicação deve ser entregue com possibilidade de ser executada completa na máquina do avaliador, sendo assim, fica definido o uso de um docker-compose para subir a API junto com o banco de dados e/ou outros recursos que o participante queira utilizar. Exemplo...
- Deve ser utilizado pelo menos 1 database a critério do participante
- Não deve ser possível cadastrar um usuário menor de idade, devendo retornar no caso um 404 com a mensagem  "The person is a minor"
- Não deve ser possível cadastrar um usuário sem que o mesmo forneça todas as suas informações requeridas (Name, Birthday, Username e Passwaord), devendo retornar um HTTP Status 400 com a mensagem "Missing required(s) field(s)"  
- Para fins didádicos, a senha de usuário deve vir descriptografada e ser criptografada (usando o Bcrypt como criptografia) antes do salvamento no database
- Não deve ser possível cadastrar um produto com estoque menor que 0, devendo retornar no caso um 404 com a mensagem "The stock must be 0 or bigger"
- Não deve ser possível cadastrar um produto sem passar todas as suas informações requeridas (Name, StockQuantity, e Price), devendo retornar um HTTP Status 400 com a mensagem "Missing required(s) field(s)"
- Não deve ser possível cadastrar um produto com preço menor ou igual a 0, devendo retornar no caso um 404 com a mensagem "The product must have a price greater than 0"
- Não deve ser possível comprar um produto que a quantidade do estoque ao final da operação venha a ser menor que zero. Exemplo: Iphone5 possui 5 em seu campo StockQuantity e o POST/PUT do carrinho está tentando inserir 6 na compra. A operação inteira deve ser impossibilitada
- Não deve ser possível criar um carrinho sem um usuário, devendo retornar um HTTP Status 400 com a mensagem "User is required"
- Não deve ser póssível criar um carrinho sem pelo menos um produto, devendo retornar um HTTP Status 400 com a mensagem "Product is required"

## Critérios de avaliação
Para avaliar a execução das APIs, faremos um load test utilizando a ferramenta ... que irá acessar os endpoints disponíveis e avaliar os retornos esperados. O test será o mesmo para todos os repositórios avaliados e o resultado será a média de 5 execuções, a fim de diminuir o risco de distorções.

## Como executar os testes no local
...

## Datas e prazos
- A rinha terá um prazo de entrega no dia ../../2024
- Faremos uma cerimônia de agradecimento e confraternização (online e presencial) na data de ../../2024
