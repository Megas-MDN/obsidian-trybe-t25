[[Mongo DB]]

## Método find()

Após inserir documentos em seu banco de dados, você vai querer recuperá-los. Certo?

Assim como nos bancos de dados relacionais, no **MongoDB** temos um método específico para essa operação: o `find()`.

## Parâmetros do find()

O método `find()` serve para selecionar os documentos de uma **coleção** e retorna um **cursor** com esses documentos.

Esse método recebe dois parâmetros:

`db.collection.find(query, projection)`

-   `query` (opcional):
    -   Tipo: documento;
    -   Descrição: especifica os filtros da seleção usando os _query operators_. Para retornar todos os documentos da coleção, é só omitir esse parâmetro ou passar um documento vazio ({}).
-   `projection` (opcional):
    -   Tipo: documento;
    -   Descrição: especifica quais atributos serão retornados nos documentos selecionados pelo parâmetro _query_. Para retornar todos os atributos desses documentos, é só omitir esse parâmetro.

Esse método retorna um **cursor** para os documentos que correspondem aos critérios de consulta.

## Projeção (projection)

Como dito, o parâmetro **projection** determina quais atributos serão retornados dos documentos que atendam aos critérios de filtro. O formato recebido por ele é algo como:

```js
{ "atributo1": <valor>, "atributo2": <valor> ... }
```


O `<valor>` pode ser uma das seguintes opções:

-   `1` ou `true` para incluir um campo nos documentos retornados;
    
-   `0` ou `false` para excluir um campo;
    
-   Uma expressão usando [Projection Operators](https://docs.mongodb.com/manual/reference/operator/projection/).
    

Você pode escolher exibir no resultado da consulta apenas certos atributos.

A **projeção** é sempre o segundo parâmetro do método `find()`.

Veja só este exemplo:

```js
db.movies.insertOne(
    {
        "title" : "Forrest Gump",
        "category" : [ "drama", "romance" ],
        "imdb_rating" : 8.8,
        "filming_locations" : [
            { "city" : "Savannah", "state" : "GA", "country" : "USA" },
            { "city" : "Monument Valley", "state" : "UT", "country" : "USA" },
            { "city" : "Los Anegeles", "state" : "CA", "country" : "USA" }
        ],
        "box_office" : {
            "gross" : 557, "opening_weekend" : 24, "budget" : 55
        }
    }
)
```

A operação acima insere um documento na coleção `movies` com vários atributos. Com a operação abaixo, selecionamos esse documento na coleção `movies`, passando como parâmetro de **projeção** apenas os atributos `title` e `imdb_rating`:

```js
db.movies.findOne(
    { "title" : "Forrest Gump" },
    { "title" : 1, "imdb_rating" : 1 }
)
```

Como resultado, teremos o seguinte:

```js
{
    "_id" : ObjectId("5515942d31117f52a5122353"),
    "title" : "Forrest Gump",
    "imdb_rating" : 8.8
}
```

Note que o atributo `_id` também foi retornado. Isso acontece porque ele é o único atributo que você não precisa especificar para que seja retornado. O movimento aqui é ao contrário, se você não quiser vê-lo no retorno, é só suprimí-lo da seguinte forma:

```js
db.movies.findOne(
    { "title" : "Forrest Gump" },
    { "title" : 1, "imdb_rating" : 1, "_id": 0 }
)
```

Agora sim, nosso resultado será apenas com os atributos devidos:

```json
{
    "title" : "Forrest Gump",
    "imdb_rating" : 8.8
}
```


## Gerenciamento do cursor

Ao executar o método `find()`, o **MongoDB Shell** itera automaticamente o cursor para exibir os 20 primeiros documentos. Digite `it` para continuar a iteração. Assim, mais 20 documentos serão exibidos até o final do cursor.

Um método bastante interessante que é utilizado num `cursor` é o `countDocuments()`. O método `countDocuments()` retorna o número de documentos de uma coleção, e também pode receber um critério de seleção para retornar apenas o número de documentos que atendam a esse critério.

**Nota:**na documentação do mongo você poderá encontrar o método `count()` que tem uso similar ao `countDocuments()`, porém foi depreciado a partir da versão `4.0`. Você pode encontrar os detalhes [aqui.](https://docs.mongodb.com/manual/reference/method/db.collection.count/)

Você pode retornar o número de documentos de uma coleção com a seguinte operação:

```js
db.movies.countDocuments({})
```

Veremos adiante mais utilizações para o método `countDocuments()`.


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d2b16462-a889-47fc-aa04-92517825b186/day/da82d65f-2261-4bcb-87bb-71e6a7e565f5/lesson/c3dfe5a7-5fe5-4df9-9501-127c9f2b4b34)
