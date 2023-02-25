# Core

Projeto que concentrará todos os classes bases e implementações comuns para outros projetos.

```bash
/core
  /communication                #
  /domain                       # Objetos de Domínio
    EntityBase.java             #
    IAggregateRoot.java         #
    IEntity.java                #
  /dto                          # Objeto de transferência de Dados | Data Transfer Objects
    ErrorResponse.java          #
    RequestBase.java            # Objeto base para criação de Requests
    ResponseBase.java           # objeto base para croação de Responses
    SuccessResponse.java        #
  /exception                    # Exceptions
    ApplicationException.java   # Exceção para erros no sistema em geral (As demais exceptions devem extender este)
    PersistenceException.java   # Exceção para erros de persistência
    SecurityException.java      # Exceção para erros de segurança
    ValidationException.java    # Exceção para erros de validação
  /util                         # Utilitários
    ColletionUtils.java         # Utilitários para Collections
  /validation                   # Validação de objetos
    IValidator.java             # Interface Validator
    Validator.java              # Implementação de Validator
```
