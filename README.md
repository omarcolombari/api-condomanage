<h1 align='center'> Api Condo Manage </h1>

# **Rotas que não precisam de autenticação**

<h2 align ='center'> Cadastro de usuários </h2>

Este endpoint /register, irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password. Você pode adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

`POST /register - FORMATO DA REQUISIÇÃO`
```json
{
	"email": "teste@teste.com",
	"password": "123456",
	"name": "Condominio Milenius",
	"cnpj": "xxxxxxxxxxx",
	"cpf": "xxxxxxxxxxx",
	"valueBase" : "380.00",
	"complement" : "Predio",
	"address": "Rua Professor Raimundo"
}
```

Se tudo der certo, essa será a resposta:

`POST /register - FORMATO DA RESPOSTA - STATUS 201`

```json
{
	"accessToken": "xxxxxxxx.xxxxxxxx.xxxxxxxx",
	"user": {
		"email": "teste@teste.com",
		"id": 1 
	}
}
```

<h2 align ='center'> Login </h2>

Neste endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de usuários.

`POST /login - FORMATO DA REQUISIÇÃO` 
```json
{
	"email": "teste@teste.com",
	"password": "123456"
}
```
Se tudo der certo, essa será a resposta:

`POST /login - FORMATO DA RESPOSTA - STATUS 200`
```json
{
	"accessToken": "xxxxxxxx.xxxxxxxx.xxxxxxxx",
	"user": {
		"email": "Ronaldo@testgmail.com",
		"name": "Condominio Milenius",
		"cnpj": "xxxxxxxxxxx",
		"cpf": "xxxxxxxxxxx",
		"valueBase": "380.00",
		"complement": "Prédio",
		"address": "Rua Professor Raimundo",
		"id": 3
	}
}
```

# **Rotas que precisam de autenticação***
## *Nessas rotas é necessario infomar no corpo da requisição o id em que você está logado, passe-o como "UserId". E também o seu token no header.*
### Por exemplo:
```json
{
	"userId": 1
}
```


<h2 align ='center'> Cadastro de moradores </h2>

Somente o usuário logado, que no caso sera o sindico, pode registrar um novo morador.

`POST /tenants - FORMATO DA REQUISIÇÃO`
```json
{
	"name": "José",
	"email":"jose@gmail.com",
	"userId": 1,
	"password": "123456",
	"number": "402",
	"responsible": "Maria",
	"cpf":"xxxxxxxxxx",
	"value": 1000,
	"status": "Comprado"
}
```

O síndico também pode alterar esses dados utilizando este endpoint: 

`PUT /tenants/:tenant_id - FORMATO DA REQUISIÇÃO`
```json
{
	"name": "Mario",
	"email": "mario@gmail.com"
}
```

Também é possivel deletar o morador, utilizando este endpoint:

`DELETE /tenants/:tenent_id`
```
Não é necessário um corpo de requisição
```

<h2 align ='center'> Cadastro do financeiro </h2>

Cadastre suas entradas e saidas finaceiras do prédio.

`POST /finances - FORMATO DE REQUISIÇÃO`

```json
{
	"name": "mensalidade condominio",
	"value": "380",
	"status": "Entrada",
	"userId": 3
}
```
`POST /finances - FORMATO DA RESPOSTA - STATUS 201`
```json
{
	"name": "Mensalidade apartamento 10",
	"value": 380,
	"status": "Entrada",
	"userId": 3,
	"id": 1
}
```

`GET /finances - FORMATO DA RESPOTA - 200`
```json
[
	{
		"name": "Mensalidade apartamento 10",
		"value": 380,
		"status": "Entrada",
		"userId": 3,
		"id": 1
	},
	{
		"name": "Reparo no apartamento 23",
		"value": 380,
		"status": "Saida",
		"userId": 3,
		"id": 2
	}
]
```

`DELETE /finances/:finance_id `

```
Não é necessário um corpo de requisição
```

<h2 align ='center'> Alterar dados do prédio </h2>

Para alterar os dados de sua conta, voce deve inserir email e password no corpo da requisição e utilizar este endpoint

`PUT /users/:user_id - FORMATO DA REQUISIÇÃO`
```json
{
	"name": "mensalidade condominio",
	"value": "380",
	"status": "Entrada",
	"userId": 3
}
```
`PUT /users/:user_id - FORMATO DA RESPOSTA - STATUS 200`
```json
{
	"name": "mensalidade condominio",
	"value": "380",
	"status": "Entrada",
	"userId": 3,
	"id": 1
}
```

<h2 align ='center'> Adicionar demandas do prédio </h2>

Utilize este endpoint para adicionar demandas relacionados ao prédio, por exemplo: Cobranças e manutenções.

`POST /demands - FORMATO DA REQUISIÇÃO`
```json 
{
	"description": "Cobrar 14 meses de aluguel",
	"status": "Dependete",
	"valor" : 14.000,
	"userId": 1
}
```

`POST /demands - FORMATO DA REPOSTA - 201`
```json 
{
	"description": "Cobrar 14 meses de aluguel",
	"status": "Dependete",
	"valor": 14.000,
	"userId": 1,
	"id": 1
}
```

Para ver as demandas, utilize este endpoint:

`GET /demands - FORMATO DA RESPOSTA - 200` 
```json
[
	{
		"description": "Cobrar 14 meses de aluguel",
		"status": "Dependete",
		"valor" : 14000,
		"userId": 1,
		"id": 1
	},
	{
		"description": "Pintar as escadas",
		"status": "Ok",
		"valor" : 2000,
		"userId": 1,
		"id": 2
	}
]
```

`PUT /demands/;demand_id - FORMATO DA REQUISIÇÃO - 201`
```json
{
	"status": "Ok",
}
```

`PUT /demands/:demand_id - FORMATO DA REQUISIÇÃO - 201`
```json
{
	"status": "Ok",
}
```

`DELETE /demands/:demand_id`
```
Não é necessário um corpo da requisição.
```