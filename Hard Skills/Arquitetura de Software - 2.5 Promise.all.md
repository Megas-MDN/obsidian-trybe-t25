[[Arquitetura de Software]]
[[Arquitetura de Software - 2 Camada Model]]
[[Promise]]


No JavaScript, utilizar métodos assíncronos em loops nem sempre nos dá o resultado esperado. Isso porque simplesmente usar `async/await` não garante que o comportamento da função será esperar que todas as `promises` sejam resolvidas.

Um exemplo fácil para ilustrar a situação, é tentar utilizar `async/await` dentro de um `forEach` que utiliza o módulo `fs` do Node.

> Para conseguir executar o código a seguir sem erros, crie um novo diretório chamado promise-all e dentro dele os arquivos `file1.txt`, `file2.txt`, `file3.txt` e `usingForEach.js`.

```bash
mkdir promise-all
cd promise-all
touch file1.txt file2.txt file3.txt usingForEach.js
```

```javascript
// usingForEach.js

const fs = require('fs').promises;

const files = [
  'file1.txt',
  'file2.txt',
  'file3.txt',
]

async function main() {
  try{
    await files.forEach(async (file, index) => {
      const contentFile = await fs.readFile(file, 'utf8');
      console.log(`File ${index + 1}: ${contentFile}`);
    });
    console.log(`That's all folks!`);
  } catch (err) {
    console.error(`Erro ao ler o arquivo: ${err.message}`);
  }
};

main()
```
> Você pode executar o código com o comando `node usingForEach.js`.

Caso os arquivos `.txt` estejam vazios, o resultado ao executar o código acima será:


```text
That's all folks!
File 2: 
File 3: 
File 1:
```

Maravilha, o código rodou sem erros! Mas você reparou que apesar de não acontecer nenhum erro, mesmo com o `await` antes do `forEach`, a função não esperou para executar o `console.log` depois de resolver as promises? 🤔

Para resolver isso, vamos conhecer mais sobre o `Promise.all`!

## Rodando várias promises com Promise.all

Como você viu em algumas partes do código do conteúdo de hoje, o `Promise.all` é um método que recebe um array de Promises e devolve uma única Promise, que será resolvida a partir do **retorno de todas as outras**. Para facilitar a abstração, vamos a um exemplo!

Imagine que é aniversário de uma amiga e você e mais duas pessoas da galera decidiram fazer um bolo surpresa para ela. Cada um ficou responsável por contribuir com o que podia e, no fim, Sam ficou de comprar os ingredientes, Frodo de emprestar a batedeira e você de fazer o bolo. Nesse caso, os ingredientes e a batedeira seriam como o array de Promises e a feitura do bolo seria o `Promise.all`, consegue dizer por que?

Isso porque só quando os ingredientes e a batedeira, estiverem com você (as Promises forem resolvidas) é que você poderá fazer o bolo! Se ou os ingredientes ou a batedeira não chegarem até você (equivale a uma das Promises ser rejeitada), seria impossível que o bolo fosse feito (Promise.all seria rejeitada).

Voltando ao código, utilizando o `Promise.all` em conjunto com um `map` poderíamos resolver de forma simples o problema do código apresentado anteriormente, pois esse método consegue garantir que o código irá esperar o loop inteiro ser concluído antes de executar as linhas seguintes.

Vamos criar um novo arquivo chamado `usingPromiseAll.js` para demonstrar essa ideia:

```javascript
// usingPromiseAll.js

const fs = require('fs').promises;

const files = [
  'file1.txt',
  'file2.txt',
  'file3.txt',
]

async function main() {
  try {
    const promises = files.map(async (file, index) => {
      const contentFile = await fs.readFile(file, 'utf8');
      console.log(`File ${index + 1}: ${contentFile}`)
    }) 
    await Promise.all(promises);
    console.log(`That's all folks!`);
  } catch (err) {
    console.error(`Erro ao ler o arquivo: ${err.message}`);
  }
}

main()
```

> Você pode executar o código com `node usingPromiseAll.js`.

Agora, ao executar o código teremos como resultado algo assim:

Copiar

```text
1File 3:
2File 1:
3File 2:
4That's all folks!
```

> 🖋️ Anota aí: Assim como o forEach com async/await, o Promise.all com map não garante que cada promise será resolvida na ordem em que aparece dentro do loop. Por isso, o ‘File 3’ ainda pode aparecer antes do ‘File 1’ e ‘File 2’, por exemplo. O que o Promise.all garante é que todas as promises dentro do array serão resolvidas antes de prosseguir com a execução do resto da função.

Para dar outro exemplo com `Promise.all`, suponha que precisássemos do resultado da leitura dos três arquivos da função anterior para escrever no final a soma do tamanho de todos os arquivos. Poderíamos escrever a função da seguinte forma:

```javascript
// usingPromiseAll.js

