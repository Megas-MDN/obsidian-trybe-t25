[[React]]

Para importar um arquivo que está dentro do próprio projeto ou que esteja em uma biblioteca externa, você pode utilizar o `import`, com a seguinte sintaxe:

```jsx
import myImport from 'file';
```


Onde o `myImport` é a variável pela qual você acessará o módulo importado. Caso você queira importar algo que não seja a exportação _default_, será necessário colocar o nome do que está sendo importado entre chaves:

```jsx
import { myImport } from 'file';
```

A origem do arquivo importado é indicada após o `from`, e pode ser um caminho relativo ou o nome da biblioteca que foi instalada no projeto:

Copiar

```jsx
import React from 'react' // importando de uma biblioteca
import Header from './components/Header.js' // importando de um caminho relativo
```

A utilização de CSS (estilização) em componentes React não é nada muito diferente de como é feito no `HTML`, você deve criar um arquivo para manter todo o seu `CSS` e então deverá importá-lo onde você deseja utilizá-lo e colocar as `classes` e `ids` que você criou nos elementos da sua página.

Para facilitar o entendimento veja o exemplo abaixo:

```css
/* App.css */
.App {
  background-color: #282c34;
  text-align: center;
}
```

```jsx
// App.js
import React from 'react';
import './App.css';

function App() {
  return (
    <div className='App'>
      <h1>APP</h1>
    </div>
  );
}

export default App;
```

Se quiser ver um exemplo maior da importação e utilização do `CSS`, retorne ao app `testando-meu-computador` que você criou na seção de instalação, ao observar a estrutura você verá que não é nada muito diferente do que você já estava fazendo. Caso queira se aprofundar mais na utilização do CSS no **_React_** e também no `import` utilizado no arquivo `App.js`, vá até a seção de `Recursos adicionais` e dê uma olhada nas documentações sobre esses tópicos.