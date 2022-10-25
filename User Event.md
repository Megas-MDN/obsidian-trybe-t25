[[Teste Assincrono]]
[[React]]
[[Promise]]



Por enquanto, estamos apenas testando se as coisas estão sendo renderizadas, mas também precisamos testar o comportamento da pessoa usuária, como um clique em um botão. Para isso, usaremos a [userEvent](https://testing-library.com/docs/ecosystem-user-event/).

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
    

## Reforçando o conteúdo

Acabamos de aprender um pouco sobre os seletores. Agora, tire alguns minutos para conferir o Cheatsheet na documentação oficial.

Lembrando que não é necessário ler todo o documento, mas sim conferir algumas das queries usadas e reforçar os conceitos!

[RTL Cheatsheet](https://testing-library.com/docs/dom-testing-library/cheatsheet)

É muito importante criarmos o hábito de ler as documentações e os artigos sobre os temas que estamos estudando ou desenvolvendo. A maioria está em inglês, então você pode aproveitar para desenvolver a habilidade de leitura nessa língua também! Mas, caso precise, pode usar as ferramentas de tradução, como a extensão `translate` do Google.
