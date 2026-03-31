# Arquitetura do Sistema - <!-- Nome do Projeto -->

## 1. Visão Geral

O **ResolveAqui** é uma plataforma digital voltada para o registro, acompanhamento e resolução de demandas comunitárias.

A arquitetura segue o padrão **cliente-servidor** com separação em
camadas.

------------------------------------------------------------------------

## 2. Estilo Arquitetural

- Arquitetura em camadas (Layered Architecture)
- API RESTful
- Separação entre frontend, backend e banco de dados

------------------------------------------------------------------------

## 3. Componentes do Sistema

### 3.1 Frontend

Responsável pela interface com o usuário.

Tecnologias sugeridas: 
- React.js (Web) 
- React Native (Mobile)

Funções: 
- Login e autenticação 
- Cadastro de demandas 
- Visualização de demandas 
- Apoio às demandas 
- Comentários



### 3.2 Backend

Responsável pela lógica de negócio.

Tecnologias sugeridas: 
- Node.js com Express

Funções: 
- Autenticação (JWT) 
- Processamento de regras de negócio 
- Controle de permissões (RBAC) 
- Detecção de demandas semelhantes 
- Gerenciamento de dados



### 3.3 Banco de Dados

Responsável pelo armazenamento de dados.

Tecnologia sugerida: 
- PostgreSQL

Principais entidades: 
- Usuários 
- Demandas 
- Apoios 
- Categorias 
- Comentários

------------------------------------------------------------------------

## 4. Diagrama de Arquitetura

Usuário → Frontend → API Backend → Banco de Dados

<img src="Diagrama de Arquitetura.png">

------------------------------------------------------------------------

## 5. Padrões Utilizados

- REST
- MVC
- RBAC
- JWT

------------------------------------------------------------------------

## 6. Decisões Técnicas

- API REST para integração futura
- PostgreSQL pela robustez
- Busca por similaridade (LIKE inicialmente)

------------------------------------------------------------------------

## 7. Escalabilidade

- Backend escalável
- Banco com índices

------------------------------------------------------------------------

## 8. Segurança

- JWT
- bcrypt
- Controle por perfil

------------------------------------------------------------------------

## 9. Considerações Finais

Arquitetura simples, escalável e adequada para impacto social.
