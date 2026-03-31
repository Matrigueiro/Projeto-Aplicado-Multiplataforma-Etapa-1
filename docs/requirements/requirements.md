# Documentação de Requisitos - <!-- Nome do Projeto -->

# 1. Introdução

## 1.1 Visão Geral

O ** ResolveAqui ** é uma plataforma digital voltada para o registro, acompanhamento e resolução de demandas comunitárias.


## 1.2 Propósito

Este documento define os requisitos funcionais e não funcionais do
sistema, servindo como base para desenvolvimento, testes e manutenção.


## 1.3 Escopo

O sistema contempla:
- Gestão de usuários
- Registro de demandas
- Sistema de apoio às demandas
- Classificação por categorias
- Detecção de demandas semelhantes
- Atualização de status
- Comentários e feedback
- Relatórios administrativos

------------------------------------------------------------------------

# 2. Glossário

## 2.1 Termos de Domínio

| Termo | Definição |
|-------|-----------|
|  **Demanda** | Registro de um problema ou solicitação dentro de uma comunidade |
| **Apoio** | Confirmação de usuários indicando que reconhecem a mesma demanda |
| **Categoria** | Classificação do tipo de problema |
| **Localização** | Local onde a demanda ocorre |



## 2.2 Papéis (Roles)

| Role | Descrição |
|------|-----------|
| **user** | Usuário comum que cria demandas |
| **responsável** | Usuário responsável por resolver demandas |
| **admin** | Administrador com acesso completo ao sistema |



## 2.3 Status da Demanda

| Status | Descrição |
|--------|-----------|
| **aberta** | Demanda registrada |
| **lida** | Demanda visualizada pelo responsável |
| **pendente** | Demanda aceita pelo responsável |
| **em_andamento** | Demanda em processo de resolução |
| **resolvida** | Problema solucionado |
| **cancelada** | Demanda Rejeitada ( com motivo obrigatório) |

-------------------------------------------------------------------------

# 3. Requisitos Funcionais

## 3.1 Autenticação (RF-AUTH)

### RF-AUTH-001 Registro de Usuário
**Prioridade:** Essencial

O sistema deve permitir cadastro de novos usuários com:
- Nome (obrigatório 2-100 caracteres)
- Email (obrigatório, único, formato válido)
- Senha (obrigatório, mín. 6 caracteres, deve conter letra, número e caractere especial)
- Telefone (opcional, formato válido)



### RF-AUTH-002 Login
**prioridade:** Essencial

O sistema deve autenticar usuários via email e senha.

**Regras:**
- Credenciais inválidas retornam erro 401
- Retorna token de autenticação
- Atualiza último login



### RF-AUTH-003 Perfil do Usuário
**Prioridade:** Essencial

O sistema deve permitir visualizar os dados do usuário autenticado.

**Regras** Não retorna o campo senha



### RF-AUTH-004 Atualização de Senha
**Prioridade:** Importante

O sistema deve permitir alteração de senha do usuário autenticado.

**Regras:**
- Requer senha atual correta
- Nova senha deve atender critérios de validação
- Senha atual incorreta retorna erro 401



### RF-AUTH-005 Atualização de Perfil
**Prioridade:** Importante

O sistema deve permitir atualização de dados do perfil.

**Campos atualizáveis**
- Telefone

**Regras:**
- Requer senha atual correta

------------------------------------------------------------------------

## 3.2 Gestão de Demandas (RF-DEM)

### RF-DEM-001 Criar Demanda
**Prioridade:** Essencial

Usuários autenticados podem criar demandas.

**Campos obrigatórios:**
- Título (3-100 caracteres)
- Descrição (mín. 10 caracteres)
- Data do problema
- Categoria (deve existir e estar ativa)
- Localização (endereço, cidade, estado)

**Campos opcionais:**
- Imagem (formato URL válido)
- tags (máx. 10 tags, cada uma 3-30 caracteres)

**Regras:**
- Status inicial = aberta
- Demanda associada ao usuário criador



### RF-DEM-002 Detecção de Demandas Semelhantes
**Prioridade:** Essencial

Antes de registrar nova demanda, o sistema deve buscar demandas
semelhantes com base em:

- Título
- Descrição

Caso encontre demandas semelhantes:

- Exibir sugestões
- Permitir apoiar demanda existente



### RF-DEM-003 Listar Demandas (Busca Pública)
**Prioridade:** Importante

O sistema deve permitir listar demandas com filtros:

- Categoria
- Status
- Localização
- Texto de busca
- Tags
- Período/intervalo de datas

**Ordenação:**
- Data (asc/desc), recentes

**Paginação padrão:**
- 10 itens por página.

**Regras:**
- Público vê apenas: approvalStatus=approved AND status=active
- Retorna metadados de paginação e filtros aplicados



### RF-DEM-004 Visualizar Demanda
**Prioridade:** Essencial

O sistema deve permitir visualizar detalhes da demanda incluindo:

- Descrição
- Status
- Autor
- Número de apoios
- Comentários
- Histórico de atualização

**Regras:**
- Demandas pendentes/em andamento: acesso público
- Demandas abertas/lidas/canceladas: apenas responsável ou admin



### RF-DEM-005 Atualizar Status
**Prioridade:** Essencial

Responsáveis podem atualizar o status da demanda.

**Fluxos permitido:**
- aberta → lida → pendente → em_andamento → resolvida
- aberta → lida → cancelada




