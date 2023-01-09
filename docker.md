# Padrões e Nomenclatura - Docker

Padrões e nomenclatura para containers e staks docker

- `-` - para nomes compostos
- `_` - separação de lógica, objetivos e coisas diferentes

<br>

## Nomenclaturas em geral

O objetivo de se manter um padrão de nomeação é para facilitar a identificação dos serviços e organização nas listagens.

### **Projeto**

Determinar um nome significativo e objetivo para servir de identificaror do projeto na `stack` ou `composer`. Este nome servirá como prefixo e base para geração dos demais nomes.

Exemplo:

- Nome: Project 101 - Catálogo de Produtos
- Nome:
  - `project101`

No meu caso em particular, estou nomeando sequencialmente

### **Serviços**

Definir um nome significativo e objetivo (no singular) adicionando um sufixo para identificar o tipo de serviço;

Template:

- `<servico-nome>-<servico-tipo>`

Exemplo:

- Descrição: API para manutenção de Clientes
- Nome significativo:
  - `cliente`
- Tipo de serviço:
  - `api`
- Resultado/Nome do serviço:
  - `cliente-api`

_Tipos de Serviços_

- `api` - Microsserviço interface
- `db` - Banco de dados
- `cache` - Serviço de cache
- `queue` - Serviço de filas

Caso hava mais de um tipo de serviço da mesma categoria, adicionar o nome do mesmo

Exemplo:

- Banco de dados
  - `db-postgres`
  - `db-mysql`
- Filas:
  - `queue-rabbitmq`
  - `queue-activemq`

### **Imagens**

O nome de uma imagem deve conter o username do Docker Hub `jeanbarcellos`, uma barra para separação `/`, seguido do identificador do projeto e o nome do servico separados por `_`

Template:

- `<docker-hub-id>_<projeto-nome>_<servico-nome>`

Exemplo:

- `jeanbarcellos/project101_cliente-db_data`

### **Container**

Ao nomear o container adicione o nome do projeto como prefixo usando o `_` como separador

Exemplo:

- Template:
  - `<projeto-nome>_<servico-nome>`
- Nome:
  - `project101_cliente-api`

_OBSERVAÇÃO_

### **Rede**

Adicionar o sufixo `net` logo após ao nome do projeto

Template:

- `<projeto-nome>_net`

Exemplo:

- `project101_net`

### **Volumes**

O nome de um volmume do tipo `named` deveiniciar com o nome do projeto, sequido do nome do serviço que utilizará o mesmo.

Template:

- `<projeto-nome>_<servico-nome>_<volume-nome>`

Exemplo:

- `project101_cliente-db_data`

<br>
<br>

---

## Arquivo de configuração

### **Docker File**

O nome padrão do arquivo é `Dockerfile`

Geralmente este arquivo contém apenas um estágio (_stage_), no qual o Docker pega o app compilado e adiciona no container.

- `Dockerfile`
  - Containeriza um app pré compilado/construido
- `Dockerfile.multistage`
  - Stage 1: Realiza o _build_ (construção)
  - Stage 2: Containerizar o app constuído

Estágios:

- Buid - Constuir/Empacotar um app
- Run - Executar app já '_buildado_'

<br>

### **Docker Compose**

O nome padrão do arquivo do compose é `docker-compose.yml`

#### **Padrão de nome para os arquivos**

Sugestões de nomes para o docker-compose.

Primeiramente vamos fazer sugestôes conforme ambiente. Na sequência exemplos de possíveis e ultilizações. E por fim, o resultado desejado

- **Ambientes**

  **Desenvolvimento**

  - `docker-compose_dev.yml`
    - Opção 1: Faz o _bind mount_ dos serviços com a maquina local
    - Opção 2: Apenas execução de imagens previamente criadas e armazenadas localmente ou no Docker Hub
  - `docker-compose_dev-build.yml`
    - Realiza o _build_ as imagens antes de subir
    - Faz o _build_ das imagens antes de subir
      - Multi-stage
  - `docker-compose_bind-mount.yml`
    - Faz o _bind mount_ dos serviços com a maquina local
  - `docker-compose_only-resources.yml`
    - Contendo apenas os recursos como banco de dados, filas, chache, etc.
    - O objetivo é permitir que os serviços com código-fonte sejam executados na maquina local

  **Produção**

  - `docker-compose_prod.yml`
    - Apenas execução de imagens previamente criadas e armazenadas localmente ou no Docker Hub
    - Não faz _build_ as imagens
      - A geração da imagem deve ser realizada manualmente ou com o uso de CI/CD
  - `docker-compose_prod-build.yml`
    - Faz o _build_ das imagens antes de subir
      - Multi-stage

  <br>

