[[Arquitetura de Software]]
[[Arquitetura de Software - 2 Camada Model]]
[[Arquitetura de Software - 2.1 Camada Model - Implementando um CRUD]]


Continuando a lição anterior vamos implementar a função para inserir dados na tabela `passengers`. Para isso vamos fazer a seguinte mudança em `src/models/passenger.model.js`.

Copiar

```js
// const camelize = require('camelize');
const snakeize = require('snakeize');
// const connection = require('./connection');

// ...

const insert = async (passenger) => {
  const columns = Object.keys(snakeize(passenger)).join(', ');

  const placeholders = Object.keys(passenger)
    .map((_key) => '?')
    .join(', ');

  const [{ insertId }] = await connection.execute(
    `INSERT INTO passengers (${columns}) VALUE (${placeholders})`,
    [...Object.values(passenger)],
  );

  return insertId;
};

// module.exports = {
//   findAll,
//   findById,
  insert,
// };
```

Perceba que esse código possui algumas novidades se comparado com o anterior, veremos os principais pontos. Começamos pela importação da função `snakeize` do módulo com o mesmo nome.

Na sequência definimos uma variável para receber uma _string_ com os nomes das colunas que serão gerados a partir dos nomes de atributo de um objeto. Para chegar nesse resultado foi usado uma combinação de 4 recursos:

-   _**snakeize**_: Transforma o nome dos atributos para o padrão snake_case.
-   _**Object.keys**_: Cria o array com o nome dos atributos.
-   _**join**_: Transforma o array criado pelo `Object.keys` em uma string.

O próximo passo é criar uma _string_ formada por uma sequência de caracteres `?`, sendo uma `?` para cada atributo e são separados por vírgulas. Essa construção permite utilizar o recurso do módulo `mysql2` de preparar a operação a ser executada de forma segura. Nos referimos a essa funcionalidade como **Prepared Statement**. Como precisamos de um sinal de interrogação para cada atributo, usamos novamente o `Object.keys`, porém sem a necessidade de aplicar o `snakeize` dessa vez, pois precisamos do array só para saber a quantidade de vezes que o `map` será executado para gerar o array de `?`. Ao final desse processo transformamos esse array em uma string usando novamente a função `join`.

Portanto, se passarmos um objeto no seguinte formato para função `insert`:

```js
{
  "name": "John Doe",
  "email": "johndoe@gmail.com",
  "phone": "99 99999-9999"
}
```

Os valores das variáveis **columns** e **placeholders** serão respectivamente `name, email, phone` e `?, ?, ?`. Caso houvesse algum atributo no padrão **camelCase**, a função `snakeize` transformaria esse nome para o padrão **snake_case**. (Por exemplo: `createdAt` se tornaria `created_at`).

O próximo passo é montar a query com o valor dessas duas variáveis e chamar a função `connection.execute`.

```js
  const [{ insertId }] = await connection.execute(
    `INSERT INTO passengers (${columns}) VALUE (${placeholders})`,
    [...Object.values(passenger)],
  );
```

Perceba, que dessa vez estamos desestruturando o retorno usando `[{ insertId }]`. Fizemos isso, pois operações do tipo **INSERT**, **UPDATE** e **DELETE** retornam uma resposta em um formato diferente das operações do tipo **SELECT**. Dito isso, a função retorna um `array` onde o primeiro elemento é objeto que possui alguns atributos, dentre eles o `insertId` que é o valor da chave primária gerada pelo banco de dados.

Além disso, passamos como segundo parâmetro da função `connection.execute` o valor `[...Object.values(passenger)]`, ou seja, estamos pegando os valores que estão nos atributos do objeto e transformando em um array. Estamos aplicando o **spread operator** para espalhar os valores de `Object.values(passenger)` dentro do array que forma o segundo parâmetro da função `connection.execute`.

## Implementando o teste

Vamos escrever o teste para essa função?

Antes de escrever o teste, precisaremos de um objeto para ser utilizado como parâmetro para a função `passengerModel.insert`. Para isso acrescente no arquivo de mock o seguinte objeto e sua respectiva exportação.

```js
// tests/unit/models/mocks/passenger.model.mock.js

// ...

const newPassenger = {
  name: 'Bruce Lane',
  email: 'bruce.lane@acme.com',
  phone: '(77) 8179-0943',
};

// module.exports = {
  // passengers,
  newPassenger,
// };
```

Agora no arquivo de teste adicione o caso de teste `it`:

