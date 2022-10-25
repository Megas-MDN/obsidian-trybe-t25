[[DOM]]
[[JavaScript]]

A propriedade `parentNode` acessa o elemento pai do elemento sobre o qual a propriedade é chamada. Mas ela não é a única forma de, a partir de um elemento, navegar para outros.

Há, ao todo, as seguintes propriedades:

-   `parentNode`: retorna o nó pai.
-   `parentElement`: retorna o elemento pai.
-   `childNodes`: retorna um NodeList com todos os nós filhos.
-   `children`: retorna um HTMLCollection com todos os elementos filhos.
-   `firstChild`: retorna o primeiro nó filho.
-   `firstElementChild`: retorna o primeiro elemento filho.
-   `lastChild`: retorna o último nó filho.
-   `lastElementChild`: retorna o último elemento filho.
-   `nextSibling`: retorna o próximo nó.
-   `nextElementSibling`: retorna o próximo elemento.
-   `previousSibling`: retorna o nó anterior.
-   `previousElementSibling`: retorna o elemento anterior.
    

É importante dizer que, à primeira vista, as propriedades `nextSibling` e `nextElementSibling` parecem fazer a mesma coisa, mas uma pega o próximo nó do _DOM_, enquanto a outra pega o próximo elemento, e nem sempre o próximo nó é um elemento.

Para você entender melhor, observe com atenção a estrutura `HTML` que temos abaixo:

```html
<!-- arquivo index.html -->

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>  
  <main>
    <div id="start"></div>
    nó
    <p>elemento</p>
  </main>
  <script src="script.js"></script>
</body>
</html>
```

Como você pode ver, o arquivo possui um elemento `main` contendo dois elementos filhos: uma `<div>` e um `<p>`. Então você vai aplicar as propriedades `nextSibling` e `nextElementSibling` para ver a diferença entre elas:

```js
// arquivo script.js

console.log(document.getElementById('start').nextSibling) // nó

console.log(document.getElementById('start').nextElementSibling) // <p>elemento</p>
```

**Observação:** para testar o código acima, crie um arquivo `index.html` e outro `script.js`, copie os códigos e salve os documentos. Para visualizar as saídas no console, dê start no Live Server, inspecione a página e abra o console.

Primeiro, foi selecionado o elemento `div` utilizando o seu `id`, ‘start’. Na sequência, aplicadas as propriedades `nextSibling` e `nextElementSibling`. Você pode ver que `nextSibling` retornará o texto “nó” que representa o próximo nó do _DOM_ a partir da `div`, enquanto `nextElementSibling` retornará o próximo elemento propriamente, ou seja, o elemento `<p>`.

Adicione o código abaixo a uma página _HTML_ e adicione uma tag `script`. Você deverá fazer tudo usando somente _JavaScript_.

```html
<main id="paiDoPai">
  <section id="pai">
    <section id="primeiroFilho"></section>
    <section id="elementoOndeVoceEsta">
      <section id="primeiroFilhoDoFilho"></section>
      <section id="segundoEUltimoFilhoDoFilho"></section>
    </section>
    Atenção!
    <section id="terceiroFilho"></section>
    <section id="quartoEUltimoFilho"></section>
  </section>
</main>
```

-   Acesse o elemento `elementoOndeVoceEsta`.
-   Acesse `pai` a partir de `elementoOndeVoceEsta` e adicione uma `color` a ele.
-   Acesse o `primeiroFilhoDoFilho` e adicione um texto a ele. Você se lembra dos vídeos da aula anterior, como fazer isso?
-   Acesse o `primeiroFilho` a partir de `pai`.
-   Agora acesse o `primeiroFilho` a partir de `elementoOndeVoceEsta`.
-   Agora acesse o texto `Atenção!` a partir de `elementoOndeVoceEsta`.
-   Agora acesse o `terceiroFilho` a partir de `elementoOndeVoceEsta`.
-   Agora acesse o `terceiroFilho` a partir de `pai`.

Adicione o código abaixo a uma página _HTML_ e adicione uma tag `script`. Você deverá fazer tudo usando somente _JavaScript_.

```html
<main id="paiDoPai">
  <section id="pai">
    <section id="primeiroFilho"></section>
    <section id="elementoOndeVoceEsta">
      <section id="primeiroFilhoDoFilho"></section>
      <section id="segundoEUltimoFilhoDoFilho"></section>
    </section>
    Atenção!
    <section id="terceiroFilho"></section>
    <section id="quartoEUltimoFilho"></section>
  </section>
</main>
```

-   Acesse o elemento `elementoOndeVoceEsta`.
-   Acesse `pai` a partir de `elementoOndeVoceEsta` e adicione uma `color` a ele.
-   Acesse o `primeiroFilhoDoFilho` e adicione um texto a ele. Você se lembra dos vídeos da aula anterior, como fazer isso?
-   Acesse o `primeiroFilho` a partir de `pai`.
-   Agora acesse o `primeiroFilho` a partir de `elementoOndeVoceEsta`.
-   Agora acesse o texto `Atenção!` a partir de `elementoOndeVoceEsta`.
-   Agora acesse o `terceiroFilho` a partir de `elementoOndeVoceEsta`.
-   Agora acesse o `terceiroFilho` a partir de `pai`.

---

Essa solução está dividida pelas etapas do enunciado e indicadas dentro do código html abaixo:
```html
<!-- <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <main id="paiDoPai">
    <section id="pai">
      <section id="primeiroFilho"></section>
      <section id="elementoOndeVoceEsta">
        <section id="primeiroFilhoDoFilho"></section>
        <section id="segundoEUltimoFilhoDoFilho"></section>
      </section>
      Atenção!
      <section id="terceiroFilho"></section>
      <section id="quartoEUltimoFilho"></section>
    </section>
  </main> -->

  <script>
    // Acesse o elemento elementoOndeVoceEsta.
    const elementoOndeVoceEsta = document.getElementById('elementoOndeVoceEsta');

    // Acesse pai a partir de elementoOndeVoceEsta e adicione uma color a ele.
    const pai = elementoOndeVoceEsta.parentElement;
    pai.style.color = 'red';

    // Acesse o primeiroFilhoDoFilho e adicione um texto a ele.
    // Você se lembra dos vídeos da aula anterior, como fazer isso?
    const primeiroFilhoDoFilho = elementoOndeVoceEsta.firstElementChild;
    primeiroFilhoDoFilho.innerText = 'primeiroFilhoDoFilho';

    // Acesse o primeiroFilho a partir de pai.
    const primeiroFilho = pai.firstElementChild;

    // Agora acesse o primeiroFilho a partir de elementoOndeVoceEsta.
    const primeiroFilho2 = elementoOndeVoceEsta.previousElementSibling;
    
    // Agora acesse o texto Atenção! a partir de elementoOndeVoceEsta.
    const textElement = elementoOndeVoceEsta.nextSibling;

    // Agora acesse o terceiroFilho a partir de elementoOndeVoceEsta.
    const terceiroFilho = elementoOndeVoceEsta.nextElementSibling;

    // Agora acesse o terceiroFilho a partir de pai.
    const terceiroFilho2 = pai.lastElementChild.previousElementSibling;
  </script>
<!-- </body>
</html> -->
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/d8690b8d-eaa4-4344-997c-cd1a2674076f/day/61f1b2b7-a34e-4ad9-8c2e-2c2db96e3d9c/lesson/d284bcba-89f4-47de-acb0-10f670ebe89c)
