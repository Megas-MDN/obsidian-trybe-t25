
[[React]]
[[Conceitos do RTL]]

![[RTL.png]]


No conteúdo de testes já visto no curso, funções eram testadas. Já no `RTL` o objetivo é testar comportamento, como se algo aparece ou não na tela. Por exemplo:

-   Podemos testar se a nossa página possui um título específico;
-   Em uma lista de tarefas, como o projeto `To do list`, precisamos verificar, por exemplo, se a funcionalidade de adicionar uma nova tarefa funciona. Para isso, devemos simular o comportamento de quem usa, que seria adicionar um texto no campo de _texto alvo_ e clicar no botão que adiciona a nova tarefa. Para testar se funcionou, verificamos se o texto aparece em algum lugar da página. O `RTL` nos dá as ferramentas necessárias para realizar essa simulação!

Esses são apenas alguns dentre muitos exemplos! Agora, veremos por meio de um passo a passo a estrutura desses testes e suas ferramentas:

-   **Passo 1**: Crie uma nova aplicação com o comando `npx create-react-app testes-react`. Note que a biblioteca RTL já vem instalada nos novos projetos.
-   **Passo 2**: Abra a aplicação no `VSCode` e o arquivo `App.test.js`.
-   **Passo 3**: Observe o arquivo `App.test.js`:

```jsx
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});
```

Note que ele está fazendo uma verificação se algum elemento dentro do componente `App` possui o texto “learn react” (`_/string/i_` é utilizado para ignorar _case sensitive_, ou seja, não diferenciar letras maiúsculas e minúsculas).

Para rodar os testes vá para a pasta `src` e execute `npm test`. Caso apareça a mensagem abaixo basta clicar na tecla “a”.

![[RTL1.webp]]
> Terminal mostrando que não encontrou nenhum teste

Após clicar a tecla “a”, este deve ser o resultado:
![[RTL2.webp]]
> Terminal mostrando quais testes passaram ou não passaram da aplicação.

Como podemos ver, o nosso único teste passou. Quer dizer que existe o texto “learn react” dentro do componente `App`! Se rodar aplicação com o `npm start`, você encontrará o texto “learn react”, conforme indicado pelo teste.
Agora, vamos provocar um erro ou uma falha. Mude o texto “learn react” para “algo que não aparece” e rode o teste. Seu terminal acusará este erro:
![[RTL3.webp]]
> Parte inicial do erro

Observe que ele está falando que não foi possível encontrar um elemento o qual possui o texto “/algo que não aparece/i”.

Agora, dê uma olhada na cheatsheet da `react-testing-library`. Ela explica de forma resumida como a biblioteca funciona. Nos aprofundaremos nas explicações posteriormente!

Ao executar o comando `npx create-react-app`, por padrão, é criado o arquivo `setupTests.js`. Dentro dele, temos comentários e uma importação; esta importação fornece para nossos testes o que chamamos de `seletores customizados do Jest` (`custom jest matchers`). O `.toBeInTheDocument()`, no exemplo acima, é um deles, e você pode consultar outros na documentação do [[Jest]]-[[DOM]] sempre que precisar.

## Renderização

Testar um componente significa, em poucas palavras, renderizá-lo em um browser real ou em uma simulação de um browser e testar nele o comportamento desejado. Na `RTL`, é necessário o uso da função `render()` para fazer isso. A função `render()` faz a renderização de um componente em memória para que se possa simular as interações com esse componente.
```jsx
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});
```

Para usar o seletor/query `getByText`, precisamos usar o `screen.getByText`. Observe que ele é muito parecido com os seletores do DOM, como o `document.getElementById()` ou `document.querySelector()`.

Seguindo a mesma lógica, ao usar o `screen.getByText()`, ele retornará um elemento html. A vantagem de utilizar o `screen` é que você não precisará atualizar e desestruturar a chamada do render para todo teste que você fizer, pois é possível consultar e utilizar todos os elementos do DOM por meio do próprio `screen`. Em outras palavras, ele receberá um objeto com os elementos contidos no DOM e você poderá acessar as propriedades desse objeto através dele.

## Seletores

`Seletores` ou `Queries` são métodos que usamos para indicar ao RTL algum elemento da nossa aplicação e assim podermos realizar nossos testes e comparações.

Veremos agora algumas formas de buscar por algum elemento HTML. No exemplo anterior, foi visto apenas o `getByText` o qual busca por um elemento que possui determinado texto. 

