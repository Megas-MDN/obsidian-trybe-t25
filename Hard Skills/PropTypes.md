[[React]]
[[Props]]


Outro importante fundamento do _React_ é a **checagem de tipos**! Imagine que você criou um componente reutilizável e que ele, para funcionar corretamente, precisa receber determinadas _props_ de tipos específicos, caso contrário, a aplicação quebrará. A checagem de tipos ajuda a previnir cenários como esse, pois verifica os tipos das `props` passadas para um componente durante o desenvolvimento e levanta um _warning_ se algo não estiver como planejado. Como deve ter notado, essa verificação previne inúmeros erros, economizando muito tempo de desenvolvimento!

A melhor forma para compreender o uso dessa ferramenta é visualizar um exemplo prático e destrinchá-lo:

```jsx
import React from 'react';
import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    const { name, lastName } = this.props;
    return (<h1>Hello, {name} {lastName}</h1>);
  }
}

Greeting.propTypes = {
  name: PropTypes.string,
  lastName: PropTypes.string,
};

export default Greeting;
```

1.  O primeiro passo para utilizar o _prop-types_ é importá-lo no componente:

```jsx
import PropTypes from 'prop-types';
```

Caso **não** tenha utilizado o `create-react-app` para preparar o aplicativo **React**, será necessário o _download_ da depedência externa do **PropTypes** através do seguinte comando:

```bash
npm install --save-dev prop-types
```

2.  Em seguida, para executarmos a checagem de tipos no componente `Greeting`, adicionamos a seguinte estrutura antes do `export default`:

```jsx
Greeting.propTypes = {
  name: PropTypes.string,
  lastName: PropTypes.string,
};
```

É dentro dessa estrutura que ocorre a checagem das `props`. Basta pegarmos o nome da `prop` que queremos _tipar_ e usar a sintaxe de identificação apropriada para o caso. À primeira vista, pode parecer confuso, por isso vamos ao exemplo:

1.  A primeira `prop` que queremos _tipar_ é a `name`. Queremos ter certeza que ela sempre será uma `prop` do tipo `string`, **caso ao contrário nossa aplicação pode quebrar**. Para isso:

```jsx
// ...
name: PropTypes.string,
// ...
```

2.  A outra `prop` que falta ser _tipada_, `lastName`, se encontra em uma situação bem semelhante à anterior. Então repetimos o processo, trocando apenas o nome da `prop`:

```jsx
// ...
name: PropTypes.string,
lastName: PropTypes.string,
// ...
```

Agora podemos ter certeza de que, caso o componente seja renderizado com alguma `prop` de tipo inválido, o **console disparará um aviso**, facilitando muito o processo de _debugging_.

E, caso o nosso componente seja renderizado sem nenhum valor numa `prop`, ainda será disparado o aviso? Em casos como esse, no qual as `props` são _essenciais_ para o bom funcionamento do componente, é importante acrescentar o `.isRequired` - inglês para _“é obrigatório”_ - após a definição do tipo da `prop`:
```jsx
Greeting.propTypes = {
  name: PropTypes.string.isRequired,
  lastName: PropTypes.string.isRequired,
};
```

Desse modo, sempre que o componente for renderizado sem uma das `props` ou com alguma do tipo errado, um aviso será disparado.

Abaixo seguem alguns dos principais validadores oferecidos pela **PropTypes**. 

```jsx
MyComponent.propTypes = {
  // Todos os validadores aqui são, por padrão, validadores opcionais.
  // Para torná-los obrigatórios, basta adicionar .isRequired
  numeroObrigatorio: PropTypes.number.isRequired,

  // Tipos básicos do JS.
  stringOpcional: PropTypes.string,
  numeroOpcional: PropTypes.number,
  booleanoOpcional: PropTypes.bool,
  funcaoOpcional: PropTypes.func,
  objetoOpcional: PropTypes.object,
  arrayOpcional: PropTypes.array,

  // Um array de determinado tipo básico
  arrayDeNumeros: PropTypes.arrayOf(PropTypes.number),

  // Um objeto de determinado tipo básico
  objetoDeNumeros: PropTypes.objectOf(PropTypes.number),

  // Um objeto com forma específica
  objetoComForma: PropTypes.shape({
    name: PropTypes.string,
    age: PropTypes.number,
  }),

  // Um objeto que não permite props extras
  objetoComFormatoRigoroso: PropTypes.exact({
    name: PropTypes.string,
    quantity: PropTypes.number,
    availability: PropTypes.bool,
  }),
};
```

