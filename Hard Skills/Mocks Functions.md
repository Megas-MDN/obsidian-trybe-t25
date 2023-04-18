[[React Testing Library - RTL]]
[[API]]
[[Teste Assincrono]]
[[Jest]]
[[Testes com Jest]]

Mock Functions são ferramentas que nos permitem simular o comportamento  de funções reais (quebrar dependências).

O objetivo de _mockar_ uma função, módulo ou requisição é permitir a quem desenvolve ter controle sobre todo o funcionamento de seus testes. Pense em uma requisição de API que constantemente muda seu retorno. Como ter certeza do seu retorno e, principalmente, de que seu teste não está caindo em um **falso-positivo**?

No exemplo abaixo, podemos ver um caso em que simular o comportamento da função seria necessário para o teste:
```jsx
const retornaNumeroAleatorio = () => Math.floor(Math.random() * 100);

const divisivelPorDois = () => (retornaNumeroAleatorio() % 2) === 0;

test('quando o número aleatório é par, a função retorna `true`', () => {
  expect(divisivelPorDois()).toBe(true); // Como garantimos que o número retornado será par?
});
```

_Mockar_ o comportamento da função `retornaNumeroAleatorio()` para garantir que ela está, nesse teste, retornando um número par seria a solução para esse impasse!

Dentre as principais formas de se _mockar_ algo somente utilizando Jest, destacam-se três:

-   jest.fn();
-   jest.mock();
-   jest.spyOn().

## Mockando funções com Jest

O método **jest.fn()** configura-se como a forma mais simples de mockar algo: ele transforma uma função em uma simulação. Ou seja: ao _mockar_ uma função com o `jest.fn()` e fazer a chamada dela, o comportamento definido no _mock_ será chamado, em vez da função original.

Ele é muito útil para casos como o do exemplo da seção anterior, em que precisamos ter controle dos números gerados aleatoriamente.

Fazendo o teste para saber se a função é chamada, temos:
```jsx
// const retornaNumeroAleatorio = () => Math.floor(Math.random() * 100);

// const divisivelPorDois = () => (retornaNumeroAleatorio() % 2) === 0;

test("#divisivelPorDois", () => {
  // testando se a função foi chamada
  divisivelPorDois();
  expect(divisivelPorDois).toHaveBeenCalled();
});
```

Esse teste deveria passar, não? Afinal, a função foi chamada logo acima dele. Mas ele não passa, e o erro nos indica o que fazer:

> **Matcher error**: received value must be a mock or spy function.

Esse erro acontece porque a propriedade _toHaveBeenCalled_, assim como outras que serão ensinadas a seguir, é exclusiva para funções simuladas. Ou seja: **se você não simula uma função, a propriedade não funciona corretamente**.

Portanto, vamos utilizar o `jest.fn()` para testar a chamada dessa função:
```jsx
// ...
test("#divisivelPorDois", () => {
  // testando se a função foi chamada. Não simulamos nenhum comportamento aqui, pois, para esse teste, isso não importa! Apenas queremos saber se ela foi chamada.
  divisivelPorDois = jest.fn();

  divisivelPorDois();
  expect(divisivelPorDois).toHaveBeenCalled();
});
```

Ao declarar `divisivelPorDois = jest.fn();`, estamos dizendo ao teste que, a partir daquele momento, estamos tomando controle da função `divisivelPorDois` e que ela será uma simulação da função original.

Por ser uma simulação, **podemos especificar qual vai ser o retorno da função**. Basicamente, o que podemos dizer é: _“No contexto deste teste, quando essa função for chamada, ela retornará o valor que eu defini, em vez de um valor aleatório!”_. Duas propriedades nos permitem fazer essa declaração: `mockReturnValue(value)` e `mockReturnValueOnce(value)`. O `mockReturnValue` define um valor padrão de retorno. Já o `mockReturnValueOnce` retorna o valor definido apenas uma vez, e é importante, pois pode ser encadeado para que chamadas sucessivas retornem valores diferentes.
```jsx
//...
test("#divisivelPorDois", () => {
  // testando se a função foi chamada e qual seu retorno
  divisivelPorDois = jest.fn().mockReturnValue(true);

  divisivelPorDois();
  expect(divisivelPorDois).toHaveBeenCalled();
  expect(divisivelPorDois()).toBe(true);
});
```

No exemplo acima, estamos manualmente chamando a função _divisivelPorDois();_. Caso isso não seja feito, o teste _expect(divisivelPorDois).toHaveBeenCalled()_ irá falhar. Isso acontece porque _mockar_ uma função redefine seu comportamento, mas não a executa. A propriedade _toHaveBeenCalled()_ espera que a função dentro do `expect` tenha sido executada por alguma chamada anterior a essa linha dentro do contexto desse teste.

