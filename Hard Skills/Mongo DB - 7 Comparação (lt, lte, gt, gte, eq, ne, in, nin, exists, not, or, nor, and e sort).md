[[Mongo DB]]

Os **operadores de comparação** servem para que você execute consultas comparando os valores de atributos dos documentos de uma coleção.

Esses operadores são utilizados como parte do filtro de alguns métodos para leitura de documentos do **MongoDB**. Por exemplo, o `find()` e o `countDocuments()`, que você já viu nesta seção, ou o `updateOne()`, que você verá em breve, aceitam filtros de comparação.

Vale lembrar que, para comparações de **BSON types** diferentes, você deve entender a [ordem de comparação](https://docs.mongodb.com/manual/reference/bson-type-comparison-order/#bson-types-comparison-order).

Os operadores seguem uma sintaxe padrão que é composta por um subdocumento, como no exemplo abaixo.


```js
{ <campo>: { <operador>: <valor> } }
```

Além disso, os operadores são identificados pelo prefixo **$**.

## Operador `$lt`

O operador `$lt` seleciona os documentos em que o valor do **atributo** filtrado é **menor do que (<)** o **valor** especificado.

Veja o exemplo abaixo:

```js
db.inventory.find({ qty: { $lt: 20 } })
```

Essa consulta selecionará todos os documentos na coleção `inventory` cujo valor do atributo `qty` é **menor do que 20**.

## Operador `$lte`

O operador `$lte` seleciona os documentos em que o valor do **atributo** filtrado é **menor ou igual (<=)** ao **valor** especificado.

Veja o exemplo abaixo:

```js
db.inventory.find({ qty: { $lte: 20 } })
```

Essa query selecionará todos os documentos na coleção `inventory` cujo valor do atributo `qty` é **menor ou igual a 20**.

## Operador `$gt`

O operador `$gt` seleciona os documentos em que o valor do **atributo** filtrado é **maior do que (>)** o **valor** especificado.

Veja o exemplo abaixo:


```js
db.inventory.find({ qty: { $gt: 20 } })
```

Essa query selecionará todos os documentos na coleção `inventory` cujo valor do atributo `qty` é **maior do que 20**.

## Operador `$gte`

O operador `$gte` seleciona os documentos em que o valor do **atributo** filtrado é **maior ou igual (>=)** ao **valor** especificado.

Veja o exemplo abaixo:

```js
db.inventory.find({ qty: { $gte: 20 } })
```

Essa query selecionará todos os documentos na coleção `inventory` cujo valor do atributo `qty` é **maior ou igual a 20**.

## Operador `$eq`

O operador `$eq` seleciona os documentos em que o valor do **atributo** filtrado é **igual** ao valor especificado. Esse operador é equivalente ao filtro `{ campo: <valor> }` e não tem nenhuma diferença de performance.

Veja o exemplo abaixo:

```js
db.inventory.find({ qty: { $eq: 20 } })
```

A operação acima é exatamente equivalente a:

```js
db.inventory.find({ qty: 20 })
```

Durante a aula você verá mais exemplos que o `$eq` é apenas uma maneira de explicitar o operador.

## Operador `$ne`

Esse operador é o contrário do anterior. Ao utilizar o `$ne`, o **MongoDB** seleciona os documentos em que o valor do **atributo** filtrado **não é igual** ao valor especificado.

```js
db.inventory.find({ qty: { $ne: 20 } })
```

A query acima retorna os documentos da coleção `inventory` cujo valor do atributo `qty` é **diferente de 20,** incluindo os documentos em que o atributo `qty` não existe.

## Operador `$in`

O operador `$in` seleciona os documentos em que o valor do **atributo** é igual a um dos valores do **array**. Embora você também possa executar essa consulta utilizando o operador `$or`, que você verá mais à frente no conteúdo, escolha o operador `$in` para executar comparações de igualdade com mais de um valor no mesmo atributo.

Veja o exemplo abaixo:

```js
db.inventory.find({ qty: { $in: [ 5, 15 ] } })
```

A query acima retorna todos os documentos da coleção `inventory` em que o valor do atributo `qty` é **5** ou **15**.

## Operador `$nin`

O operador `$nin` seleciona os documentos em que o valor do **atributo** filtrado não é igual ao especificado no **array,** ou o campo não existe.

Veja o exemplo abaixo:

```js
db.inventory.find( { qty: { $nin: [ 5, 15 ] } } )
```

Essa consulta seleciona todos os documentos da coleção `inventory` em que o valor do atributo `qty` é **diferente** de **5** e **15**. Esse resultado também inclui os documentos em que o atributo `qty` não existe.

## Operador `$exists`

Sintaxe:

```js
{ campo: { $exists: <boolean> } }
```

Quando o `<boolean>` é verdadeiro (`true`), o operador `$exists` encontra os documentos que contêm o **atributo,** incluindo os documentos em que o valor do atributo é igual a `null`. Se o `<boolean>` é falso (`false`), a consulta retorna somente os documentos que não contêm o atributo.

Veja o exemplo abaixo:

```js
db.inventory.find({ qty: { $exists: true } })
```

Essa consulta retorna todos os documentos da coleção `inventory` em que o atributo `qty` existe.

Você também pode combinar operadores, como no exemplo abaixo:

```js
db.inventory.find({ qty: { $exists: true, $nin: [ 5, 15 ] } })
```

Essa consulta seleciona todos os documentos da coleção `inventory` em que o atributo `qty` existe **E** seu valor é diferente de **5** e **15**.

## Operador `$not`

Sintaxe:

```js
{ campo: { $not: { <operador ou expressão> } } }
```

O operador `$not` executa uma operação lógica de **NEGAÇÃO** no **< operador ou expressão >** especificado e seleciona os documentos que **não** correspondam ao **< operador ou expressão >**. Isso também inclui os documentos que **não** contêm o **atributo**.

Veja o exemplo abaixo:

```js
db.inventory.find({ price: { $not: { $gt: 1.99 } } })
```

Essa consulta seleciona todos os documentos na coleção `inventory` em que o valor do atributo `price` é menor ou igual a **1.99** (em outras palavras, não é maior que **1.99**), ou em que o atributo **price** não existe.

**IMPORTANTE**: a expressão `{ $not: { $gt: 1.99 } }` retorna um resultado diferente do operador `$lte`. Ao utilizar `{ $lte: 1.99 }`, os documentos retornados serão somente aqueles em que o campo `price` existe e cujo valor é menor ou igual a **1.99**.

## Operador `$or`

O operador `$or` executa a operação lógica **OU** em um array de uma ou mais expressões e seleciona os documentos que satisfaçam **ao menos** uma das expressões.

Sintaxe:

```js
{ $or: [{ <expression1> }, { <expression2> }, ... , { <expressionN> }] }
```

Considere o exemplo a seguir:

```js
db.inventory.find({ $or: [{ qty: { $lt: 20 } }, { price: 10 }] })
```

Essa consulta seleciona todos os documentos da coleção `inventory` em que o valor do atributo `qty` é menor do que **20** ou o valor do atributo `price` é igual a **10**.

## Operador `$nor`

O operador `$nor` também executa uma operação lógica de **NEGAÇÃO,** porém, em um array de uma ou mais expressões, e seleciona os documentos em que todas essas expressões **falhem,** ou seja, seleciona os documentos em que todas as expressões desse array sejam falsas.

Sintaxe:

```js
{ $nor: [ { <expressão1> }, { <expressão2> }, ...  { <expressãoN> } ] }
```

Veja o exemplo abaixo:

```js
db.inventory.find({ $nor: [{ price: 1.99 }, { sale: true }] })
```

Essa query retorna todos os documentos da coleção `inventory` que:

-   Contêm o atributo `price` com o valor diferente de **1.99** e o atributo `sale` com o valor diferente de **true**;
    
-   Ou contêm o atributo `price` com valor diferente de **1.99** e **não** contêm o atributo `sale`;
    
-   Ou **não** contêm o atributo `price` e contêm o atributo `sale` com valor diferente de **true**;
    
-   Ou **não** contêm o atributo `price` e **nem** o atributo `sale`.
    

Pode parecer complexo, mas você fará mais exercícios para praticar esse operador.

## Operador `$and`

O operador `$and` executa a operação lógica **E** num array de uma ou mais expressões e seleciona os documentos que satisfaçam **todas** as expressões no array. O operador `$and` usa o que chamamos de **avaliação em curto-circuito** (_short-circuit evaluation_). Se alguma expressão for avaliada como **falsa,** o **MongoDB** não avaliará as expressões restantes, pois o resultado final sempre será **falso** independentemente do resultado delas.

Sintaxe:

```js
{ $and: [{ <expressão1> }, { <expressão2> } , ... , { <expressãoN> }] }
```

## Múltiplas expressões especificando o mesmo atributo

Considere o exemplo abaixo:

```js
db.inventory.find({
    $and: [
        { price: { $ne: 1.99 } },
        { price: { $exists: true } }
    ]
})
```

Essa consulta seleciona todos os documentos da coleção `inventory` em que o valor do atributo `price` é diferente de **1.99** e o atributo `price` existe.

## Múltiplas expressões especificando o mesmo operador

Considere o exemplo abaixo:

```js
db.inventory.find({
    $and: [
        { price: { $gt: 0.99, $lt: 1.99 } },
        {
            $or: [
                { sale : true },
                { qty : { $lt : 20 } }
            ]
        }
    ]
})
```

Essa consulta seleciona todos os documentos da coleção `inventory` em que o valor do campo `price` é maior que **0.99** e menor que **1.99,** **E** o valor do atributo `sale` é igual a **true,** **OU** o valor do atributo `qty` é menor do que **20**. Ou seja, essa expressão é equivalente a `(price > 0.99 E price < 1.99)` (onde o **E** está implícito na vírgula aqui `{ $gt: 0.99, $lt: 1.99 }`) **E** `(sale = true OU qty < 20)`.


## Método `sort()`

Sintaxe:

```js
db.colecao.find().sort({ "campo": "1 ou -1"})
```

Quando existe a necessidade de ordenar os documentos por algum atributo, o método `sort()` se mostra muito útil. Usando um valor positivo (`1`) como valor do atributo, os documentos da consultas são ordenados de forma crescente ou alfabética (também ordena por campos com `strings`). Em complemento, usando um valor negativo (`-1`), os documentos de saída estarão em ordem decrescente ou contra alfabética.

Esse método pode ser combinado com o método `find()`:

```js
db.example.find({}, { "value": 1, "name": 1 }).sort({ "value": -1, "name": 1 })
```

O `sort()` só pode ser usado se tiver algum resultado de busca antes:

```js
db.colecao.find().sort({ nomeDoAtributo: 1 }) // certo
db.colecao.sort({ nomeDoAtributo: 1 }) // errado
```

Vamos ver um exemplo?

```js
db.example.insertMany([
    { "name": "Mandioquinha Frita", "price": 14 },
    { "name": "Litrão", "price": 8 },
    { "name": "Torresmo", "price": 16 }
])
```


```js
db.example.find().sort({ "price": 1 }).pretty()
```



```js
// Resultado esperado:
{
        "_id" : ObjectId("5f7dd0582e2738debae74d6c"),
        "name" : "Litrão",
        "price" : 8
}
{
        "_id" : ObjectId("5f7dd0582e2738debae74d6b"),
        "name" : "Mandioquinha Frita",
        "price" : 14
}
{
        "_id" : ObjectId("5f7dd0582e2738debae74d6d"),
        "name" : "Torresmo",
        "price" : 16
}
```



```js
db.example.find().sort({ "price": -1, "name" : 1 }).pretty()
```



```js
// Resultado esperado:
{
        "_id" : ObjectId("5f7dd0582e2738debae74d6d"),
        "name" : "Torresmo",
        "price" : 16
}
{
        "_id" : ObjectId("5f7dd0582e2738debae74d6b"),
        "name" : "Mandioquinha Frita",
        "price" : 14
}
{
        "_id" : ObjectId("5f7dd0582e2738debae74d6c"),
        "name" : "Litrão",
        "price" : 8
}
```


###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d2b16462-a889-47fc-aa04-92517825b186/day/8bcc6393-e0d4-4280-ae0a-ca6d53a96eef/lesson/f985d5ae-c6b1-4a8a-a657-9f8807922f96)
