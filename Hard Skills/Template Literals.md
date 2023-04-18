
[[JavaScript]]
[[Funções]]
[[React]]



`template literals` é uma `feature` do ES6 que nos permite criar `strings` complexas de forma mais fácil. Você já deve ter concatenado `strings` e variáveis em Javascript da seguinte forma:
```js
const myName = 'Isabella';
console.log('Hello' + ' ' + myName + '!');
```

Essa solução ~~nada elegante~~ é como fazíamos antes do ES6 introduzir uma nova forma de criar e manipular strings dinamicamente através de `template literals`. Com o `template literals`, o exemplo acima pode ser substituído por:
```js
const myName = 'Isabella';
console.log(`Welcome ${myName}!`);
```

A sintaxe do `template literals` pede para usarmos o sinal de _crases_ no início e no final da frase, e variáveis dentro de um `${...}`. Você também pode adicionar uma expressão dentro das chaves, como `${a + b}`. Outra novidade é poder adicionar quebras de linha com o `template literals` sem a necessidade de concatená-las com o operador `+` e `\n` para trocar de linha. Execute o código abaixo para ver o resultado!
```js
// Com o template literals
console.log(`Primeira linha;
Segunda linha;
Terceira linha;`
);

// Sem o template literals:
console.log('Primeira linha;\n' + 'Segunda linha;\n' + 'Terceira linha;\n');
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/131a8311-a3d9-4404-ae50-2ea6c971f5d8/day/3ff84b4e-d7c4-4e82-8e0d-ceb79321b834/lesson/52736aee-9b87-4126-8f11-4e3b3aae5ac4)