```js
// tests/unit/models/passenger.model.test.js

// ...

// const connection = require('../../../src/models/connection');
const { passengers, newPassenger } = require('./mocks/passenger.model.mock');

// describe('Testes de unidade do model de pessoas passageiras', function () {
//   ...

   it('Cadastrando uma pessoa passageira', async function () {
    // Arrange
    sinon.stub(connection, 'execute').resolves([{ insertId: 42 }]);
    // Act
    const result = await passengerModel.insert(newPassenger);
    // Assert
    expect(result).to.equal(42);
  });

//  afterEach(function () {
//    sinon.restore();
//  });
// });
```

Primeiro, importamos o objeto `newPassenger` que vem do arquivo de mock para usarmos como parâmetro da função `insert`.

Perceba que para refletir o retorno do `connection.execute` através do **sinon** fizemos um **arranjo** para criar um dublê para retornar um array com o objeto `{ insertId: 42 }` (lembrando que o `sinon.stub()` precisa emular o retorno no mesmo formato que o real). Na linha seguinte, chamamos o método `insert` (**ação**) e guardamos seu retorno na variável `result`. Na última linha fazemos a **asserção** de comparar se `result` é igual ao valor `42`, o valor que **mockamos** na primeira no **arranjo**. Execute esse teste agora e veja que ele passará.

Perfeito, não? Já temos a camada **Model** pronta para fazer 3 das 5 operações básicas de um CRUD. 🎉 🥳 🎉

## Configurando seu ambiente para Debug

Uma boa prática que podemos adotar em nossa vida de pessoa desenvolvedora é a prática de `depurar` (ou debugar) nosso código.

Provavelmente, para analisar suas aplicações `JavaScript`, você utiliza o famoso **console.log**. Isso é válido e necessário. Porém, hoje você vai aprender uma maneira menos verbosa e mais elegante de depurar o seu código através do próprio **VsCode**.

Esse processo de depuração (debugging em inglês) é importante porque conseguimos analisar passo a passo cada linha de nosso código, entendendo, por exemplo, em qual linha ocorre um erro ou é chamada uma **callback**.

Para configurar sua máquina para fazer o debug, clique na opção `Run and Debug` no menu à esquerda do seu VsCode ou utilize o atalho `Ctrl + Shift + D` se for usuário do Linux.

![Debug ícone VsCode](https://content-assets.betrybe.com/prod/eb4c6e08-a83e-4c6d-b352-c3b6075b10e2-Debug%20%C3%ADcone%20VsCode.JPG)

Depois, clique na opção `Run and Debug` destacada em azul.

![Run and Debug VsCode](https://content-assets.betrybe.com/prod/eb4c6e08-a83e-4c6d-b352-c3b6075b10e2-Run%20and%20Debug%20VsCode.JPG)

Ao abrir a caixa de seleção, clique em `Node.Js`.

![Node.Js Debug VsCode](https://content-assets.betrybe.com/prod/eb4c6e08-a83e-4c6d-b352-c3b6075b10e2-Node.Js%20Debug%20VsCode.JPG)

Depois selecione o **script** utilizado para rodar a aplicação em desenvolvimento, por exemplo, em nossa aplicação **TrybeCar**, selecione a opção `Run Script: debug`.

⚠️ **Caso o script de debug não funcione, você pode selecionar a opção Run Current File ao final da lista.**

![Run Script: debug VsCode](https://content-assets.betrybe.com/prod/eb4c6e08-a83e-4c6d-b352-c3b6075b10e2-Run%20Script:%20debug%20VsCode.JPG)

Isso fará com que o servidor inicie o `nodemon` em processo de depuração.

## Breakpoints

Para que o **debug** fique mais nítido, podemos especificar a linha que desejamos analisar através de uma ferramenta chamada `breakpoint`. Em tradução livre, `breakpoint` pode significar `"ponto de parada"`. Podemos marcar esses _pontos de parada_ clicando com o mouse à esquerda do número da linha. Quando fazemos isso, um pequeno **círculo vermelho** aparecerá, indicando que aquela linha é um `breakpoint`.

![Breakpoint](https://content-assets.betrybe.com/prod/eb4c6e08-a83e-4c6d-b352-c3b6075b10e2-Breakpoint.png)

Isso significa que, quando sua depuração chegar àquela linha, haverá uma pausa para que você possa analisar aquele **escopo**. Essa análise é feita no **menu lateral**, onde você poderá identificar informações como variáveis, nome do arquivo, funções chamadas etc.

![Left Bar Debug](https://content-assets.betrybe.com/prod/eb4c6e08-a83e-4c6d-b352-c3b6075b10e2-Left%20Bar%20Debug.png)



###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/94d0e996-1827-4fbc-bc24-c99fb592925b/section/d8fc0320-73f1-45d4-9f4f-2b6911b176b1/day/6b5ecd71-9499-4ffe-8776-e91e46f93a08/lesson/395a6abf-b513-40f2-b392-6d242671b0d9)