Todos os seletores (queries) estão disponíveis nessa [lista de queries](https://testing-library.com/docs/dom-testing-library/api-queries) da `react-testing-library`, mas não é necessário ler toda a documentação! Use-a para tirar dúvidas ou procurar algum assunto específico. Além disso, veremos algumas queries durante a aula.

Mas como fazer para buscar um elemento que não possui um texto? Como um input? Para isso, existem outros seletores.

Vamos acrescentar um input de e-mail ao arquivo `App.js`:
```jsx
// App.js
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <label htmlFor="id-email">
        Email
        <input id="id-email" type="email" />
      </label>
    </div>
  );
}

export default App;
```

Pronto, mudamos a estrutura e adicionamos um campo email com uma label dentro do nosso arquivo `App.js`. Agora, precisamos testar se esse input está, de fato, aparecendo na tela. Como ele não possui um texto, não podemos usar o `getByText`, mas podemos usar o `getByLabelText`, onde ele pegará o input de acordo com o texto da `label` que está associado a ele. Nesse caso, o input está relacionado com a label `Email`.
```jsx
// App.test.js
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';

test('Verificando se existe o campo Email.', () => {
  render(<App />);
  const inputEmail = screen.getByLabelText('Email');
  expect(inputEmail).toBeInTheDocument();
  expect(inputEmail).toHaveProperty('type', 'email');
});
```

Como pode ver, mudamos os `expects` também, verificando se o elemento está na tela e é do tipo correto.
Mas e se um campo não tiver texto nem label? Podemos usar o `getByRole`. Ele busca pelo atributo role. No caso de um botão, o _role_ é definido pela propriedade `type="button"`. O _role_ serve, por exemplo, para buscar por um elemento `<button>Enviar<button/>` ou `<input type="button" value="Enviar" />`.

Adicione um botão ao `App.js`.
```jsx
// App.js
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <label htmlFor="id-email">
        Email
        <input id="id-email" type="email" />
      </label>
      <input id="btn-send" type="button" value="Enviar" />
    </div>
  );
}

export default App;
```

Também adicione o teste abaixo dentro do arquivo `App.test.js`:

```jsx
test('Verificando se existe um botão', () => {
  render(<App />);
  const btn = screen.getByRole('button');
  expect(btn).toBeInTheDocument();
});
```

Agora, adicione um novo botão na aplicação.
```jsx
// App.js
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <label htmlFor="id-email">
        Email
        <input id="id-email" type="email" />
      </label>
      <input id="btn-send" type="button" value="Enviar" />
      <input id="btn-back" type="button" value="Voltar" />
    </div>
  );
}

export default App;
```

Note que, ao rodar os testes ocorre um erro. O que acontece é que o `getByRole` espera encontrar apenas um elemento, mas acaba encontrando dois, o botão de `Enviar` e o de `Voltar`, pois ambos possuem o _role_ `button`, retornando a mensagem `Found multiple elements with the role "button"`. Para resolver esse problema, precisamos usar outro seletor, o `getAllByRole`, que armazenará todos os valores encontrados pelo seletor em um array.

Para testar, precisamos mudar o teste para:
```jsx
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';

test('Verificando se existe o campo Email.', () => {
  render(<App />);
  const inputEmail = screen.getByLabelText('Email');
  expect(inputEmail).toBeInTheDocument();
  expect(inputEmail).toHaveProperty('type', 'email');
});

// test('Verificando se existe um botão', () => {
//   const { getByRole } = render(<App />);
//   const btn = getByRole('button');
//   expect(btn).toBeInTheDocument();
// });

test('Verificando se existem dois botões', () => {
  render(<App />);
  const buttons = screen.getAllByRole('button');
  expect(buttons).toHaveLength(2);
});
```

Observe que usamos `buttons` juntamente com `toHaveLength` para verificar se foram encontrados dois botões. Com isso, não precisamos usar o `toBeInTheDocument` para realizar a verificação de presença no documento!

Foi necessário comentar o nosso segundo teste para não ocorrer um erro. Com isso, teremos que modificá-lo para verificar se existe um botão de enviar. Para isso usaremos a query `getByTestId`. Para usá-la, devemos adicionar uma propriedade ao nosso botão de enviar, o `data-testid`, que é um identificador para a biblioteca de testes.
```jsx
// App.js
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <label htmlFor="id-email">
        Email
        <input id="id-email" type="email" />
      </label>
      <input id="btn-send" type="button" data-testid="id-send" value="Enviar" />
      <input id="btn-back" type="button" value="Voltar" />
    </div>
  );
}

export default App;
```

O teste ficará assim:
```jsx
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';

test('Verificando se existe o campo Email.', () => {
  render(<App />);
  const inputEmail = screen.getByLabelText('Email');
  expect(inputEmail).toBeInTheDocument();
  expect(inputEmail).toHaveProperty('type', 'email');
});

test('Verificando se existem dois botões', () => {
  render(<App />);
  const buttons = screen.getAllByRole('button');
  expect(buttons).toHaveLength(2);
});

test('Verificando se existe um botão de enviar', () => {
  render(<App />);
  const btnSend = screen.getByTestId('id-send');
  expect(btnSend).toBeInTheDocument();
  expect(btnSend).toHaveProperty('type', 'button');
  expect(btnSend).toHaveValue('Enviar');
});
```

Buscamos o elemento pelo `data-testid` e verificamos se ele está na tela. Em seguida, verificamos se este elemento é um botão e, com a propriedade `toHaveValue`, conferimos se possui o texto `Enviar`.


Por enquanto, estamos apenas testando se as coisas estão sendo renderizadas, mas também precisamos testar o comportamento da pessoa usuária, como um clique em um botão. Para isso, usaremos a [[User Event]] (https://testing-library.com/docs/ecosystem-user-event/).

A `user-event` é uma biblioteca _complementar_ à React Testing Library (RTL) que possibilita a simulação de várias interações com o navegador. Essa biblioteca é baseada no método `fireEvent` da React Testing Library, mas seus métodos são mais aproximados da interação da pessoa usuária.

Enquanto um `fireEvent.change(input, { target: { value: 'hello world' } })` dispara um evento de alteração do campo de input, um `userEvent.type(input, 'hello world')` testará interações **keyDown, keyPress e keyUp** para cada caractere digitado. Portanto é uma boa prática, e altamente recomendado utilizar `userEvent` ao invés de `fireEvent`, **sempre que possível**.

Você pode consultar a [documentação](https://github.com/testing-library/user-event) com os eventos do `userEvent` e a [lista completa](https://github.com/testing-library/dom-testing-library/blob/master/src/event-map.js) de eventos suportados pelo `fireEvent`.

A maioria dos métodos do userEvent são síncronos, exceto quando utilizar o userEvent.type, pois ele aguarda a informação que será testada.

O type possui três parâmetros, sendo o terceiro parâmetro opcional, **type(element, text, [options])**. Esse terceiro parâmetro pode ser utilizado para passar um _delay_, em milissegundos, que será o tempo esperado entre dois caracteres digitados para realizar a ação do teste.

> Você pode utilizar essa opção caso queira testar o comportamento de uma pessoa usuária com maior ou menor agilidade de digitação, o valor _default_ para o delay é **0**.


O userEvent.type é um evento que retorna uma Promise, porém, como valor default é 0, você só precisará aguardar o retorno dessa Promise caso passe algum valor para a option _delay_, do contrário o userEvent.type funcionará de modo síncrono.

Modificaremos nosso `App.js` para que quem usa possa inserir o seu e-mail no campo, salvá-lo e mostrá-lo na tela:
```jsx
// App.js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      email: '',
      saveEmail: '',
    };
  }

  changeEmail(value) {
    this.setState({ email: value });
  }

  changeSaveEmail(value) {
    this.setState({ saveEmail: value, email: '' });
  }

  render() {
    const { email, saveEmail } = this.state;
    return (
      <div className="App">
        <label htmlFor="id-email">
          Email
          <input
            id="id-email"
            value={ email }
            type="email"
            onChange={ (e) => this.changeEmail(e.target.value) }
          />
        </label>
        <input
          id="btn-enviar"
          type="button"
          data-testid="id-send"
          value="Enviar"
          onClick={ () => this.changeSaveEmail(email) }
        />
        <input id="btn-id" type="button" value="Voltar" />
        <h2 data-testid="id-email-user">{`Valor: ${saveEmail}`}</h2>
      </div>
    );
  }
}

export default App;
```


Observe as mudanças que foram feitas.

Rode a aplicação e a teste manualmente, adicionando seu email no campo e clicando no botão de enviar. Veja se seu email foi salvo.

Agora, iremos automatizar cada passo que você fez no código usando o `userEvent`, para não precisar testar manualmente cada passo desses toda vez que alterar o código. Bastará, ao invés disso, apenas rodar o `npm test`.

Para utilizar o `userEvent` é necessário importar a biblioteca para o arquivo onde o teste será realizado:

```jsx
import userEvent from '@testing-library/user-event';
```

Observe cada linha do teste:

```jsx
// App.test.js
import React from 'react';
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import App from './App';


// Adicione esse teste.
test('Verificando se o botão e o campo email estão funcionando.', () => {
  render(<App />);

  const EMAIL_USER = 'email@email.com';

  const textEmail = screen.getByTestId('id-email-user');
  expect(textEmail).toBeInTheDocument();
  expect(textEmail).toHaveTextContent('Valor:');

  const btnSend = screen.getByTestId('id-send');
  const inputEmail = screen.getByLabelText('Email');
  userEvent.type(inputEmail, EMAIL_USER);
  userEvent.click(btnSend);

  expect(inputEmail).toHaveValue('');
  expect(textEmail).toHaveTextContent(`Valor: ${ EMAIL_USER }`);
});
```

Agora, vamos entender o passo a passo:

-   **Passo 1**: Renderizamos a aplicação, depois salvamos o email da pessoa usuária em uma variável (o que é uma boa prática).
-   **Passo 2**: Verificamos se a tag `<h2>` onde o email aparece na tela está apenas com o texto `Valor:`,
-   **Passo 3**: Procuramos pelo o campo de email e o botão que enviará os dados.
-   **Passo 4**: Simulamos a digitação da pessoa usuária no campo de email, com o `userEvent.type(inputEmail, EMAIL_USER)`, passando o campo do input como primeiro parâmetro e o valor esperado como segundo parâmetro (`'email@email.com'`).
-   **Passo 5**: Simulamos um clique no botão com o `userEvent.click(btnSend)`, passando o elemento do botão como parâmetro.
-   **Passo 6**: Verificamos se após o `click`, o campo de input do email retorna para vazio e se a tag `<h2>`, que anteriormente só exibia `Valor:`, agora recebe o email passado ao input, resultando em `Valor: email@email.com`.

# Testando apenas um componente

Agora, imagine que você está escrevendo um teste para a aplicação, mas precisa apenas testar **_um componente_** que você criou ou ainda vai criar. Não é preciso que você renderize toda a sua aplicação para realizar um teste: é possível renderizar apenas aquele componente específico e criar os testes para ele.

Para isso, usaremos a mesma aplicação que vimos anteriormente e criaremos um componente que mostra se o email é válido ou não.

**Passo 1:** Crie o componente `ValidEmail.js`:

```jsx
// ValidEmail.js
import React from 'react';
import PropTypes from 'prop-types';

const verifyEmail = (email) => {
  const emailRegex = /[^@ \t\r\n]+@[^@ \t\r\n]+\.[^@ \t\r\n]+/;
  return emailRegex.test(email);
};

const ValidEmail = (props) => {
  const { email } = props;
  return (
    <div>
      <h2 data-testid="id-email-user">{`Valor: ${email}`}</h2>
      <h3>{(verifyEmail(email) ? 'Email Válido' : 'Email Inválido')}</h3>
    </div>
  );
};

ValidEmail.propTypes = {
  email: PropTypes.string.isRequired,
};

export default ValidEmail;
```

**Passo 2:** Substitua a linha do `h2` no `App.js` e não esqueça de importar o `ValidEmail`:

```jsx
<h2 data-testid="id-email-user">{ `Valor: ${ saveEmail }` }</h2>
// Substitua a linha de cima pela a debaixo.
<ValidEmail email={ saveEmail } />
```

**Passo 3:** Rode os testes e observe que mesmo sem mudar nenhum, todos eles passaram, assegurando que nossa aplicação continua funcionando mesmo após essa mudança (super conveniente, certo?). Agora, falta testar essa funcionalidade nova que adicionamos. Mas, testaremos apenas renderizando o nosso componente `ValidEmail`.

**Passo 4:** Crie um arquivo `ValidEmail.test.js`.

```jsx
import React from 'react';
import { render, screen } from '@testing-library/react';
import ValidEmail from './ValidEmail';

test('Testando um componente, caso o email seja válido.', () => {
  const EMAIL_USER = 'email@email.com';
  render(<ValidEmail email={ EMAIL_USER } />);
  const isValid = screen.getByText('Email Válido');
  expect(isValid).toBeInTheDocument();
});
```

Observe que a estrutura é bem semelhante comparada com a dos outros testes. O que foi modificado é o que está sendo renderizado.

No lugar de `render(<App />)`, colocamos `render(<ValidEmail email={ EMAIL_USER } />)`. O componente que queremos renderizar precisa de uma **props** para funcionar, portanto precisamos passar um valor para ela, que no caso é `email={ EMAIL_USER }`. O teste verifica se, com a prop passada, o nosso teste passará.

Já estamos testando o cenário onde o email é válido, agora precisamos testar o cenário contrário, ou seja, quando o email é inválido. Para isso, basta criar um novo teste, definindo a constante `EMAIL_USER` com o valor de um email inválido e alterando o texto buscado para `Email inválido`.

**Passo 5:** Adicione o teste abaixo e rode os testes:

```jsx
test('Testando um componente, caso o email seja inválido.', () => {
  const EMAIL_USER = 'emailerrado';
  render(<ValidEmail email={ EMAIL_USER } />);
  const isValid = screen.getByText('Email Inválido');
  expect(isValid).toBeInTheDocument();
});
```

###### Fonte: [Curse - Seção: Testes automatizados com React Testing Library](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/095ebb0d-1932-4d37-933b-9e1d721646fb/section/89bf51d9-0bcc-4c9f-86a5-c7ff5df910bc/day/d57d0d2f-3835-4729-92e4-ff75370f6769/lesson/3bb680f8-45e1-4004-a4d5-5acd205e8833)
