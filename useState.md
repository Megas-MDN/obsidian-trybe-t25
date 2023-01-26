[[React Hooks - useState e useEffect]]
[[React]]
[[Funções]]


O `useState` é o _hook_ mais comum do React, ele permite que você utilize o estado do **React** em componentes funcionais. Para começar, assista ao vídeo abaixo que mostra na prática como refatorar uma aplicação que foi escrita utilizando classes para uma que utiliza funções.

Para entender melhor o que estamos falando, veja este contador feito com um componente de classe e, em seguida, o mesmo componente feito com Hooks:


```jsx
// ./src/App.js
import React, { Component } from 'react';

class App extends Component {
  constructor() {
    super();
    this.state = {
      counter: 0,
    };
  }

  render() {
    const { counter } = this.state;

    return (
      <div>
        <div>Counter: {counter}</div>
        <button
          type="button"
          onClick={() =>
            this.setState((prevState) => ({ counter: prevState.counter + 1 }))
          }
        >
          Increase Counter
        </button>
      </div>
    );
  }
}

31export default App;
```

Agora, vamos criar esse mesmo componente usando função e Hooks:

```jsx
// ./src/App.js
import React, { useState } from 'react';

function App() {
  const [counter, setCounter] = useState(0);
  return (
    <div>
      <div>Counter: {counter}</div>
      <button type="button" onClick={() => setCounter(counter + 1)}>
        Increase Counter
      </button>
    </div>
  );
}

export default App;
```

#### Estrutura do useState

No exemplo anterior, observe a linha de código `const [counter, setCounter] = useState(0)`. Vamos entender o que está acontecendo.

Assim como qualquer Hook, o `useState` é uma função. No caso específico desse Hook, ele **recebe um argumento**, que será o estado inicial e **retorna um `array`** com dois, e apenas dois, itens:

-   O primeiro item do `array` retornado é a variável que armazena o estado;
-   O segundo item do `array` é uma função que serve para escrever e atualizar o estado:
    -   Note que, para atualizar o estado, você **sempre** precisará utilizar essa função, e nunca manipular a variável de estado diretamente;
    -   Essa função receberá o novo valor a ser atualizado no estado.

Observe que para conseguimos acessar os dados do array retornado pelo `useState()`, precisamos usar a [desestruturação de array](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#desestrutura%C3%A7%C3%A3o_de_array). Quando desestruturamos um array é importante a posição em que cada item se encontra. Dessa forma, podemos utilizar a estrutura `[ nomeDoEstado, setNomeDoEstado ]`, para acessar a variável que armazena o estado e a função para escrever e atualizar o estado, respectivamente.

Você deve ter percebido que por convenção utilizamos o prefixo **_set_** para nomear a função que escreve e atualiza o estado.

#### Outras diferenças em relação a classes

Podemos perceber outras diferenças no nosso exemplo:

-   Nosso _event handler_ `onClick` também mudou. No lugar de `this.setState`, temos somente a chamada da função `setCounter` definida anteriormente, recebendo como parâmetro o novo valor de `counter`, neste caso `counter + 1`;
    
-   Observe que tanto `this.setState` quanto `setCounter` possuem o objetivo de atualizar o estado do componente. Da mesma forma que valores atualizados por `this.setState` acontecem de forma assíncrona, mudanças utilizando `setCounter` também não são instantâneas.
    
-   Com o `useState`, no lugar de termos todos os estados do componente dentro de um grande objeto, podemos ter um `useState` diferente para cada valor de estado que estiver sendo utilizado.
    
-   A atualização do estado ocorre de forma diferente com o `this.setState` e o `useState`. No caso das classes, você pode atualizar parcialmente um valor do estado. No Hook, o estado será completamente substituído pelo novo estado. Para entender mais, você pode [ler a documentação](https://beta.reactjs.org/learn/updating-objects-in-state).



Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/095ebb0d-1932-4d37-933b-9e1d721646fb/section/94fad02a-cf1d-4277-871d-1553af1aded4/day/8afaccae-ee94-4334-9d10-2f51359f061f/lesson/4b76c901-1037-428e-ba8f-02acc1a963f3)

