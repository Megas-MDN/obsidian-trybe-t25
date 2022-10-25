[[DOM]]
[[React]]


A manipulação de eventos com elementos React é muito semelhante à manipulação de eventos em elementos DOM. Existem algumas diferenças de sintaxe:

-   Os eventos React são nomeados usando camelCase, em vez de minúsculas.
-   Com JSX você passa uma função como manipulador de eventos, ao invés de uma string.

Por exemplo, o HTML:

```html
<button onclick="activateLasers()">
  Activate Lasers
</button>
```

é um pouco diferente no React:

```jsx
<button onClick={activateLasers}>  Activate Lasers
</button>
```

Outra diferença é que você não pode retornar `false` para evitar o comportamento padrão no React. Você deve chamar `preventDefault`explicitamente. Por exemplo, com HTML simples, para evitar o comportamento padrão de envio do formulário, você pode escrever:

```jsx
<form onsubmit="console.log('You clicked submit.'); return false">
  <button type="submit">Submit</button>
</form>
```

Em React, isso poderia ser:

```jsx
function Form() {
  function handleSubmit(e) {
    e.preventDefault();    console.log('You clicked submit.');
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  );
}
```

Aqui, `e`é um evento sintético. O React define esses eventos sintéticos de acordo com a [especificação W3C](https://www.w3.org/TR/DOM-Level-3-Events/) , então você não precisa se preocupar com a compatibilidade entre navegadores. Os eventos do React não funcionam exatamente da mesma forma que os eventos nativos. Consulte o [`SyntheticEvent`](https://reactjs.org/docs/events.html)guia de referência para saber mais.

Ao usar o React, você geralmente não precisa chamar `addEventListener` para adicionar ouvintes a um elemento DOM depois que ele é criado. Em vez disso, apenas forneça um ouvinte quando o elemento for renderizado inicialmente.

Quando você define um componente usando uma [classe ES6](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) , um padrão comum é que um manipulador de eventos seja um método na classe. Por exemplo, este `Toggle`componente renderiza um botão que permite ao usuário alternar entre os estados “ON” e “OFF”:

```jsx
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback    this.handleClick = this.handleClick.bind(this);  }

  handleClick() {    this.setState(prevState => ({      isToggleOn: !prevState.isToggleOn    }));  }
  render() {
    return (
      <button onClick={this.handleClick}>        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```

[**Experimente no CodePen**](https://codepen.io/gaearon/pen/xEmzGg?editors=0010)

Você precisa ter cuidado com o significado de retornos de `this`chamada JSX. Em JavaScript, os métodos de classe não são [vinculados](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_objects/Function/bind) por padrão. Se você esquecer de vincular `this.handleClick`e passar para `onClick`, `this`será `undefined`quando a função for realmente chamada.

Este não é um comportamento específico do React; é uma parte de [como as funções funcionam em JavaScript](https://www.smashingmagazine.com/2014/01/understanding-javascript-function-prototype-bind/) . Geralmente, se você se referir a um método sem `()`depois dele, como `onClick={this.handleClick}`, você deve vincular esse método.

Se ligar `bind` te incomoda, há duas maneiras de contornar isso. Você pode usar [a sintaxe de campos de classe pública](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Public_class_fields#public_instance_fields) para vincular corretamente os retornos de chamada:

```jsx
class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.  handleClick = () => {    console.log('this is:', this);  };  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

Essa sintaxe é habilitada por padrão em [Create React App](https://github.com/facebookincubator/create-react-app) .

Se você não estiver usando a sintaxe de campos de classe, poderá usar uma [função de seta](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions) no retorno de chamada:

```jsx
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // This syntax ensures `this` is bound within handleClick    return (      <button onClick={() => this.handleClick()}>        Click me
      </button>
    );
  }
}
```

O problema com essa sintaxe é que um retorno de chamada diferente é criado toda vez que o `LoggingButton`renderiza. Na maioria dos casos, isso é bom. No entanto, se esse retorno de chamada for passado como um suporte para componentes inferiores, esses componentes poderão fazer uma nova renderização extra. Geralmente, recomendamos vincular no construtor ou usar a sintaxe de campos de classe para evitar esse tipo de problema de desempenho.

## Passando argumentos para manipuladores de eventos

Dentro de um loop, é comum querer passar um parâmetro extra para um manipulador de eventos. Por exemplo, se `id`for o ID da linha, qualquer uma das seguintes opções funcionará:

```jsx
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

As duas linhas acima são equivalentes e usam [as funções de seta](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) e [`Function.prototype.bind`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)respectivamente.

Em ambos os casos, o `e`argumento que representa o evento React será passado como um segundo argumento após o ID. Com uma função de seta, temos que passá-la explicitamente, mas com `bind`quaisquer outros argumentos são encaminhados automaticamente.

Fonte: https://reactjs.org/docs/handling-events.html#passing-arguments-to-event-handlers