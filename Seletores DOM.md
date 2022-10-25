[[DOM]]
[[JavaScript]]

Vamos a um exemplo! Suponha que você quer acessar o texto que está dentro da `<div>` de um site. Você pode estar baixando informações de sua página para alimentar uma base de dados, por exemplo.

Utilizando _JavaScript_ você pode, com código, recuperar exatamente o texto que está dentro da `<div>` que você quiser.

Para entender como você pode fazer isso, vamos aprender a usar a função `getElementById`.

Observe bem: após recuperar algum elemento via _JavaScript_, você pode alterá-lo! Para começar a praticar, copie para um arquivo em sua máquina o exemplo abaixo.

```html
<!DOCTYPE html>
<html>
  <body>
    <header>
      <h2 id="page-title">Título</h2>
      <p id="paragraph">Dê uma cor para este parágrafo!</p>
      <h4 id="subtitle">Subtítulo</h4>
      <p id="second-paragraph">Segundo parágrafo!</p>
    </header>
    <script>
      const paragraph = document.getElementById("paragraph");
      paragraph.style.color = "red";
    </script>
  </body>
</html>
```

Agora, você! Faça o seguinte:

-   Recupere o elemento que contém o título da página e faça algo com ele, por exemplo alterá-lo para o nome do seu filme favorito.
-   Agora recupere o segundo parágrafo e use sua criatividade para alterá-lo.
-   Por fim, recupere o subtítulo e altere-o também.

Existem diversas formas de você acessar o conteúdo dos elementos do seu _HTML_. Aí vão algumas!
```html
<!DOCTYPE html>
<html>
  <body>
    <header>
      <h2 id="page-title">Título</h2>
      <p id="paragraph">Dê uma cor para este parágrafo!</p>
      <h4 id="subtitle">Subtítulo</h4>
      <p id="second-paragraph">Segundo parágrafo!</p>
    </header>
    <script>
      const paragraph = document.getElementById("paragraph");
      paragraph.style.color = "red";
    </script>
  </body>
</html>
```

-   Adicione uma classe igual para os dois parágrafos;
-   Recupere os seus parágrafos via código _JavaScript_, usando a função `getElementsByClassName`;
-   Altere algum estilo do primeiro deles;
-   Recupere o subtítulo e altere a cor dele usando a função `getElementsByTagName`.

Há uma função única que você pode usar para acessar qualquer elemento: o `querySelector`.

Mas como fazer uma busca que retorna vários elementos e não apenas o primeiro? Bem, para isso existe o `querySelectorAll`, que tem comportamento semelhante ao `querySelector`. A diferença é simples: ela retorna uma array com todos os elementos que _“casem”_ com a sua seleção, em vez de retornar apenas o primeiro deles. Veja o vídeo a seguir para entender melhor essa função.