### RF-DEM-006 Cancelar Demanda
**Prioridade:** Essencial

Usuário criador ou administrador pode cancelar uma demanda.



### RF-DEM-007 Minhas Demandas
**Prioridade:** Essencial

O sistema deve listar demandas do usuário autenticado.

**Filtro:**
- Status
- Apoio

**Retorna:**
- Lista de demandas do usuário
- Contadores por status e apoios
- paginação

------------------------------------------------------------------------

## 3.3 Apoio às Demandas (RF-APO)

### RF-APO-001 Apoiar Demanda
**Prioridade:** Essencial

Usuários podem apoiar demandas existentes.

**Regras:**
- Um usuário pode apoiar apenas uma vez
- Apoio incrementa contador de reconhecimento da demanda



### RF-APO-002 Listar Demandas Mais Apoiadas
**Prioridade:** Essencial

O sistema deve permitir listar demandas com maior número de apoios.

------------------------------------------------------------------------

## 3.4 Comentários e Feedback (RF-COM)

### RF-COM-001 Comentários
**Prioridade:** Essencial

Usuários podem comentar em demandas.



### RF-COM-002 Feedback de Resolução
**Prioridade:** Essencial

Responsáveis podem adicionar feedback ao resolver uma demanda.

Exemplo:

"Lâmpada substituída pela equipe de manutenção."

------------------------------------------------------------------------

## 3.5 Gestão de Categorias (RF-CAT)

### RF-CAT-001 Listar Categorias
**Prioridade:** Essencial

Sistema deve listar categorias disponíveis.

**Exemplos:**
- Iluminação
- Estrutura
- Limpeza
- Segurança
- Equipamentos



### RF-CAT-002 Criar Categoria
**Prioridade:** Essencial

O sitema deve permitir a criação de categorias.

**Campos:**
- Nome (obrigatório, único, 2-50 caracteres)
- Descrição (opcional, máx. 200 caracteres)

**Regras:**
- Apenas admins podem criar
- Nome duplicado retorna erro 400



### RF-CAT-003 Editar Categoria
**Prioridade:** Essencial

O sistema deve permitir a edição de categorias.

**Regras:**
- Apenas admins podem editar
- Nome deve permanecer único



### RF-CAT-004 Excluir Categoria
**Prioridade:** Essencial

O sistema deve permitir a exclusão de categorias.

**Regras:**
- Apenas admins podem excluir
- Categorias associadas a demandas não podem ser excluídas

------------------------------------------------------------------------

## 3.6 Gestão de Usuários (RF-USR)

### RF-USR-001 Listar Usuários
**Prioridade:** Importante

O sistema deve listar usuários cadastrados.

**Regras:**
- Apenas admins têm acesso
- Senha nunca é retornada


### RF-USR-001 Visualizar Usuários
**Prioridade:** Importante

O sistema deve retornar detalhes de um usuário.

**Regras:**
- Apenas admins têm acesso
- Senha nunca é retornada


#### RF-USR-004: Excluir Usuário
**Prioridade:** Importante

O sistema deve permitir exclusão de usuários.

**Regras:**
- Apenas admins podem excluir
- Usuários com demandas ativas não podem ser excluídas

------------------------------------------------------------------------

# 4. Requisitos Não Funcionais

## Segurança

-   Autenticação baseada em JWT
-   Senhas armazenadas com hash bcrypt

## Performance

-   Tempo máximo de resposta: 3 segundos
-   Listagens com paginação

## Usabilidade

-   Interface responsiva (desktop, tablet, mobile)
-   Mensagens em português

------------------------------------------------------------------------

# 5. Regras de Negócio

RN-001: Demandas com maior número de apoios devem receber maior
prioridade.

RN-002: Responsáveis só podem gerenciar demandas da unidade atribuída.

RN-003: O sistema deve sugerir demandas semelhantes antes da criação de
novas.

------------------------------------------------------------------------

# 6. Casos de Uso

## UC-001 Criar Demanda

1.  Usuário preenche dados
2.  Sistema verifica demandas semelhantes
3.  Usuário confirma criação
4.  Demanda é registrada

## UC-002 Apoiar Demanda

1.  Usuário visualiza demanda
2.  Clica em apoiar
3.  Sistema registra apoio
4.  Contador é atualizado

## UC-003 Atualizar Status

1.  Responsável acessa demanda
2.  Atualiza status
3.  Usuários acompanham atualização

------------------------------------------------------------------------

# 7. Matriz de Permissões

| Ação | Usuário | Responsável | Admin |
|------|---------|-------------|-------|
| Criar demanda | ✅ | ✅ | ✅ |
| Apoiar demanda | ✅ | ✅ | ✅ |
| Comentar | ✅ | ✅ | ✅ |
| Atualizar status | - | ✅ | ✅ |
| Gerenciar categorias | - | - | ✅ |
| Gerenciar usuários | - | - | ✅ |
| Visualizar relatórios | - | ✅ | ✅

------------------------------------------------------------------------

# 8. Validações de Dados

## Usuário

| Campo | Regra |
|-------|-------|
| Nome | 2 a 100 caracteres |
| Email | formato válido e único |
| Senha | mínimo 6 caracteres |

## Demanda

| Campo | Regra |
|-------|-------|
| Titulo | 3 a 100 caracteres |
| Descricao | mínimo 10 caracteres |
| Categoria | obrigatória |

