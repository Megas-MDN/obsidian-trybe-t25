[[DOM]]
[[JavaScript]]
[[Buscando elementos em DOM]]


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

-   Crie um irmão para `elementoOndeVoceEsta`.
-   Crie um filho para `elementoOndeVoceEsta`.
-   Crie um filho para `primeiroFilhoDoFilho`.
-   A partir desse filho criado, acesse `terceiroFilho`.

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
    // Crie um irmão para `elementoOndeVoceEsta`.
    const pai = document.getElementById('pai'); // Recupere o elemento com o id pai
    const irmaoElementoOndeVoceEsta = document.createElement('section'); // Crie um novo elemento
    irmaoElementoOndeVoceEsta.id = 'irmaoElementoOndeVoceEsta';
    pai.appendChild(irmaoElementoOndeVoceEsta); // Adicione o elemento criado como filho do elemento com o id `pai`

    // Crie um filho para `elementoOndeVoceEsta`.
    const elementoOndeVoceEsta = document.getElementById('elementoOndeVoceEsta'); // Recupere o elemento com o id elementoOndeVoceEsta
    const filhoElementoOndeVoceEsta = document.createElement('section'); // Crie um novo elemento 
    filhoElementoOndeVoceEsta.id = 'filhoElementoOndeVoceEsta';
    elementoOndeVoceEsta.appendChild(filhoElementoOndeVoceEsta); // Adicione o elemento criado como filho do elemento `elementoOndeVoceEsta`

    // Crie um filho para `primeiroFilhoDoFilho`.
    const primeiroFilhoDoFilho = document.getElementById('primeiroFilhoDoFilho'); // Recupere o elemento com o id `primeiroFilhoDoFilho`
    const filhoPrimeiroFilhoDoFilho = document.createElement('section'); // Crie um novo elemento 
    filhoPrimeiroFilhoDoFilho.id = 'filhoPrimeiroFilhoDoFilho';
    primeiroFilhoDoFilho.appendChild(filhoPrimeiroFilhoDoFilho); // Adicione o elemento criado como filho do elemento `primeiroFilhoDoFilho`

    // A partir desse filho criado, acesse `terceiroFilho`.
    const terceiroFilho = filhoPrimeiroFilhoDoFilho
      .parentElement // primeiroFilhoDoFilho
      .parentElement // elementoOndeVoceEsta
      .nextElementSibling; // terceiroFilho
    console.log(terceiroFilho);
  </script>
<!-- </body>
</html> -->
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/d8690b8d-eaa4-4344-997c-cd1a2674076f/day/61f1b2b7-a34e-4ad9-8c2e-2c2db96e3d9c/lesson/84a4bafd-6457-4f08-b0f2-2475c5621d8f)
