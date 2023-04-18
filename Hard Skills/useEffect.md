[[Teste Assincrono]]
[[React]]
[[Promise]]

## Por que usar useEffect?

Uma das ferramentas mais interessantes do React é a possibilidade de manipulação dos ciclos de vida de seus componentes. Até o momento, estas alterações eram feitas por meio dos `lifecycle methods`, conhecidos como `componentDidMount`, `componentDidUpdate` e `componentWillUnmount`.

O hook `useEffect` é uma função que pode ser utilizada para gerenciar os diferentes momentos do ciclo de vida, de forma semelhante aos três métodos citados anteriormente.

A documentação do ReactJS se refere à esta ferramenta da seguinte forma:

> **_Se você tem familiaridade com métodos de ciclo de vida de React, você pode entender o hook useEffect como uma junção de componentDidMount, componentDidUpdate e componentWillUnmount (Tradução livre)._**

## Estrutura do useEffect

Assim como todos os Hooks, o `useEffect` é uma função. Diferentemente do Hook `useState`, o `useEffect` não retorna nada. O que importa aqui são os dois argumentos que iremos passar:

-   O primeiro argumento deverá ser uma função (_callback_);
-   O segundo argumento, que é opcional, deverá ser um _array_. Ele é chamado de _array de dependências_.

Temos quatro comportamentos diferentes no `useEffect`:

#### useEffect sem segundo argumento


```jsx
useEffect(() => {});
```

Essa configuração executará a _callback_ **repetidas vezes**, toda vez que o componente sofrer qualquer tipo de alteração e renderizar. O comportamento aqui é semelhante ao `componentDidUpdate()` quando usamos componentes de classe.

Essa configuração precisa ser utilizada com **cautela**, pois facilmente resulta em **loops infinitos**.


#### useEffect com o segundo argumento sendo um array vazio.

```jsx
useEffect(() => {}, []);
```

Essa configuração executará a _callback_ apenas na primeira renderização do componente. A _callback_ será executada similarmente ao `componentDidMount`, ou seja, rodando apenas uma vez.


#### useEffect com o segundo argumento sendo um array com itens

```jsx
useEffect(() => {}, [foo, bar, ...baz]);
```

Essa configuração executará a _callback_ sempre que qualquer dos itens do array sofrer alteração. É importante colocarmos no array de dependências variáveis que estamos utilizando dentro da função _callback_: isso evita que tenhamos variáveis desatualizadas no _callback_.


#### useEffect com a _callback_ retornando uma função

```jsx
useEffect(() => {
  return () => {};
}, []);
```


Nessa caso, o `useEffect` está retornando uma nova função. Essa função também é chamada de **função _cleanup_**. A função _cleanup_ será executada:

-   No momento da desmontagem do componente. O comportamento aqui é semelhante ao `componentWillUnmount()` quando usamos componentes de classe;
-   No momento anterior à próxima execução da _callback_, quando o componente é renderizado novamente. Para saber mais, leia [esse tópico](https://beta.reactjs.org/apis/react/useEffect#my-cleanup-logic-runs-even-though-my-component-didnt-unmount) da documentação.

Você poderá utilizar a função _cleanup_ sempre que precisar limpar algo criado com [efeito colateral](https://beta.reactjs.org/learn/keeping-components-pure#side-effects-unintended-consequences) (como um `setInterval()` ou `setTimeout()`, por exemplo).

## Resumindo

Aqui vai um resumo das diferentes maneiras de utilizar o useEffect:

-   O `useEffect` executa, quando disparado, a função que recebe como primeiro parâmetro;
-   Se não receber um segundo parâmetro, o `useEffect` executa a função sempre que o componente é renderizado;
-   Se receber um array vazio como segundo parâmetro, o `useEffect` executa a função somente quando o componente é montado;
-   Quando o `useEffect` recebe um array com valores dentro, sempre que **algum** desses valores é alterado, a função é executada;
-   Se o primeiro parâmetro retornar uma função, essa função será executada quando o componente é desmontado e **também** antes da próxima renderização.

Fonte: [Course](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/095ebb0d-1932-4d37-933b-9e1d721646fb/section/94fad02a-cf1d-4277-871d-1553af1aded4/day/8afaccae-ee94-4334-9d10-2f51359f061f/lesson/aa8c353d-4971-433b-9678-c8940e18a463)
