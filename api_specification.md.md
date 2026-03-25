# Especificação de API - <!-- Nome do Projeto -->

## 1. Visão Geral

A API do sistema **<!-- Nome do Projeto -->** segue o padrão RESTful, utilizando
JSON para comunicação entre cliente e servidor.

Base URL: http://localhost:3000/api

------------------------------------------------------------------------

## 2. Autenticação

Autenticação via JWT.

Header obrigatório: Authorization: Bearer `<token>`{=html}

------------------------------------------------------------------------

## 3. Endpoints

## 3.1 Autenticação

### POST /auth/register
Cria um novo usuário.

#### Request Body
```json
{
  "nome": "Arthur Oliveira",
  "email": "arthur@email.com",
  "senha": "Senha@123",
  "telefone": "85999999999"
}
```

#### Response (201)
```json
{
  "id": "uuid",
  "email": "arthur@email.com"
}
```


### POST /auth/login
Autentica usuário.

#### Request Body
```json
{
  "email": "arthur@email.com",
  "senha": "Senha@123"
}
```

#### Response (200)
```json
{
  "token": "jwt_token"
}
```


### GET /auth/me
Retorna dados do usuário autenticado.

#### Autenticação
Bearer Token obrigatório

#### Response (200)
```json
{
  "id": "uuid",
  "nome": "Arthur Oliveira",
  "email": "arthur@email.com"
}
```


## 3.2 Demandas

### POST /demands
Cria uma nova demanda.

#### Autenticação
Obrigatória

#### Request Body
```json
{
  "titulo": "Buraco na rua",
  "descricao": "Buraco grande na via",
  "data_problema": "2026-03-20",
  "categoria_id": "uuid",
  "localizacao": {
    "endereco": "Rua A",
    "cidade": "Fortaleza",
    "estado": "CE"
  },
  "imagem": "https://imagem.com/foto.jpg",
  "tags": ["infraestrutura"]
}
```

#### Response (201)
```json
{
  "id": "uuid",
  "status": "aberta"
}
```


### GET /demands
Lista demandas.

#### Query Params

| Parâmetro | Tipo | Descrição |
|----------|------|----------|
| status | string | Filtrar por status |
| categoria | string | Filtrar por categoria |
| page | number | Página |
| limit | number | Itens por página |

#### Response (200)
```json
{
  "data": [],
  "meta": {
    "page": 1,
    "total": 50
  }
}
```


### GET /demands/:id
Retorna detalhes de uma demanda.

#### Response (200)
```json
{
  "id": "uuid",
  "titulo": "Buraco na rua",
  "descricao": "Detalhes...",
  "status": "aberta"
}
```


### PUT /demands/:id/status
Atualiza status da demanda.

#### Autenticação
Responsável/Admin

#### Request Body
```json
{
  "status": "Em andamento"
}
```

#### Response (200)
```json
{
  "mensagem": "Status atualizado"
}
```


### DELETE /demands/:id
Cancela uma demanda.

#### Response (200)
```json
{
  "mensagem": "Demanda cancelada"
}
```



## 3.3 Apoios

### POST /demands/:id/support
Apoiar uma demanda.

#### Response (200)
```json
{
  "mensagem": "Apoio registrado"
}
```


### GET /demands/:id/supports
Lista apoios de uma demanda.

#### Response (200)
```json
{
  "total": 10
}
```



## 3.4 Comentários

### POST /comments
Cria um comentário.

#### Request Body
```json
{
  "demanda_id": "uuid",
  "conteudo": "Isso também acontece aqui"
}
```


### GET /demands/:id/comments
Lista comentários.



## 3.5 Categorias

### GET /categories
Lista categorias.


### POST /categories
Cria categoria (admin).

#### Request Body
```json
{
  "nome": "Iluminação",
  "descricao": "Problemas com luz pública"
}
```


### PUT /categories/:id
Atualiza categoria.


### DELETE /categories/:id
Remove categoria.



## 3.6 Usuários

### GET /users
Lista usuários (admin).


### PUT /users/:id
Atualiza usuário.


### DELETE /users/:id
Remove usuário.

------------------------------------------------------------------------

## 4. Códigos de Resposta

| Código | Descrição |
|--------|-----------|
| 200 | Sucesso |
| 201 | Criado |
| 400 | Erro de validação |
| 401 | Não autorizado |
| 403 | Proibido |
| 404 | Não encontrado |

------------------------------------------------------------------------

## 5. Considerações Finais

A API foi projetada para ser simples, escalável e compatível com
aplicações web e mobile.
