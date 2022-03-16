# api-condomanage
Url base :

### Cadastro
*POST /register

Este endpoint /register, irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password. Você pode adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

Exemplo de cadastro de Condominio
# Exemplo : {
    "email": "Ronaldo@testgmail.com",
	"password": "123456",
    "name": "Condominio Milenius",
    "cnpj": "00000000",
    "cpf": "0000000",
    "valueBase" : "380.00",
    "complement" : "Predio",
    "address": "rua professor raimundo"

    }

# Resposta :
    {
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlM0B0ZXN0Z21haWwuY29tIiwiaWF0IjoxNjQ3Mzg3MzE2LCJleHAiOjE2NDczOTA5MTYsInN1YiI6IjMifQ.v6FjvFybUrIhaFh38EwyfpqpcRt4CjkD3wRAqNVzpvc",
	"user": {
		"email": "Ronaldo@testgmail.com",
		"id": 3
	}
}

### Login
*POST /login

Neste endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users".

# Exemplo :  {
            "email": "Ronaldo@testgmail.com",
            "password": "123456"
         }



# Resposta :
    {
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlM0B0ZXN0Z21haWwuY29tIiwiaWF0IjoxNjQ3Mzg3MzE2LCJleHAiOjE2NDczOTA5MTYsInN1YiI6IjMifQ.v6FjvFybUrIhaFh38EwyfpqpcRt4CjkD3wRAqNVzpvc",
	"user": {
		"email": "Ronaldo@testgmail.com",
		"name": "Condominio Milenius",
		"cnpj": "00000000",
		"cpf": "0000000",
		"valueBase": "380.00",
		"complement": "Predio",
		"address": "rua professor raimundo",
		"id": 3
	}
}

### Tenants

*POST/tenants
Somente o usuario Logado pode registrar um novo morador. ELE VAI PRECISAR DO BEARER TOKEN NA REQUISICAO .

# Exemplo :  {
            "email":"jose@gmail.com",
            "password": "123456",
            "number": "402",
            "responsible": "maria",
            "cpf":"101010101",
            "value":"10142",
            "status": "Comprado"
         }

*GET /tenants 
Todos pode ver estas informacoes atraves deste endpoint. nao e necessario o token.

*PUT /tenants
Nesta requisicao sera necessario passar o token no corpo da requisicao,e os valores a serem alterados(Voce pode alterar qualquer valor menos o id) . e passar na url o id do morador. no exemplo o id 1 do morador que tem esse id. ex : http://localhost:3001/tenants/1

*DELETE /tenants
Nesta requisicao sera necessario passar o token no corpo da requisicao,e passar na url o id do morador. no exemplo o id 1 do morador que tem esse id. ex : http://localhost:3001/tenants/1

### Finance

O usuario precisa esta logado pra ler os dados e gravar novos dados.

*POST/ finance  
para cadastrar um novo valor e necesario na requisicao passa o bearer token, e uma referencia do id do usuario ::ex{"userId": 3}

# Exemplo :{
	"name": "mensalidade condominio",
	"value": "380",
	"status": "Entrada",
	"userId": 3
    }

# Resposta :
{
	"name": "mensalidade condominio",
	"value": "380",
	"status": "Entrada",
	"userId": 3,
	"id": 1
}

*GET / finance
Para acessa os dados e nessario passar o Bearer Token no corpo da requisicao

*PUT /tenants
Nesta requisicao sera necessario passar o token no corpo da requisicao,e os valores a serem alterados(Voce pode alterar qualquer valor menos o id) . e passar na url o id do morador. no exemplo o id 1 do morador que tem esse id. ex : http://localhost:3001/tenants/1

*DELETE /tenants
Nesta requisicao sera necessario passar o token no corpo da requisicao,e passar na url o id do morador. no exemplo o id 1 do morador que tem esse id. ex : http://localhost:3001/tenants/1

### Settings

O usuario precisa esta logado pra ler os dados e gravar novos dados.

*POST/ settings
para cadastrar um novo valor e necesario na requisicao passa o bearer token, e uma referencia do id do usuario ::ex{"userId": 3}

# Exemplo :{
	"name": "mensalidade condominio",
	"value": "380",
	"status": "Entrada",
	"userId": 3
    }

# Resposta :
{
	"name": "mensalidade condominio",
	"value": "380",
	"status": "Entrada",
	"userId": 3,
	"id": 1
}

*GET / settings
Para acessa os dados e nessario passar o Bearer Token no corpo da requisicao

*PUT /tenants
Nesta requisicao sera necessario passar o token no corpo da requisicao,e os valores a serem alterados(Voce pode alterar qualquer valor menos o id) . e passar na url o id do morador. no exemplo o id 1 do morador que tem esse id. ex : http://localhost:3001/tenants/1

*DELETE /tenants
Nesta requisicao sera necessario passar o token no corpo da requisicao,e passar na url o id do morador. no exemplo o id 1 do morador que tem esse id. ex : http://localhost:3001/tenants/1


### demands
*POST/demands

Somente o usuario Logado pode registrar uma nova demanda . ELE VAI PRECISAR DO BEARER TOKEN NO CORPO DA REQUISICAO .

# Exemplo :  {
            "description":"cobrar 14 meses de aluguel",
            "status": "Dependete",
			"valor" : "14.000"
         	}

*GET /demands 
Todos pode ver estas informacoes atraves deste endpoint.

*PUT /tenants
Nesta requisicao sera necessario passar o token no corpo da requisicao,e os valores a serem alterados(Voce pode alterar qualquer valor menos o id) . e passar na url o id do morador. no exemplo o id 1 do morador que tem esse id. ex : http://localhost:3001/tenants/1

*DELETE /tenants
Nesta requisicao sera necessario passar o token no corpo da requisicao,e passar na url o id do morador. no exemplo o id 1 do morador que tem esse id. ex : http://localhost:3001/tenants/1