Além disso, podemos também testar quantas vezes a função foi chamada. Para isso, utilizamos a propriedade `toHaveBeenCalledTimes(number)`:
```jsx
// ...
test("#divisivelPorDois", () => {
  // testando quantas vezes a função foi chamada e qual seu retorno
  divisivelPorDois = jest
    .fn()
    .mockReturnValue('default value')
    .mockReturnValueOnce('first call')
    .mockReturnValueOnce('second call');

  expect(divisivelPorDois).toHaveBeenCalledTimes(0);

  expect(divisivelPorDois()).toBe("first call");
  expect(divisivelPorDois).toHaveBeenCalledTimes(1);

  expect(divisivelPorDois()).toBe("second call");
  expect(divisivelPorDois).toHaveBeenCalledTimes(2);

  expect(divisivelPorDois()).toBe("default value");
  expect(divisivelPorDois).toHaveBeenCalledTimes(3);
});
```

É possível implementar vários comportamentos em uma simulação. No exemplo acima, note que a implementação _mockReturnValueOnce_ se sobrepõe em relação ao _mockReturnValue_, que se torna um padrão apenas após os retornos de _mockReturnValueOnce_ serem executados.


## Mockando Módulos

Diferentemente do `jest.fn()`, que simula apenas uma função por vez, temos o `jest.mock()`, que tem como principal diferencial `mockar` todo um pacote de dependências ou módulo de uma vez.

Por exemplo: em um arquivo chamado `math.js`, temos as seguintes funções:
```jsx
const sleep = (ms) => {
  return new Promise(resolve => setTimeout(resolve, ms));
};

const somar = async (a, b) => { await sleep(10000); return a + b }; // Função de somar mais lenta do mundo
const subtrair = (a, b) => a - b;
const multiplicar = (a, b) => a * b;
const dividir = (a, b) => a / b;

module.exports = { somar, subtrair, multiplicar, dividir };
```

Utilizando o `jest.fn()`, teríamos que `mockar` todas as funções uma a uma. Com o `jest.mock()`, podemos `mockar` todas com um só comando:
```jsx
jest.mock('./math');
```

Uma vez que _mockarmos_ todo o arquivo `math.js`, passamos a simular o comportamento de todas as suas funções, porém sua implementação individual permanece indefinida. Caso passemos os parâmetros 1 e 2 para a função `somar`, por exemplo, o retorno será “undefined”. Isso se dá porque a simulação deixou de acessar o comportamento da função original do `math.js`.

Apesar de podermos definir um retorno com `mockReturnValue`, há casos em que é útil ir além dessa capacidade de retornar valores e criar um novo comportamento para a função simulada. É o que o método `mockImplementation(func)` faz. Ele aceita uma função que deve ser usada como implementação.

Veja um exemplo:
```jsx
const math = require('./math');
jest.mock("./math");

test("#somar", () => {
  // Aqui testamos se a função foi chamada, quantas vezes foi chamada, quais parâmetros foram usados e qual seu retorno

  math.somar.mockImplementation((a, b) => a + b);
  math.somar(1, 2);

  expect(math.somar).toHaveBeenCalled();
  expect(math.somar).toHaveBeenCalledTimes(1);
  expect(math.somar).toHaveBeenCalledWith(1, 2);
  expect(math.somar(1, 2)).toBe(3);
});
```

No exemplo acima, utilizamos também o método `toHaveBeenCalledWith(...args)`, que valida quais parâmetros foram passados para a função.

Assim como o `mockReturnValueOnce`, podemos também implementar uma funcionalidade para apenas uma chamada com `mockImplementationOnce`.

## Trabalhando com mock e funções originais

Ter controle sobre o comportamento de uma função e usar _matchers_ como o `toHaveBeenCalled` são ferramentas essenciais para quem desenvolve.

Existem casos nos quais é útil verificar os **efeitos colaterais de uma função**, como em uma alteração de um elemento na página, por exemplo. Mas como fazer isso se, ao _mockar_ uma função, ela perde sua implementação original? E ao mesmo tempo, sem _mockar_, não podemos testá-la com o matcher?

O **jest.spyOn()** é capaz de resolver esse problema. Ele “espia” a chamada da função simulada, enquanto deixa a implementação original ativa.

Por exemplo: em um arquivo chamado `math.js`, temos as seguintes funções:
```jsx
const sleep = (ms) => {
  return new Promise(resolve => setTimeout(resolve, ms));
};

const somar = async (a, b) => { await sleep(10000); return a + b }; // Função de somar mais lenta do mundo
const subtrair = (a, b) => a - b;
const multiplicar = (a, b) => a * b;
const dividir = (a, b) => a / b;

module.exports = { somar, subtrair, multiplicar, dividir };
```

