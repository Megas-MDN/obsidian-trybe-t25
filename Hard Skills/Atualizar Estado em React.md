[[React]]
[[Estado]]
[[Arrow Functions]]
[[Desestruturação Dinâmica]]
[[DOM]]
[[Operador Condicional Ternário]]


Para atualizar/salvar no [[DOM]] um estado você precisa criar uma função que comece com a palavra ***`handle`***.

## EX:

Suponhamos que precisamos atualizar o estado de todos os inputs no evento `onChange` dentro de um formulário, para isso vamos criar a função `handleInputChange`. Essa função é criada antes do `render` e é chamada dentro do componente `onChange` juntamente com o prefixo `this`, conforme abaixo:

```React
onChange={ this.handleInputChange }
```

Se você necessitar que ela execute basta incluir () após o nome da função.

Essa função precisa receber como parametro um `event`. 
Após inserir este parametro o próximo passo e começar a desenvolver a função. Primeiro deveremos desconstruir as variáveis para recebermos apenas o que queremos, e logo após "setar" o estado

```React
handleInputChange = (event) => {
const { value} = event.target;
this.setState({
	name: value,
	cvc: value,
})
};
```

Lembrando que o `.taget` vai nos retornar o value daquilo que foi digitado.
Neste caso está funcionando porém tem um problema, pois quando o usuário digitar, o `setState` irá armazenar a mesma informação de todos os campos, no exemplo acima seria de name e cvc.

Para resolver este problema você deve garantir que o seu estado tenha o mesmo nome dos seus imputs e fazer uma [[Desestruturação Dinâmica]].

```React
handleInputChange = (event) => {
const { name, value} = event.target;
this.setState({
	[name]: value,
})
};
```

Desta forma o elemento `[name]` vai ser igual a `key` que for clicada e o `value` será o valor digitado. Desta forma se os campos e os imputs tiverem o mesmo nome, vamos conseguir pegar a informação contida em cada um deles e trabalhar da melhor maneira que precisarmos. 


![[Captura de tela de 2022-09-27 20-49-51.png]]![[Captura de tela de 2022-09-27 20-50-01.png]]

Se o input e o campo tiver nomes diferentes será criado um campo dinâmico e o imput não terá o valor atualizado.

Como os valores neste momento estão sendo salvos no [[DOM]], uma boa prática é atribuir este valor na propriedade `value` no seu formulário. Este processo tem o nome de componente controlado, pois desta forma o [[--React]] está controlando este campo e ele ficará responsável por atualizar a informação deste campo.

```JavaScript React
handleInputChange = (event) => {
const { name, type, checked } = event.target;
const value = type === 'checkbox' ? checked : event.target.value;
this.setState({
	[name]: value,
})
};
```

Acima seria a forma de fazer quando tem a opção `checkbox` utilizando o [[Operador Condicional Ternário]], desta forma o modelo acima pode ser usado como padrão para este tipo de situação.

