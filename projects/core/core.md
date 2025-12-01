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
    RequestBase.java            # Objeto base para criação de Requests
    ResponseBase.java           # objeto base para croação de Responses
    ErrorResponse.java          # DTO de Erros
    SuccessResponse.java        # DTO de Resposta
    GenericResponse.java        # DTO de resposta genérica (sucesso ou falha)
    StandardResponse.java
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

## Domain

```java

// User -----------------------------------------

public class Role {
	  private UUID id; (pode ser long)
    private String name;
    private String description;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
    // --
    private Set<Role> childRoles = new HashSet<>();
    private Set<Role> parentRoles = new HashSet<>();
}

public class User {
	  private UUID id; (pode ser long)
    private String name;
    private String email;
    private String password;
    private UserStatus status = UserStatus.INACTIVE;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
    // --
  	private Set<Role> roles = new HashSet<>();
}

// E-commerce -----------------------------------

public class Category {
    private UUID id; (pode ser long)
    private String name;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
}

public class Product {
    private UUID id; (pode ser long)
    private Category category;
    private String name;
    private String description;
    private String image;
    private Boolean active;
    private BigDecimal value;
    private Integer quantity;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
}


// Posts ----------------------------------------

public class Person {
    private Long id;
    private String name;
    private String personalNumber;
    private LocalDate dateBirthday;
    private String email;
    // --
    private List<Comment> comments = new ArrayList<>();
    private List<Post> posts = new ArrayList<>();
}

public class Category {
    private Long id;
    private String name;
    private String description;
    // --
    private List<Post> posts = new ArrayList<>();
}

public class Post {
    private Long id;
    private Category category;
    private String title;
    private String text;
    private Person author;
    // --
    private List<Comment> comments = new ArrayList<>();
}

public class Comment {
    private Long id;
    private Post post;
    private Person author;
    private String text;
}

```