- **Exemplos**

  Exemplos sugeridos e possíveis a partir dos ambientes (_estudar qual melhor padrão adotar_):

  Exemplo 1: Default apenas roda as imagens

  - `docker-compose.yml` - Apenas execução de imagens previamente criadas e armazenadas localmente ou no Docker Hub
  - `docker-compose_build.yml` - Faz o _build_ das imagens antes de subir
  - `docker-compose_dev.yml` - Faz o _bind mount_ dos serviços com a maquina local
  - `docker-compose_only-resources.yml` - Contendo apenas os recursos como banco de dados, filas, chache, etc.

  Exemplo 2: Default faz o _bind mount_

  - `docker-compose.yml` - Faz o _bind mount_ dos serviços com a maquina local
  - `docker-compose_only-resources.yml` - Contendo apenas os recursos como banco de dados, filas, chache, etc.
  - `docker-compose_build.yml` - Faz o _build_ das imagens antes de subir
  - `docker-compose_prod.yml` - Apenas execução de imagens previamente criadas e armazenadas localmente ou no Docker Hub

  Exemplo 3: Default apenas roda as imagens e se necessário, O `prod` entra em ação

  - `docker-compose.yml` - Apenas execução de imagens previamente criadas e armazenadas localmente ou no Docker Hub
  - `docker-compose_build.yml` - Faz o _build_ das imagens antes de subir
  - `docker-compose_dev.yml` - Faz o _bind mount_ dos serviços com a maquina local
  - `docker-compose_only-resources.yml` - Contendo apenas os recursos como banco de dados, filas, chache, etc.
  - `docker-compose_prod.yml` - (_Se necessário_) Apenas execução de imagens previamente criadas e armazenadas localmente ou no Docker Hub

  <br>

- **Resultado (_Escolhido_)**

  O resultado escolhido é o exemplo 3. Que é uma mescla do desenvolvimento com o produção. Porém a diferença é que o default não faz _build_ e nem _bind mount_, mas roda uma imagem previamente executada

  - `docker-compose.yml`
    - Apenas execução de imagens previamente criadas e armazenadas localmente ou no Docker Hub
    - Não faz _build_ as imagens
      - A geração da imagem deve ser realizada manualmente ou com o uso de CI/CD
  - `docker-compose_build.yml`
    - Realiza o _build_ as imagens antes de subir
    - Faz o _build_ das imagens antes de subir
      - Multi-stage
  - `docker-compose_dev.yml`
    - Faz o _bind mount_ dos serviços com a maquina local
  - `docker-compose_only-resources.yml`
    - Contendo apenas os recursos como banco de dados, filas, chache, etc.
    - O objetivo é permitir que os serviços com código-fonte sejam executados na maquina local
  - `docker-compose_prod.yml` - Apenas execução de imagens previamente criadas e armazenadas localmente ou no Docker Hub - Não faz _build_ as imagens - A geração da imagem deve ser realizada manualmente ou com o uso de CI/CD
    <br>
    <br>

#### **Conteúdo do arquivo**

Nos arquivos `yml` de configuração as chaves devem seguir a ordem:

- `version` - versão do Compose;
- `services` - containers/serviços que vão rodar nessa aplicação;
- `volumes` - possível adição de volumes;
- `networks` - redes

Dentro de um serviço, as chaves devem seguir a orgem:

- `container_name`
- `image`
- `build`
- `depends_on`
- `ports`
- `restart`
- `networks`
- `volumes`
- `environment`
- _outras configurações ..._

<br>
<br>
<br>

---

## Referências

- https://itnext.io/a-beginners-guide-to-deploying-a-docker-application-to-production-using-docker-compose-de1feccd2893
- https://ionutbanu.medium.com/build-spring-boot-docker-image-using-multi-stage-dockerfile-2-13b9f1e89393
