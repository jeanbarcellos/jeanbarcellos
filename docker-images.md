# Docker - Images

## Maven

Apache Maven é uma ferramenta de gerenciamento e compreensão de projetos de software. Com base no conceito de um modelo de objeto de projeto (POM), o Maven pode gerenciar a construção, os relatórios e a documentação de um projeto a partir de uma informação central.

https://hub.docker.com/_/maven

Rodar usando bind mount

```bash
docker run -it --rm --name my-maven-project -v "$(pwd)":/usr/src/mymaven -w /usr/src/mymaven maven:3.6.3-jdk-11-slim bash
```

Fazendo cache local para ser reutilizado nos containers

```bash
docker volume create --name maven_repo

docker run -it -v maven_repo:/root/.m2 maven mvn archetype:generate
```

Rodar usando diretório de cache .m2 comparilhado

```bash
docker run -it --rm -v "$PWD":/usr/src/mymaven -v "$HOME/.m2":/root/.m2 -v "$PWD/target":/usr/src/mymaven/target -w /usr/src/mymaven maven bash
```

Exemplos:
