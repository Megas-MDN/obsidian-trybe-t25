[[Funções]]
[[JavaScript]]


Você já deve ter percebido que uma das vantagens do ES6 é que a nova sintaxe elimina códigos repetitivos, contribuindo para a limpeza do código. O `property shorthand` é um recurso muito útil na hora de declarar objetos em Javascript. A função abaixo recebe como parâmetro informações sobre uma nova pessoa usuária e retorna um objeto contendo esses dados. Observe que as propriedades do objeto retornado e os argumentos que passamos para `newUser` são idênticos. Essa repetição parece desnecessária, não é mesmo?

```js
const newUser = (id, name, email) => {
  return {
    id: id,
    name: name,
    email: email,
  };
};

console.log(newUser(54, 'isabella', 'isabella@email.com')); // { id: 54, name: 'isabella', email: 'isabella@email.com' }

```

É exatamente essa repetição que a `feature` `property shorthand` elimina: podemos simplesmente substituir `id: id` por `id` que o Javascript entende que você quer atribuir o valor de `id` a uma propriedade com o mesmo nome que o parâmetro passado:
```js
const newUser = (id, name, email) => {
  return {
    id,
    name,
    email,
  };
};

console.log(newUser(54, 'isabella', 'isabella@email.com')); // { id: 54, name: 'isabella', email: 'isabella@email.com' }
```

Muito legal, não é mesmo? Este é mais um recurso que te permite escrever códigos mais concisos!

## Para Fixar

Agora é hora de praticar: altere a função `getPosition` utilizando a `property shorthand`.
```js
const getPosition = (latitude, longitude) => ({
  latitude: latitude,
  longitude: longitude,
});

console.log(getPosition(-19.8157, -43.9542));
```

#### **Solução**

```js
const getPosition = (latitude, longitude) => ({
  latitude,
  longitude,
});

console.log(getPosition(-19.8157, -43.9542));
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/ccfff26d-24c9-422e-b886-6ee19f20db14/day/9f13f306-fdc8-4208-94a8-a1e20101cd21/lesson/5ffcd9eb-5524-4071-92d8-9088fb6fe1a9)
