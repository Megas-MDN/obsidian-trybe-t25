[[HTML]]
[[JavaScript]]

**Cookies** são dados salvos em pequenos arquivos de texto no computador da pessoa que utiliza a _Internet_.

Quando o servidor envia a página _Web_ para o _browser_, a conexão é desligada e o servidor não tem mais acesso às informações da requisição - como os itens que a pessoa usuária adicionou a um carrinho de compras ou o e-mail que lhe dará acesso a sua conta. **Cookies** foram inventados para salvar dados das pessoas usuárias no próprio _browser_, pois, dessa forma, uma página conseguirá acessá-los para executar uma lógica com os parâmetros personalizados por pessoa.

Cookies são salvos no formato `chave-valor`. Quando o navegador faz a requisição ao servidor para acessar uma página Web, os _cookies_ dessa página são adicionados à requisição. Dessa forma, o servidor tem acesso aos dados da pessoa usuária. Nos exemplos a seguir, você irá aprender a criar e manipular _cookies_. Para testá-los, é importante que o seu navegador tenha o suporte a _cookie_ habilitado. Para visualizar os cookies de uma aplicação, abra a janela para inspecionar a página. No menu superior, clique em Application e, na barra lateral esquerda, na sessão Storage, clique em Cookies.

O Javascript permite que a gente crie, leia e delete cookie através da propriedade `document.cookie`.

Para criar um cookie, você só precisa atribuir à propriedade `document.cookie` uma `string` contendo o nome e o valor do que se pretende armazenar:

```js
document.cookie = 'email=isabella@email.com';
```

Por definição, o `cookie` é deletado quando fechamos o navegador. Para que isso não aconteça, você pode adicionar uma data para expiração, como no exemplo abaixo:

```js
document.cookie = 'email=isabella@email.com; expires=Thu, 17 Dec 2020 12:00:00 UTC';
```

Você pode adicionar também o parâmetro `path`, que dirá ao navegador a qual caminho o cookie que você criou pertence. Por padrão, o cookie pertence à página atual.


```js
document.cookie = 'email=isabella@email.com; expires=Thu, 17 Dec 2020 12:00:00 UTC; path=/';
```

O Javascript permite que você atribua `document.cookie` a uma variável. Assim, você conseguirá ler as informações que estão armazenadas. No exemplo abaixo, ao imprimirmos no `console` o valor de myCookie, o que será retornado é uma `string` contendo o nome e o valor do cookie. Quando temos mais de um par chave-valor, a variável armazenará em uma única `string` os pares separados por ponto-vírgula.

```js
const myCookie = document.cookie;
console.log(myCookie) // email=isabella@email.com
```

E você pode também alterar o valor do cookie da mesma forma que o criamos. Basta atribuir a `document.cookie` a nova informação que você quer armazenar.

```js
document.cookie = 'email=cleyton@email.com; expires=Thu, 17 Dec 2020 12:00:00 UTC';
```

Para deletar o cookie, você não precisa especificar o valor que pretende deletar. Você pode deletá-lo passando uma data que já expirou:

```js
document.cookie = 'email=; expires=Tue, 01 Dec 2020 12:00:00 UTC;'
```

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/fc998c60-386e-46bc-83ca-4269beb17e17/section/d8690b8d-eaa4-4344-997c-cd1a2674076f/day/601a2d75-6ae1-42e6-8e1a-afdfb0f0c4cc/lesson/d26b68d3-5595-4bba-96e6-381a1168eac1)