Tanto o `querySelector` quanto o `querySelectorAll` acessam CSS Selectors de todos os tipos. Ou seja, eles podem acessar muito além de valores de ids e classes. Para saber mais sobre CSS Selectors, clique [aqui](https://www.w3schools.com/cssref/css_selectors.asp).

Vamos a um exemplo! Suponha que você quer acessar o texto que está dentro da `<div>` de um site. Você pode estar baixando informações de sua página para alimentar uma base de dados, por exemplo.

Utilizando _JavaScript_ você pode, com código, recuperar exatamente o texto que está dentro da `<div>` que você quiser.

Para entender como você pode fazer isso, vamos aprender a usar a função `getElementById`.

Observe bem: após recuperar algum elemento via _JavaScript_, você pode alterá-lo! Para começar a praticar, copie para um arquivo em sua máquina o exemplo abaixo.

```html
<!DOCTYPE html>
<html>
  <body>
    <header>
      <h2 id="page-title">Título</h2>
      <p id="paragraph">Dê uma cor para este parágrafo!</p>
      <h4 id="subtitle">Subtítulo</h4>
      <p id="second-paragraph">Segundo parágrafo!</p>
    </header>
    <script>
      const paragraph = document.getElementById("paragraph");
      paragraph.style.color = "red";
    </script>
  </body>
</html>
```

Agora, você! Faça o seguinte:

-   Recupere o elemento que contém o título da página e faça algo com ele, por exemplo alterá-lo para o nome do seu filme favorito.
-   Agora recupere o segundo parágrafo e use sua criatividade para alterá-lo.
-   Por fim, recupere o subtítulo e altere-o também.

Existem diversas formas de você acessar o conteúdo dos elementos do seu _HTML_. Aí vão algumas!

```html
<!DOCTYPE html>
<html>
  <body>
    <header>
      <h2 id="page-title">Título</h2>
      <p id="paragraph">Dê uma cor para este parágrafo!</p>
      <h4 id="subtitle">Subtítulo</h4>
      <p id="second-paragraph">Segundo parágrafo!</p>
    </header>
    <script>
      const paragraph = document.getElementById("paragraph");
      paragraph.style.color = "red";
    </script>
  </body>
</html>
```

-   Adicione uma classe igual para os dois parágrafos;
-   Recupere os seus parágrafos via código _JavaScript_, usando a função `getElementsByClassName`;
-   Altere algum estilo do primeiro deles;
-   Recupere o subtítulo e altere a cor dele usando a função `getElementsByTagName`.

Há uma função única que você pode usar para acessar qualquer elemento: o `querySelector`.

Mas como fazer uma busca que retorna vários elementos e não apenas o primeiro? Bem, para isso existe o `querySelectorAll`, que tem comportamento semelhante ao `querySelector`. A diferença é simples: ela retorna uma array com todos os elementos que _“casem”_ com a sua seleção, em vez de retornar apenas o primeiro deles. Veja o vídeo a seguir para entender melhor essa função.

Tanto o `querySelector` quanto o `querySelectorAll` acessam CSS Selectors de todos os tipos. Ou seja, eles podem acessar muito além de valores de ids e classes. Para saber mais sobre CSS Selectors, clique [aqui](https://www.w3schools.com/cssref/css_selectors.asp).

  
Observe bem: após recuperar algum elemento via _JavaScript_, você pode alterá-lo! Para começar a praticar, copie para um arquivo em sua máquina o exemplo abaixo.

Copiar

```html
<!DOCTYPE html>
<html>
  <body>
    <header>
      <h2 id="page-title">Título</h2>
      <p id="paragraph">Dê uma cor para este parágrafo!</p>
      <h4 id="subtitle">Subtítulo</h4>
      <p id="second-paragraph">Segundo parágrafo!</p>
    </header>
    <script>
      const paragraph = document.getElementById("paragraph");
      paragraph.style.color = "red";
    </script>
  </body>
</html>
```

Agora, você! Faça o seguinte:

-   Recupere o elemento que contém o título da página e faça algo com ele, por exemplo alterá-lo para o nome do seu filme favorito.
-   Agora recupere o segundo parágrafo e use sua criatividade para alterá-lo.
-   Por fim, recupere o subtítulo e altere-o também.
-   Recupere o elemento que contém o título da página e faça algo com ele, por exemplo alterá-lo para o nome do seu filme favorito.


```html
    <script>
      // const paragraph = document.getElementById('paragraph');
      // paragraph.style.color = 'red';
      const title = document.getElementById('page-title');
      title.innerText = 'The hitchhiker\'s guide to the galaxy';
    </script>
```

-   Agora recupere o segundo parágrafo e use sua criatividade para alterá-lo.

```html
    <script>
      // const paragraph = document.getElementById('paragraph');
      // paragraph.style.color = 'red';
      // const title = document.getElementById('page-title');
      // title.innerText = 'The hitchhiker\'s guide to the galaxy';
      const secondParagraph = document.getElementById('second-paragraph');
      secondParagraph.innerText = 'The answer to life the universe and everything is 42.';
    </script>
```

-   Por fim, recupere o subtítulo e altere-o também.

```html
    <script>
      // const paragraph = document.getElementById('paragraph');
      // paragraph.style.color = 'red';
      // const title = document.getElementById('page-title');
      // title.innerText = 'The hitchhiker\'s guide to the galaxy';
      // const secondParagraph = document.getElementById('second-paragraph');
      // secondParagraph.innerText = 'The answer to life the universe and everything is 42.';
      const subtitle = document.getElementById('subtitle');
      subtitle.innerText = 'So long and thanks for all the fish';
    </script>
```


```html
<!DOCTYPE html>
<html>
  <body>
    <header>
      <h2 id="page-title">Título</h2>
      <p id="paragraph">Dê uma cor para este parágrafo!</p>
      <h4 id="subtitle">Subtítulo</h4>
      <p id="second-paragraph">Segundo parágrafo!</p>
    </header>
    <script>
      const paragraph = document.getElementById("paragraph");
      paragraph.style.color = "red";
    </script>
  </body>
</html>
```

-   Adicione uma classe igual para os dois parágrafos;
-   Recupere os seus parágrafos via código _JavaScript_, usando a função `getElementsByClassName`;
-   Altere algum estilo do primeiro deles;
-   Recupere o subtítulo e altere a cor dele usando a função `getElementsByTagName`.
-   Adicione uma classe igual para os dois parágrafos;

```html
<!DOCTYPE html>
<html>
  <body>
    <header>
      <!-- <h2 id="page-title">Título</h2> -->
      <p class="para" id="paragraph">Dê uma cor para este parágrafo!</p>
      <!-- <h4 id="subtitle">Subtítulo</h4> -->
      <p class="para" id="second-paragraph">Segundo parágrafo!</p>
    </header>
  </body>
</html>
```

-   Recupere os seus parágrafos via código _JavaScript_, usando a função `getElementsByClassName`;

```html
<!DOCTYPE html>
    <script>
      const paragraphs = document.getElementsByClassName('para');
    </script>
```

-   Altere algum estilo do primeiro deles;

```html
    <script>
      // const paragraphs = document.getElementsByClassName('para');
      paragraphs[0].style.fontSize = '1.5rem';
      paragraphs[0].style.color = 'green';      
    </script>
```

-   Recupere o subtítulo e altere a cor dele usando a função `getElementsByTagName`.

```html
    <script>
      // const paragraphs = document.getElementsByClassName('para');
      // paragraphs[0].style.fontSize = '1.5rem';
      // paragraphs[0].style.color = 'green';
      const subtitle = document.getElementsByTagName('h4')[0];
      subtitle.style.color = 'red';      
    </script>
```

> ⚠️ **Atenção!** ⚠️

> Enquanto os `getElementsByClassName('ClassName')` e `getElementsByTagName('TagName')` retornam uma HTMLCollection, os `querySelectorAll('.ClassName')` e `querySelectorAll('TagName')` retornam uma NodeList.

Tanto NodeList quanto HTMLCollection são coleções de nós DOM. A diferença entre eles é que, enquanto um HTMLCollection conterá apenas elementos de nó HTML, o NodeList pode conter qualquer tipo de nó.

Um outro ponto é a forma da resposta, que pode ser diferente entre os seletores (_HTMLCollection_ e _NodeList_). A forma de buscar os dados armazenados nessas estruturas, em alguns casos, pode mudar, então tenha cuidado na hora de fazer funções que utilizem o resultado dos seletores, isso pode salvar das dores de cabeça sobre o porquê de uma função aparentemente correta não funcionar.

Vamos consolidar a manipulação dos elementos `HTML`, colocando a cor do Administrador de Tempo da Trybe como na imagem abaixo usando apenas o JavaScript!

![[Pasted image 20221024213411.png]]

Você vai precisar usar o que aprendeu sobre `getElementBy` e `querySelector` para colocar em prática.

Antes de iniciar, crie um arquivo _HTML_ na pasta `exercises/seletores` e copie o código abaixo:
```html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Administrador do Tempo</title>
  </head>
  <body id="container">
    <header id="header-container">
      <h1>Administrador do Tempo da Trybe</h1>
    </header>

    <section class="emergency-tasks">
      <div>
        <h3>Urgente e Importante</h3>
      </div>
      <div>
        <h3>Urgente e Não-Importante</h3>
      </div>
    </section>

    <section class="no-emergency-tasks">
      <div>
        <h3>Não-Urgente e Importante</h3>
      </div>
      <div>
        <h3>Não-Urgente e Não-Importante</h3>
      </div>
    </section>

    <footer id="footer-container">
      <div>&copy; Trybe</div>
    </footer>
    <script src="script.js"></script>
  </body>
</html>
```

Perceba que, agora, na tag `script`, temos o atributo `src`. Ele servirá para importarmos arquivos .js externos, e funciona de forma semelhante à importação de arquivos CSS. Assim, mantemos nosso código HTML mais limpo, e podemos editar com mais facilidade nosso JavaScript. Legal, não é?

Crie um arquivo _JavaScript_ com o nome de “script.js” na pasta `exercises/seletores` e coloque seus conhecimentos de `getElementBy` e `querySelector` em prática.

Crie também um arquivo _CSS_ e copie o código abaixo para adicionar estilo à página. Fique à vontade para soltar a criatividade e alterar o arquivo como desejar!

```css
* {
  margin: 0;
}

#container {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  text-align: center;
}

#header-container {
  color: white;
  padding: 20px;
}

.emergency-tasks {
  display: inline-block;
  height: 400px;
  margin: 56px 0;
  width: 400px;
}

.emergency-tasks div {
  height: 198px;
}
.emergency-tasks h3 {
  color: white;
  margin-top: 10px;
  padding: 10px;
}

.no-emergency-tasks {
  display: inline-block;
  height: 400px;
  width: 400px;
}

.no-emergency-tasks div {
  height: 198px;
}

.no-emergency-tasks h3 {
  color: white;
  margin-top: 10px;
  padding: 10px;
}

#footer-container {
  color: white;
  font-weight: 700;
  padding: 15px;
  text-align: center;
}
```

Perceba que todo o conteúdo da página está na cor branca, utilize o que aprendeu no conteúdo de hoje para que a página fique igual ao Administrador do Tempo da Trybe.

Vamos consolidar a manipulação dos elementos `HTML`, colocando a cor do Administrador de Tempo da Trybe como na imagem abaixo usando apenas o JavaScript!

![[Pasted image 20221024213713.png]]
> Administrador de tempo finalizado.

Você vai precisar usar o que aprendeu sobre `getElementBy` e `querySelector` para colocar em prática.

Antes de iniciar, crie um arquivo _HTML_ na pasta `exercises/seletores` e copie o código abaixo:

```html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Administrador do Tempo</title>
  </head>
  <body id="container">
    <header id="header-container">
      <h1>Administrador do Tempo da Trybe</h1>
    </header>

    <section class="emergency-tasks">
      <div>
        <h3>Urgente e Importante</h3>
      </div>
      <div>
        <h3>Urgente e Não-Importante</h3>
      </div>
    </section>

    <section class="no-emergency-tasks">
      <div>
        <h3>Não-Urgente e Importante</h3>
      </div>
      <div>
        <h3>Não-Urgente e Não-Importante</h3>
      </div>
    </section>

    <footer id="footer-container">
      <div>&copy; Trybe</div>
    </footer>
    <script src="script.js"></script>
  </body>
</html>
```

Perceba que, agora, na tag `script`, temos o atributo `src`. Ele servirá para importarmos arquivos .js externos, e funciona de forma semelhante à importação de arquivos CSS. Assim, mantemos nosso código HTML mais limpo, e podemos editar com mais facilidade nosso JavaScript. Legal, não é?

Crie um arquivo _JavaScript_ com o nome de “script.js” na pasta `exercises/seletores` e coloque seus conhecimentos de `getElementBy` e `querySelector` em prática.

Crie também um arquivo _CSS_ e copie o código abaixo para adicionar estilo à página. Fique à vontade para soltar a criatividade e alterar o arquivo como desejar!

```css
* {
  margin: 0;
}

#container {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  text-align: center;
}

#header-container {
  color: white;
  padding: 20px;
}

.emergency-tasks {
  display: inline-block;
  height: 400px;
  margin: 56px 0;
  width: 400px;
}

.emergency-tasks div {
  height: 198px;
}
.emergency-tasks h3 {
  color: white;
  margin-top: 10px;
  padding: 10px;
}

.no-emergency-tasks {
  display: inline-block;
  height: 400px;
  width: 400px;
}

.no-emergency-tasks div {
  height: 198px;
}

.no-emergency-tasks h3 {
  color: white;
  margin-top: 10px;
  padding: 10px;
}

#footer-container {
  color: white;
  font-weight: 700;
  padding: 15px;
  text-align: center;
}
```

Perceba que todo o conteúdo da página está na cor branca, utilize o que aprendeu no conteúdo de hoje para que a página fique igual ao Administrador do Tempo da Trybe.

#### **Solução**

```jsx
const header = document.getElementById('header-container');
header.style.backgroundColor = 'rgb(0, 176, 105)';

const emergencyTasks = document.getElementsByClassName('emergency-tasks')[0];
emergencyTasks.style.backgroundColor = 'rgb(255, 159, 132)';

const emergencyTasksHeaders = document.querySelectorAll('.emergency-tasks h3');
for (let index = 0; index < emergencyTasksHeaders.length; index += 1) {
  emergencyTasksHeaders[index].style.backgroundColor = 'rgb(165, 0, 243)';
}

const noEmergencyTasks = document.querySelector('.no-emergency-tasks');
noEmergencyTasks.style.backgroundColor = 'rgb(249, 219, 94)';

const noEmergencyTasksHeaders = document.querySelectorAll('.no-emergency-tasks h3');
for (let index = 0; index < noEmergencyTasksHeaders.length; index += 1) {
  noEmergencyTasksHeaders[index].style.backgroundColor = 'rgb(35, 37, 37)';
}

const footer = document.getElementById('footer-container');
footer.style.backgroundColor = 'rgb(0, 53, 51)';
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/d8690b8d-eaa4-4344-997c-cd1a2674076f/day/859613ad-86a2-42f2-ab66-2264d723686f/lesson/d32d94b9-cad9-47cb-8770-e55507a3cefb)
