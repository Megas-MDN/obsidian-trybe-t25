[[Fetch API]]
[[Promise]]
[[Async e Await]]



## Encadeamento com then() e catch()

O encadeamento é essencial para entender como o código funcionará, uma vez que isso determina uma sequência de direcionamentos dentro do código. Nesse sentido, o encadeamento de Promises com then e catch vai direcionar os nossos resultados. Para entendermos de forma prática, vamos visualizar o seguinte exemplo:

```jsx
const teste = new Promise ((resolve, reject) => {
	setTimeout(() = > resolve ('Promise resolvida'), 3000)
})
// Aqui os callbacks estão ligados a teste
teste.then((res) => {}, (rej) => {})
// Nessa parte, observamos o mesmo resultado
new Promise ((resolve, reject) => {})
	.then((res) => {}, (rej) = {}
```

Podemos combinar bem o resolve com o then, que retornará sucesso, ou o reject com o catch, para falha/erro.

Além dessa forma de encadeamento, temos ainda o Async que é uma aplicação presente no ECMAScript. Essa função pode aceitar N funções em si, uma vez que será repassado dentro da pipeline do código. Nessa perspectiva, esse é um ponto importante, pois, na estruturação do seu código, nem todas as funções serão assíncronas, ou seja, a execução será realizada na ordem correta de funcionamento.

###### Fonte: [Blog trybe](https://blog.betrybe.com/javascript/promises-javascript/)
