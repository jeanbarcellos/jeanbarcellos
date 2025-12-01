Documentação docker

- `docker-compose.yml`

  Arquivo base que defina a configuração canônica dos serviços

  ```yml
  web:
    image: example/my_web_app:latest
    depends_on:
      - db
      - cache

  db:
    image: postgres:latest

  cache:
    image: redis:latest
  ```

- `docker-compose.override.yml`

  Quando você executa docker compose up, ele lê as substituições automaticamente.

  ```yml
  web:
    build: .
    volumes:
      - ".:/code"
    ports:
      - 8883:80
    environment:
      DEBUG: "true"

  db:
    command: "-d"
    ports:
      - 5432:5432

  cache:
    ports:
      - 6379:6379
  ```

- `docker-compose.prod.yml`

  Agora, seria bom usar este aplicativo Compose em um ambiente de produção. Portanto, crie outro arquivo de substituição (que pode ser armazenado em um repositório git diferente ou gerenciado por uma equipe diferente).

  ```yml
  web:
    ports:
      - 80:80
    environment:
      PRODUCTION: "true"

  cache:
    environment:
      TTL: "500"
  ```

  Para implantar com este arquivo Compose de produção, você pode executar

  ```bash
  docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d
  ```

  Isso implanta todos os três serviços usando a configuração em docker-compose.ymle docker-compose.prod.yml(mas não a configuração dev em docker-compose.override.yml).

<br>
<br>