E, em nosso arquivo de teste, temos o seguinte código:
```jsx
const math = require('./math');

test("#somar", () => {
  // testando se a função foi chamada, quantas vezes foi chamada, quais parâmetros foram usados e qual seu retorno
  const mockSomar = jest.spyOn(math, "somar");

  mockSomar(1, 2);
  expect(mockSomar).toHaveBeenCalled();
  expect(mockSomar).toHaveBeenCalledTimes(1);
  expect(mockSomar).toHaveBeenCalledWith(1, 2);
  expect(mockSomar(1, 2)).resolves.toBe(3);
});
```

Podemos notar no exemplo que a simulação da função é criada, mas sua implementação é mantida, e a soma, realizada.

Há também como limpar, resetar ou restaurar `mocks`. Existem três métodos capazes de fazer isso:

-   `mock.mockClear()`
    
    -   Útil quando você deseja limpar os dados de uso de uma simulação entre dois `expect`s.
-   `mock.mockReset()`
    
    -   Faz o que o `mockClear()` faz;
    -   Remove qualquer retorno estipulado ou implementação;
    -   Útil quando você deseja resetar uma simulação para seu estado inicial.
-   `mock.mockRestore()`
    
    -   Faz tudo que `mockReset()` faz;
    -   Restaura a implementação original;
    -   Útil para quando você quer simular funções em certos casos de teste e restaurar a implementação original em outros.

Como exemplo, imagine que você queira testar a função _mockada_ `somar` implementando para ela um método de subtração, mas que depois você queira redefinir as implementações do `mock`.

```jsx
const math = require('./math');

test("#somar", () => {
  // testando a implementação original, o mock e o mock resetado

  // implementação original
  expect(math.somar(1, 2)).resolves.toBe(3);

  // criando o mock e substituindo a implementação para uma subtração
  math.somar = jest.fn().mockImplementation((a, b) => a - b);

  math.somar(5, 1);
  expect(math.somar).toHaveBeenCalledTimes(1);
  expect(math.somar(5, 1)).toBe(4);
  expect(math.somar).toHaveBeenCalledTimes(2);
  expect(math.somar).toHaveBeenLastCalledWith(5, 1);

  // resetando o mock
  math.somar.mockReset();
  expect(math.somar(1, 2)).toBe(undefined);
  expect(math.somar).toHaveBeenCalledTimes(1);
  expect(math.somar).toHaveBeenLastCalledWith(1, 2);
});
```

No exemplo acima, por termos usado o jest.fn(), não há como restaurar as implementações originais da função, pois suas funcionalidades não permitem. A única ferramenta que nos permite transitar entre simulação e comportamento original é o **jest.spyOn()**.

```jsx
const math = require('./math');

test("#somar", () => {
  // testando a implementação original, o mock e a restauração da função original

  // implementação original
  expect(math.somar(1, 2)).resolves.toBe(3);

  // criando o mock e substituindo a implementação para uma subtração
  const mockSomar = jest
    .spyOn(math, "somar")
    .mockImplementation((a, b) => a - b);

  math.somar(5, 1);
  expect(mockSomar).toHaveBeenCalledTimes(1);
  expect(mockSomar(5, 1)).toBe(4);
  expect(mockSomar).toHaveBeenCalledTimes(2);
  expect(mockSomar).toHaveBeenLastCalledWith(5, 1);

  // restaurando a implementação original
  math.somar.mockRestore();
  expect(math.somar(1, 2)).resolves.toBe(3);
});
```

# Testando APIs e inputs

## Testando uma chamada de API no React

Agora que você já conheceu o básico de mockar funções e módulos no Jest, vamos ver como isso funciona em uma aplicação React. Utilizaremos a api de piadas aleatórias para acompanhar os exemplos.

Primeiro crie uma aplicação com `npx create-react-app`, substitua o `App.js` pelo conteúdo abaixo:
```jsx
// App.js
import React from 'react';
import './App.css';

class App extends React.Component {
  constructor() {
    super();
    this.state = {
      joke: '',
    };
    
    this.fetchJoke = this.fetchJoke.bind(this);
  }

  componentDidMount() {
    this.fetchJoke();
   }
   
   fetchJoke() {
    const API_URL = 'https://icanhazdadjoke.com/';
    const REQUEST_CONFIG = { headers: { Accept: 'application/json' } };
    fetch(API_URL, REQUEST_CONFIG)
      .then((response) => response.json())
      .then((data) => this.setState({ joke: data.joke }));
  }

  render() {
    const { joke } = this.state;

    return (
      <div className="App">
        <p>{joke}</p>
      </div>
    );
  }
}

export default App;
```

Teste se sua aplicação tem o funcionamento correto no navegador retornando uma piada aleatória a cada vez que a pagina é atualizada.

