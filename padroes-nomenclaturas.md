# Padrões e Nomenclatura

Arquivo contendo alguns padrões e nomenclaturas que defini para os meus projetos

## Builder Static Method em um objeto

Criação de objetos a partir de algum valor

- `of`
- `from`

Conversão para algum tipo

- `to`

Personalizar Saida

- `as`
  - examplo: `FindByIdAsList()`

<br>

## DTO - Data Transfer Object

Sufixos para nomes de Classes que representam DTOs

**Dados de entrada**

- `Request`
- `Input`
- `InputModel`
- `Command`

**dados de saida**

- `Response`
- `Output`
- `OutputModel`
- `CommandResult`

<br>

## Repositoy

Nome de métodos em classes Repositories

**Alteração de estado**

- `insert`
- `update`
- `delete`
- `upsert` ou `save`

**Listagem e Buscas**

Métodos de listagem e buscas por critérios retornaram uma instãncia de `List`.

Métodos de buscas que devem obter somente um ou nenhum objeto retornarão a instância encontrada. Caso não exista, por padrão, retornarão `null`.

- `findAll()`
- `findById(id)`
- `findBy(Criteria)`
- `findOneBy(Criteria)`
- `findFistBy(Criteria)`
- `findLastBy(Criteria)`

**Verificação de existência**

- `existsBy(Criteria)`
- `existsById`

**Contagem de objetos**

- `countAll()`
- `countBy(Criteria)`

**Alteração / Exclusão em lote**

- `updateBy(Criteria)`
- `deleteBy(Criteria)`

**Transação**

- `begin`
- `commit`
- `rollback`

**Customização de Retorno**

Utilização de `AsOtion` para ao invés de retornar um valor `null`, retornar `Option`.

- `findByIdAsOtion(id)`
- `findOneByAsOtion(Criteria)`
- `findFistByAsOtion(Criteria)`
- `findLastByAsOtion(Criteria)`

**Buscas ordenadas**

Métodos de buscas com resultados ordenados devem conter um argumento com o objeto `Sort`;

Exemplo:

- `findAll(Sort sort)`
- `findBy(Criteria criteria, Sort sort)`

**Buscas paginadas**

Métodos de buscas com resultados paginados devem conter um argumento com o objeto `PageRequest` e deve retornar uma instãncia de `Page`.

Exemplo:

- `findAll(PageRequest request)`
- `findBy(Criteria criteria, PageRequest request)`

**Buscas ordenadas e paginadas**

Métodos de buscas com resultados ordenados e paginados, devem conter um argumento com o objeto `Sort` e `PageRequest` consecutivamente.

Exemplo:

- `findAll(Sort sort, PageRequest request)`
- `findBy(Criteria criteria, Sort sort, PageRequest request)`

<br>

## Diretórios / Pacotes

Aguardando ...

<br>

### Serviços / Use Cases

Aguardando ...

<br>

## Endpoints APIs

Padronização dos enpoints.
