# Padrões e Nomenclatura

Arquivo contendo alguns padrões e nomenclaturas que defini para os meus projetos

## Builder Static Method em um objeto

Criação de objetos a partir de algum valor

- `of`
- `from` (evitar)

Conversão para algum tipo

- `to`

Personalizar Saída

- `as`
  - exemplo: `findByIdAsList()`

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

Métodos de listagem e buscas por critérios retornaram uma instância de `List` (Mantendo ordenação).

Métodos de buscas que devem obter somente um ou nenhum objeto. Caso não exista, por padrão, retornarão `null`.

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

Utilização de `AsOption` para ao invés de retornar um valor `null`, retornar `Option`.

- `findByIdAsOption(id)`
- `findOneByAsOption(Criteria)`
- `findFistByAsOption(Criteria)`
- `findLastByAsOption(Criteria)`

**Buscas ordenadas**

Métodos de buscas com resultados ordenados devem conter um argumento com o objeto `Sort`;

Exemplo:

- `findAll(Sort sort)`
- `findBy(Criteria criteria, Sort sort)`

**Buscas paginadas**

Métodos de buscas com resultados paginados devem conter um argumento com o objeto `PageRequest` e deve retornar uma instância de `Page`.

Exemplo:

- `findAll(PageRequest request)`
- `findBy(Criteria criteria, PageRequest request)`

**Buscas ordenadas e paginadas**

Métodos de buscas com resultados ordenados e paginados, devem conter um argumento com o objeto `Sort` e `PageRequest` consecutivamente.

Exemplo:

- `findAll(Sort sort, PageRequest request)`
- `findBy(Criteria criteria, Sort sort, PageRequest request)`

**Objetos**

| Nome          | Função                                                                                                                              |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `Criteria`    | Geralmente um `List` contendo os campos e os valores a serem buscados                                                               |
| `Sort`        | Objeto de ordenação. Emcapsula um `Map` onde a _chave_ é o campo/coluna e o _valor_ é a direção `ASC` ou `DESC`                     |
| `PageRequest` | Objeto de solicitação de paginação. Deve ser informado numero da página atual, quantidade de itens na página e ordenação (opcional) |
| `Page`        | Objeto de responsta de paginação responsta                                                                                          |

<br>

## Diretórios / Pacotes

Aguardando ...

<br>

### Serviços / Use Cases

Nome de métodos em classes de Serviços

**Alteração de estado**

- `insert`
- `update`
- `delete`
- `save` (insert/update)

**Listagem**

- `getAll`
- `getById`

<br>

## Endpoints APIs

Um endpoint representa um recurso, ou melhor, um conjunto de objetos, portanto sempre usar no plural.

Exemplo: Manutenção de Pessoas

**CRUD simples**

| Verbo    | Endpoint        | Descrição                        |
| -------- | --------------- | -------------------------------- |
| `GET`    | `/pessoas`      | Listar objetos                   |
| `POST`   | `/pessoas`      | Inserir um objeto                |
| `GET`    | `/pessoas/{id}` | Visualizar detalhes de um objeto |
| `PUT`    | `/pessoas/{id}` | Alterar um objeto                |
| `DELETE` | `/pessoas/{id}` | Excluir um objeto                |

**Alteração de estado além do alterar**

Sempre usar o verbo `PUT`

| Verbo | Endpoint                   | Descrição          |
| ----- | -------------------------- | ------------------ |
| `PUT` | `/pessoas/{id}/inactivate` | Inativar um objeto |
| `PUT` | `/pessoas/{id}/activate`   | Ativar um objeto   |

**Exibição de objetos aninhados**

| Verbo    | Endpoint                               | Descrição                                                   |
| -------- | -------------------------------------- | ----------------------------------------------------------- |
| `GET`    | `/pessoas/{id}/telefones`              | Listar objetos da lista                                     |
| `POST`   | `/pessoas/{id}/telefones`              | Inserir um objeto na lista \*¹                              |
| `GET`    | `/pessoas/{id}/telefones/{telefoneId}` | Visualizar detalhes um objeto da lista \*¹                  |
| `PUT`    | `/pessoas/{id}/telefones/{telefoneId}` | Alterar um objeto da lista \*¹                              |
| `DELETE` | `/pessoas/{id}/telefones/{telefoneId}` | Excluir um objeto da lista \*¹                              |
| `PUT`    | `/pessoas/{id}/telefones`              | LOTE: Atualizar todos objetos da lista (removal orphan \*²) |
| `DELETE` | `/pessoas/{id}/telefones`              | LOTE: Apagar todos objetos da lista                         |

- **\*1** - Usar somente se necessário. Desejável optar pela atualização completa da lista.
- **\*2** - Atualização de uma lista onde apaga-se completamente a lista persistente e adiciona a lista nova.