Agora temos o problema: _como testar a aplicação sem que quebre toda vez que nossa api retornar uma nova piada diferente?_ 🤔

Para resolver esse problema, vamos ver dois exemplos com o _Jest_ que vão nos permitir _mockar_, respectivamente, um módulo e sua implementação.

### Primeira forma de mock do fetch

Substitua o arquivo App.test.js pelo conteúdo abaixo:
```jsx
// App.test.js
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';

afterEach(() => jest.clearAllMocks());

it('fetches a joke', async () => {
  const joke = {
    id: '7h3oGtrOfxc',
    joke: 'Whiteboards ... are remarkable.',
    status: 200,
  };

  jest.spyOn(global, 'fetch');
  global.fetch.mockResolvedValue({
    json: jest.fn().mockResolvedValue(joke),
  });

  render(<App />);
  const renderedJoke = await screen.findByText('Whiteboards ... are remarkable.');
  expect(renderedJoke).toBeInTheDocument();
  expect(global.fetch).toHaveBeenCalledTimes(1);
  expect(global.fetch).toHaveBeenCalledWith(
    'https://icanhazdadjoke.com/',
    { headers: { Accept: 'application/json' } },
  );
});
```

Vamos entender passo a passo o que está acontecendo:

-   A constante `joke` cria um objeto similar ao que é retornado da `API`;
    
-   O `jest.spyOn` espiona as chamadas à função `fetch` do objeto `global`. É por meio deste objeto `global` que conseguimos usar qualquer função do sistema, por exemplo, a função `parseInt`;
    
-   Quando a função `fetch` for chamada, em vez de fazer uma requisição a uma `API` externa, será chamado nosso `mock`. Repare que para cada `.then` utilizamos `.mockResolvedValue` e simulamos o retorno que o `fetch` teria. Primeiro retornamos um objeto que contém a função `.json` e dentro dela criamos um mock que retorna a nossa piada, satisfazendo o que é esperado no nosso componente;
    
-   É importante termos o `async` em `it('fetch joke', async () => {`, para que se possa utilizar `await findByText` onde estamos dizendo ao nosso teste: **espere até que consiga encontrar esse texto no dom ou uma mensagem de erro por limite de tempo**;
    
-   As funções `toBeCalledTimes` e `toBeCalledWith` servem para garantir respectivamente, o número de chamadas ao nosso `fetch` e que ele foi chamado com os argumentos corretos.
    
-   A linha `afterEach(() => jest.clearAllMocks());` faz com que, após cada teste, nosso `mock` seja limpo, ou seja, no caso acima, garante que após o teste o `fetch` não seja mais um `mock`. Isso é bem útil para que não haja interferência entre um teste e outro.
    

### Segunda forma de mock do fetch

Existem diversas formas de `mockagem`! Você se lembra que a função `fetch` é uma `Promise`? Podemos então, `mockar` de outra forma (e igualmente válida) o `fetch` do exemplo acima:
```jsx
// App.test.js
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';

afterEach(() => jest.clearAllMocks());

it('fetches a joke', async () => {
  const joke = {
    id: '7h3oGtrOfxc',
    joke: 'Whiteboards ... are remarkable.',
    status: 200,
  };

  // Outra forma de mock do fetch:
  global.fetch = jest.fn(() => Promise.resolve({
    json: () => Promise.resolve(joke),
  }));

  render(<App />);
  const renderedJoke = await screen.findByText('Whiteboards ... are remarkable.');
  expect(renderedJoke).toBeInTheDocument();
  expect(global.fetch).toHaveBeenCalledTimes(1);
  expect(global.fetch).toHaveBeenCalledWith('https://icanhazdadjoke.com/', { headers: { Accept: 'application/json' } });
});
```

Nesse exemplo estamos dizendo que `global.fetch` agora é uma função `mockada` com `jest.fn` que retorna uma `Promise`, e na primeira vez que ela for resolvida, deve retornar um objeto com uma outra função `json` que também é uma `Promise`, que quando resolvida retorna sua piada.

### Terceira forma de mock do fetch

Uma _terceira_ forma de escrever o mesmo exemplo seria com a sintaxe `async/await`, onde temos o mock dessa forma:
```jsx
global.fetch = jest.fn(async () => ({
  json: async () => joke
}));
```

No exemplo acima, nós utilizamos o _mock_ para evitar uma chamada externa à API, tornando o nosso teste mais rápido e confiável, retornando o resultado contido na constante `joke`. Imagine que a API saia do ar ou que perdemos acesso à internet enquanto o teste roda. O teste quebraria, apesar de o seu código estar funcionando. _Mockar_ a chamada à API evita esse tipo de problema. Outro ponto é que seus testes vão rodar mais rápido se você não fizer uma chamada real à API todas as vezes que você for rodar seu teste.


