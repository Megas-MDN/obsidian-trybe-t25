[[Mongo DB]]

### Inserir um Único Documento

`db.collection.insertOne()` - insere um único documento em uma coleção.

O exemplo a seguir insere um novo documento na inventorycoleção. Se o documento não especificar um _idcampo, o MongoDB adiciona o `_idcampo` com um valor `ObjectId` ao novo documento. 

```JavaScript
db.inventory.insertOne(
   { item: "canvas", qty: 100, tags: ["cotton"], size: { h: 28, w: 35.5, uom: "cm" } }
)
```

`insertOne()` retorna um documento que inclui o _idvalor do campo do documento recém-inserido. Para obter um exemplo de documento de retorno, consulte a referência db.collection.insertOne() .

Para recuperar o documento que você acabou de inserir, consulte a coleção :

```JavaScript
db.inventory.find( { item: "canvas" } )
```


### Inserir vários documentos

`db.collection.insertMany()`pode inserir vários documentos em uma coleção. Passe uma matriz de documentos para o método.

O exemplo a seguir insere três novos documentos na inventorycoleção. Se os documentos não especificarem um _idcampo, o MongoDB adiciona o `_idcampo` com um valor `ObjectId` a cada documento. 

```JavaScript
db.inventory.insertMany([
   { item: "journal", qty: 25, tags: ["blank", "red"], size: { h: 14, w: 21, uom: "cm" } },
   { item: "mat", qty: 85, tags: ["gray"], size: { h: 27.9, w: 35.5, uom: "cm" } },
   { item: "mousepad", qty: 25, tags: ["gel", "blue"], size: { h: 19, w: 22.85, uom: "cm" } }
])
```

`insertMany()` retorna um documento que inclui os _idvalores de campo de documentos recém-inserido. Veja a referência para um exemplo.

Para recuperar os documentos inseridos, consulte a coleção :

```JavaScript
db.inventory.find( {} )
```


###### Fonte: [Documentação Oficial](https://www.mongodb.com/docs/manual/tutorial/insert-documents/)