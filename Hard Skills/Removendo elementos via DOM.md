[[DOM]]
[[Criando elementos em DOM]]
[[Buscando elementos em DOM]]
[[Removendo elementos via DOM]]
[[JavaScript]]


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

-   Remova todos os elementos filhos de `paiDoPai` exceto `pai`, `elementoOndeVoceEsta` e `primeiroFilhoDoFilho`.

**Primeiro passo:** Recupere o elemento com o id `pai`

```html
<!DOCTYPE html>
<html lang="en">
  <!--  -->
  <script>
    const pai = document.getElementById('pai');
  </script>
  <!--  -->
</html>
```

**Segundo passo:** Utilize o `.childNodes` para retornar uma coleção viva de nós filhos do elemento `pai`.

```html
<!DOCTYPE html>
<html lang="en">
  <!--  -->
  <script>
    const pai = document.getElementById('pai');
    const todosOsFilhos = pai.childNodes;
  </script>
  <!--  -->
</html>
```

**Terceiro passo:** Utilize uma estrutura de repetição para iterar sob o `array` `todosOsFilhos`.

-   Utilize o `.length` para verificar o tamanho que `todosOsFilhos` possui;
-   Como a primeira posição de um `array` é a posição 0, subtraia **1** do tamanho de `todosOsFilhos`;
-   Decremente o `index` a cada iteração.


```html
<!DOCTYPE html>
<html lang="en">
  <!--  -->
  <script>
    const pai = document.getElementById('pai');
    const todosOsFilhos = pai.childNodes;
    for (let index = todosOsFilhos.length - 1; index >= 0; index -= 1) {
    }
  </script>
  <!--  -->
</html>
```

**Quarto passo:** Armazene o filho atual em uma variável.

```html
<!DOCTYPE html>
<html lang="en">
  <!--  -->
  <script>
    const pai = document.getElementById('pai');
    const todosOsFilhos = pai.childNodes;
    for (let index = todosOsFilhos.length - 1; index >= 0; index -= 1) {
      const filhoAtual = todosOsFilhos[index];
    }
  </script>
  <!--  -->
</html>
```

**Quinto passo:** Caso o `id` do `filhoAtual` seja diferente de `elementoOndeVoceEsta`, remova o `filhoAtual`.

```html
<!DOCTYPE html>
<html lang="en">
  <!--  -->
  <script>
    const pai = document.getElementById('pai');
    const todosOsFilhos = pai.childNodes;
    for (let index = todosOsFilhos.length - 1; index >= 0; index -= 1) {
      const filhoAtual = todosOsFilhos[index];
      if (filhoAtual.id !== 'elementoOndeVoceEsta') { // Verifica se o id do filho atual é diferente de 'elementoOndeVoceEsta'
        filhoAtual.remove(); // Remove o filhoAtual
      }
    }
  </script>
  <!--  -->
</html>
```

**Sexto passo:** Recupere o elemento com o `id` `segundoEUltimoFilhoDoFilho` e o remova.

```html
<!DOCTYPE html>
<html lang="en">
  <!--  -->
  <script>
    const pai = document.getElementById('pai');
    const todosOsFilhos = pai.childNodes;
    for (let index = todosOsFilhos.length - 1; index >= 0; index -= 1) {
      const filhoAtual = todosOsFilhos[index];
      if (filhoAtual.id !== 'elementoOndeVoceEsta') {
        filhoAtual.remove();
      }
    }
    const segundoEUltimoFilhoDoFilho = document.getElementById('segundoEUltimoFilhoDoFilho'); // Recupera o elemento com o id segundoEUltimoFilhoDoFilho
    segundoEUltimoFilhoDoFilho.remove(); // Remove o segundo filho do filho
  </script>
  <!--  -->
</html>
```

###### Fonte: [Curso](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/d8690b8d-eaa4-4344-997c-cd1a2674076f/day/61f1b2b7-a34e-4ad9-8c2e-2c2db96e3d9c/lesson/a9106a62-b6fc-48a2-a31c-7935eb40e752)
