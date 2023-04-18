[[Mongo DB]]

O MongoDB trata alguns tipos de dados como equivalentes para fins de comparação. Por exemplo, tipos numéricos sofrem conversão antes da comparação. No entanto, para a maioria dos tipos de dados, os operadores de comparação do atributo destino do documento corresponde ao tipo do operando da query.

Para compreender melhor esse conceito, veja o exemplo abaixo, considerando a seguinte coleção:

```JavaScript
{ "_id": "apples", "qty": 5 }
{ "_id": "bananas", "qty": 7 }
{ "_id": "oranges", "qty": { "in stock": 8, "ordered": 12 } }
{ "_id": "avocados", "qty": "fourteen" }
```

A operação abaixo usa o operador de comparação $gt( greater than, maior que, >) para retornar os documentos em que o valor do atributo qty seja maior do que 4:

```JavaScript
db.collection.find( { qty: { $gt: 4 } } )
```

A operação trará como retorno os seguintes documentos:

```JavaScript
{ "_id": "apples", "qty": 5 }
{ "_id": "bananas", "qty": 7 }
```

O documento com o _id igual a "avocados" não foi retornado porque o valor do campo qty é do tipo string, enquanto o operador $gt é do tipo integer.

O documento com o _id igual a "oranges" também não foi retornado porque qty é do tipo object.

Nesses casos, vemos o schemaless funcionando na prática!

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d2b16462-a889-47fc-aa04-92517825b186/day/da82d65f-2261-4bcb-87bb-71e6a7e565f5/lesson/161b03e9-ba47-4457-acde-9ffbd05c96aa)
