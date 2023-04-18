[[Node]]


A leitura e escrita de arquivos é uma rotina muito realizada nas operações de back-end. Você pode, por exemplo:

-   armazenar os logs da sua aplicação;
-   ler arquivos de configurações para ações específicas;
-   exportar dados em um arquivo [CSV](https://support.google.com/google-ads/answer/9004364?hl=pt-BR).

Sendo assim, é muito importante que você, como uma boa pessoa desenvolvedora, saiba como fazer a leitura e escrita de arquivos.

## Lendo arquivos com métodos síncronos

Agora que já entendemos como funcionam _**callbacks**_, _**promises**_ e _**funções async**_, vamos nos aprofundar no módulo `fs` do Node que permite a leitura e escrita de arquivos, assim como mostra a figura a seguir:

![mind_map2](https://content-assets.betrybe.com/prod/mind_map2.png)

## Lendo arquivos com métodos assíncronos

O método fornecido pelo módulo `fs` para leitura assíncrona de arquivos é o `fs.readFile`. Esse método possui diferentes formas de retornar a leitura de um arquivo. Neste caso, iremos utilizar o retorno de uma Promise que deve deixar nosso código muito mais legível.

> Observação: Para utilizar as operações assíncronas do `fs`, precisamos alterar a importação do módulo `fs` para `('fs').promises`. Dessa forma, poderemos chamar as funções assíncronas para leitura e escrita de arquivos que retornarão Promises.

Vamos ver como ficaria o código do nosso exemplo anterior, agora de forma assíncrona com o uso de Promises e funções `async`:

```js
const fs = require('fs').promises;

async function main() {
  try {
    const data = await fs.readFile('./meu-arquivo.txt', 'utf-8');
    console.log(data);
  } catch (err) {
    console.error(`Erro ao ler o arquivo: ${err.message}`);
  }
}

main()
```

Note que para podermos utilizar o `async/await`, precisamos criar uma função `main` e colocar nossa lógica dentro dela. Isso acontece porque o `await` só pode ser utilizado dentro de funções `async`.

## Escrevendo dados em arquivos

Escrever dados em arquivos é um processo bem parecido com a leitura de dados! Assim como o módulo `('fs').promises` disponibiliza o método `readFile` para a leitura, há também o método `writeFile` para a escrita.

> my-node-project/writeFile.js

```js
const fs = require('fs').promises;

async function main() {
  try {
    await fs.writeFile('./meu-arquivo.txt', 'Meu textão');
    console.log('Arquivo escrito com sucesso!');
  } catch (err) {
    console.error(`Erro ao escrever o arquivo: ${err.message}`);
  }
}

main()
```

Rode o script com `node writeFile.js` e repare que o conteúdo do `meu-arquivo.txt` foi alterado para “Meu textão”.

Anota aí 🖊: No `writeFile`, assim como ocorre no `readFile`, você pode especificar algumas opções na escrita de arquivos passando um terceiro parâmetro (`flag`) opcional em seus métodos.

-   A opção `flag` especifica como o arquivo deve ser aberto e manipulado. O padrão é `'w'`, que especifica que o arquivo deve ser aberto para escrita.

> Observação: Se o arquivo não existir, ele é criado. Caso contrário, é reescrito, ou seja, tem seu conteúdo apagado antes de o novo conteúdo ser escrito. A flag `'wx'`, por exemplo, funciona como `'w'`, mas lança um erro caso o arquivo já exista.

Uau! Você já aprendeu várias coisas novas até aqui, não é mesmo!? E sabe qual é o mais legal? Agora a gente pode começar a unir também os conhecimentos que você já adquiriu de front-end para criar uma aplicação com front e back integrados! 🤩

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/2ed87e4f-9049-4314-8091-8f71b1925cf6/day/08afed28-2d18-4256-a8b9-a15ae8eb3375/lesson/1a1fc25d-0aab-438b-8382-1501cd4962ff)
