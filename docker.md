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

## Arquivo de configuração

Nos arquivos `yml` de configuração as chaves devem seguir a ordem:

- `version`
- `services`
- `volumes`
- `networks`

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

### Nomes

O nome padrão do arquivo do compose é `docker-compose.yml`

**Desenvolvimento**

**Somente recursos**

**Produção**

<br>
<br>
<br>
