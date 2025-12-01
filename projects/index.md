
## Estrutura

- Framework
- DB
- Migration
- Repositry
- Entity ID
- ErrorResponse
- Validator
- Mapper
- Exception + Handlers

## Quarkus

### 104 - Conhecimento

- DDD (struct)
- Quarkus
- DB H2
- Entity
  - id UUID
  - Métodos moanuais
  -
- Repository Panache
- ErrorResponse
  - sem `status`
- Validator
  - DI (annotation)
  - Constraints (FieldMatch LeghtExact, RageDate)
- Mapper
  - Manual
- Messages
  - Manual com properties
- Facades
  - Acesso estático ao container a configs, mensagens e validações (estilo laravel)
- Paginação
  - TODO - rever
- DTOs muito amarrados
- Util
  - Collection, Container, File, Http, Json, Map, Object
- ControllerBase

### 106 - Panache (ORM)

- Quarkus
- DB Postgres
- Entity
  - Id Long
  - Lombok
  - Person, Category, Post, Comment
- ErrorResponse
  - sem `status`
- Validator
  - DI (annotation)
  - Métodos: (getViolations, validate)
- Mapper
  - ModelMapper
  - MapperBase (Abstract)
  - Repository injetado
- Repository Panache

---

### 101 - BACKEND-JAVA

- DDD
- Spring Boot
- DB Postgres
- Flyway
- Swagger/OpenAPI
- Validator
  - Injeção interna
  - Métodos: (check, validate)
- Exceptions + Handlers
- Util (Collection, Json)
- ErrorResponse com `status`
- Entity
  - Id UUID
  - Métodos manuais
  - Role, User, Category, Product
- Spring Auth + JWT

---

- Security + Jwt
- Mapper > Manual
- Entities (Role, User, Category, Product)
- Tests (Mockito, Jacoco, JavaFaker)

### desafio.recargapay

- Spring Boot
- Postgres
- Flyway
- Swagger/OpenAPI

---

- Constants (API, Message)
- Validator (check, validate)
- Exceptions + Handlers
- Util (Json)
- ErrorResponse
- Entity UUID
- Mapper -> ModelMapper (MapperBase)

---

- Security + Jwt
- Entities: Role (RoleEnum), User, Wallet, WalletBalance, Transaction (TransactionTypeEnum)
- Enums mapeados
- Converters (Enum to Table)
- Tests (Mockito, Jacoco + ServiceTestBase)
- Aspects (Log)

### 111 - SHORTNER URL

- Spring Boot
- Postgres
- Flyway
- Swagger/OpenAPI

---

- Constants (Message)
- Validator (check, validate)
- Exceptions
- Util (Json)
- ErrorResponse

---

- Entities: User, Url
- Mapper -> ModelMapper (Config)

---

### 108 - message

- Spring Boot

---

### 107 - LOCALIDADES (NAO É REFERENCIA)

- Quarkus

### 110 - CACHE (NÂO É REFERENCIA)

- Spring
- Cache

### 112 - WebFlux + Reativo

- ad

---

### 101

### 110

### 111

### 112

### desafio
