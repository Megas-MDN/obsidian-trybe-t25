[[Mongo DB]]

Para remover documentos de uma coleção temos dois métodos que são utilizados para níveis de remoção diferentes: o `deleteOne()` e o `deleteMany()`. Os dois métodos aceitam um documento como parâmetro, que pode conter um filtro simples ou até mesmo um conjunto de expressões para atender aos critérios de seleção.

## `deleteOne()`

Esse método remove apenas um documento, que deve satisfazer o critério de seleção, mesmo que muitos outros documentos também se enquadrem no critério de seleção. Se nenhum valor for passado como parâmetro, a operação removerá o primeiro documento da coleção.

O exemplo abaixo remove o primeiro documento da coleção `inventory` em que o atributo `status` é igual a **D**:

```js
db.inventory.deleteOne({ status: "D" })
```

## `deleteMany()`

Esse método remove todos os documentos que satisfaçam o critério de seleção.

O exemplo abaixo remove todos os documentos da coleção `inventory` em que o atributo `status` é igual a **A**:

```js
db.inventory.deleteMany({ status : "A" })
```

Para remover todos os documentos da coleção, basta não passar nenhum parâmetro para o método `deleteMany()`:

```js
db.inventory.deleteMany({})
```



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d2b16462-a889-47fc-aa04-92517825b186/day/8bcc6393-e0d4-4280-ae0a-ca6d53a96eef/lesson/6f230ca6-68b3-4c18-b035-e42b9b02550e)

