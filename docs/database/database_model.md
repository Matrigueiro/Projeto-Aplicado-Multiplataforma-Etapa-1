# Modelo de Banco de Dados - <!-- Nome do Projeto -->

## 1. Visão Geral

O banco de dados do sistema **<!-- Nome do Projeto -->** é responsável por
armazenar informações relacionadas a usuários, demandas, apoios e
interações.

O modelo segue o padrão relacional utilizando PostgreSQL.

------------------------------------------------------------------------

## 2. Entidades Principais

- Usuario
- Demanda
- Categoria
- Apoio
- Comentario

------------------------------------------------------------------------

## 3. Descrição das Entidades

## 3.1 Usuario

| Campo | Tipo | Descrição |
|-------|------|-----------|
| id | UUID | Identificador único |
| nome | VARCHAR | Nome do usuário |
| email | VARCHAR | Email único |
| senha | VARCHAR | Senha criptografada |
| role | VARCHAR | Perfil (user, responsavel, admin) |
| created_at | TIMESTAMP | Data de criação |



## 3.2 Demanda

| Campo | Tipo | Descrição |
|-------|------|-----------|
| id | UUID | Identificador |
| titulo | VARCHAR | Título da demanda |
| descricao | TEXT | Descrição |
| status | VARCHAR | Status da demanda |
| usuario_id | UUID | Criador |
| categoria_id | UUID | Categoria |
| created_at | TIMESTAMP | Data |



## 3.3 Categoria

| Campo | Tipo | Descrição |
|-------|------|-----------|
| id | UUID | Identificador |
| nome | VARCHAR | Nome da categoria |



## 3.4 Apoio

| Campo | Tipo | Descrição |
|-------|------|-----------|
| id | UUID | Identificador |
| usuario_id | UUID | Usuário |
| demanda_id | UUID | Demanda |

Regra: - Um usuário só pode apoiar uma vez por demanda



## 3.5 Comentario

| Campo | Tipo | Descrição |
|-------|------|-----------|
| id | UUID | Identificador |
| conteudo | TEXT | Comentário |
| usuario_id | UUID | Autor |
| demanda_id | UUID | Demanda |
| created_at | TIMESTAMP | Data |

------------------------------------------------------------------------

## 4. Relacionamentos

- Usuario 1:N Demanda
- Usuario N:N Demanda (via Apoio)
- Demanda 1:N Comentario
- Categoria 1:N Demanda

------------------------------------------------------------------------

## 5. Regras de Integridade

- Email deve ser único
- Apoio único de usuário por demanda
- Categoria é obrigatória na demanda

------------------------------------------------------------------------

## 6. Diagrama ER

<img src="Diagrama ER.png" width="200" height="100">

------------------------------------------------------------------------

## 7. Considerações Finais

Modelo preparado para expansão futura com novas entidades como anexos,
notificações e histórico.