// ...

async function getFilesSizeSum() {
  try {
    let filesSizeSum = 0
    await Promise.all(files.map(async (file) => {
      contentFile = await fs.readFile(file);
      filesSizeSum = filesSizeSum + contentFile.byteLength;
    }));
    result = `Lidos 3 arquivos totalizando ${filesSizeSum} bytes`;
    return console.log(result);
  } catch (err) {
    console.error(`Erro ao ler o arquivo: ${err.message}`);
  }
}

getFilesSizeSum()
```

Também podemos encadear promises, utilizando o `.then` e escrever a função acima da seguinte forma:

```javascript
const fs = require('fs').promises;

Promise.all([
  fs.readFile('file1.txt'),
  fs.readFile('file2.txt'),
  fs.readFile('file3.txt'),
])
  .then(([file1, file2, file3]) => {
    const fileSizeSum = file1.byteLength + file2.byteLength + file3.byteLength;
    console.log(`Lidos 3 arquivos totalizando ${fileSizeSum} bytes`);
  })
  .catch((err) => {
    console.error(`Erro ao ler arquivos: ${err.message}`);
  });
```
> Repare também como esse método também nos permite utilizar um único `catch`, que será chamado caso qualquer uma das Promises seja rejeitada. 😉

Em nosso exemplo, precisamos de um método assíncrono para que o código espere o arquivo ser lido e ter seu tamanho guardado em uma variável em cada iteração para só depois chamar a variável que guardou a soma do tamanho de todos os arquivos. No conteúdo você viu que o `Promise.all` pode ser utilizado para fazer inserções simultâneas em um banco de dados e algo parecido poderia ser aplicado caso precisássemos atualizar um dado em duas tabelas ao mesmo tempo, por exemplo.

As possibilidades são muitas e agora a ferramenta está na sua mão para escolher como e quando usar!

## Para fixar

-   Com o módulo `fs`, crie uma função que lê e escreve vários arquivos ao mesmo tempo.
    -   Utilize o `Promise.all` para manipular vários arquivos ao mesmo tempo.
    -   Dado o seguinte array de strings: `['Finalmente', 'estou', 'usando', 'Promise.all', '!!!']`, faça com que sua função crie um arquivo contendo cada string, sendo o nome de cada arquivo igual a `file<index + 1>.txt`. Por exemplo, para a string “Finalmente”, o nome do arquivo é `file1.txt`.
    -   Programe sua função para que ela faça a leitura de todos os arquivos criados no item anterior, armazene essa informação e escreva em um arquivo chamado `fileAll.txt`.
    -   O conteúdo do arquivo `fileAll.txt` deverá ser `Finalmente estou usando Promise.all !!!`.


### Solução

-   Importar o módulo fs e criar a função com o Array de strings.

```javascript
const fs = require('fs').promises;

async function arrayToFile() {
  const strings = ['Finalmente', 'estou', 'usando', 'Promise.all', '!!!'];
}
```

-   Utilizar a função `map` para criar um Array de Promises, uma para cada arquivo.

```javascript
// const fs = require('fs').promises;

// async function arrayToFile() {
//   const strings = ['Finalmente', 'estou', 'usando', 'Promise.all', '!!!']

  const createFilesPromises = strings
    .map((string, index) => fs.writeFile(`./file${index + 1}.txt`, string));
// }
```

-   Utilizar `Promise.all` para aguardar a escrita de todos os arquivos - ou seja, a resolução de todas as promises.

```javascript
// const fs = require('fs').promises;

// async function arrayToFile() {
// ...

     await Promise.all(createFilesPromises);
// }
```

-   Realizar a leitura dos arquivos criados.

```javascript
// const fs = require('fs').promises;

// async function arrayToFile() {
// ...

    const fileNames = [
      'file1.txt',
      'file2.txt',
      'file3.txt',
      'file4.txt',
      'file5.txt',
    ];

    // aqui usamos a mesma estratégia
    // criamos uma promise de leitura para cada item no array `fileNames`
    const readFilesPromises = fileNames
      .map((fileName) => fs.readFile(fileName, 'utf-8'));

    // e aqui esperamos que todas as leituras sejam resolvidas
    const fileContents = await Promise.all(readFilesPromises);
// }
```

-   Concatenar o conteúdo dos arquivos e criar o arquivo novo.

```javascript
// const fs = require('fs').promises;

// async function arrayToFile() {
// ...

     const newFileContent = fileContents.join(' ');

     await fs.writeFile('./fileAll.txt', newFileContent);
// }
```

-   Executar a função.

```javascript
arrayToFile() // caso queira esperar a resolução, use o `await` ou `.then`
```