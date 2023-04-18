[[API]]
[[Fetch API]]
[[Lifecycle]]
[[Promise]]
[[Setup e Teardown]]
[[Array]]
[[Objeto]]



## O que é JSON?

**JSON é a sigla para Javascript Object Notation — ou Notação de Objeto em** [[JavaScript]], em tradução livre. É um formato de arquivo, basicamente. Sistemas nas mais variadas linguagens usam esses arquivos para manipulação e transferência de quase todo tipo de dados. A maioria delas, atualmente, é capaz de converter os dados contidos em um JSON para objetos estruturados na própria linguagem.

De maneira geral, os códigos de um arquivo JSON são buscam uma melhor legibilidade por pessoas na hora de armazenar, programar a transferência e a modificação de objetos — e demais conjuntos de dados.

Você verá um pouco mais sobre esse tema adiante: trazemos uma variedade de contextos em que aplicamos um arquivo JSON ou como o utilizamos durante a comunicação entre a aplicação e o servidor, por exemplo.

**As utilidades para o formato JSON são inúmeras na programação** — o fato de ser um arquivo mais rápido e leve que um XML ou outras notações contribui muito para isso. Até mesmo, todas as configurações de um programa podem estar alocadas como um arquivo JSON!

Ele começou a ser utilizado por volta do ano de 2002, logo após o lançamento da quinta versão do ECMAScript, outra linguagem de programação, com relações muito próximas com o JavaScript.

## Qual a sintaxe do JSON? Conheça a estrutura do JSON

Os arquivos do tipo JSON utilizam a extensão .json para todos os sistemas em que são utilizados. Para deixar claro, saiba que o JSON não é uma linguagem, mas tem uma estrutura de notação específica.

Em outras palavras, **ele funciona como um map, em Java, com uma estrutura que identifica chaves e valores**. Essa estrutura facilita para que a linguagem possa organizar os dados que o arquivo carrega da maneira que for mais conveniente.

A sintaxe que utilizamos para as notações em JSON é bem simples ao ser comparada com linguagens como Java, JavaScript ou C#. Isso porque o número de componentes necessários são bem limitados:

-   usamos as **chaves** (“**{ }**”) para iniciar nossos objetos ou conjuntos de dados;
-   os **colchetes** (“**[ ]**“) servem para indicar um array — veremos mais sobre isso, ainda neste guia;
-   separamos a chave de seus valores correspondentes por **dois pontos (“:”);**
-   a **vírgula** (“**,**”) usamos para separar cada elemento contido em nosso objeto (ou array, por exemplo)**.**

A seguir, você poderá conferir alguns exemplos bastante comuns de um arquivo JSON.

### String JSON

É um arquivo de JSON que contém apenas dados do tipo String, ou seja, são processados como caracteres.
```js
{
	"estado": "Minas Gerais"
	"cidade": "Contagem"
	"bairro": "Cabral"
	"rua": "Alameda das Cotovias"
	"número": "260"
}
```

Você reparou que o exemplo acima é um endereço? O JSON opera exatamente nesse contexto: ele organiza os dados para que, independentemente do sistema que os acessar, seja capaz de lê-lo sem problemas. É importante notar que, por conta da notação, o número “14”, que pode ser lido no exemplo, será processado como string!

### Object JSON

Objetos JSON não são nada mais que objetos estruturados na notação JSON. Isso facilita o uso de um mesmo objeto nos mais diversos tipos de linguagens POO.

```js
{
	"endereço": {
		"estado": "Minas Gerais"
		"cidade": "Contagem"
		"bairro": "Cabral"
		"rua": "Alameda das Cotovias"
		"número": "260"
	}
}
```


No exemplo acima, podemos ver um endereço, como um objeto, o qual contém um país, um estado, uma cidade e uma rua. Perceba a diferença com o anterior: uma chave é aberta para a separação dos próprios elementos.

Não podemos deixar de apontar a necessidade da indentação, pois, como falamos, **o JSON também serve no auxílio para uma melhor legibilidade humana** durante o desenvolvimento de aplicações. Saiba que é possível encontrar diversos sistemas online para facilitar a formatação de um arquivo JSON.

### Array JSON

Também é possível criarmos e manipularmos arrays em JSON. **Arrays são objetos muito parecidos com listas**, amplamente utilizados nas principais linguagens de programação da atualidade. Em JSON, podemos criar um array da seguinte maneira:

```js
{
	"estados_sudeste_Brasil": ["Espirito Santo", "Minas Geraes", "Rio de Janeiro", "São Paulo"]
}
```

Podemos, até mesmo, criar um array de arrays:

```js
{
	"regiões_Brasil":[
		"Sudeste",[
			"Espirito Santo",
			"Minas Geraes",
			"Rio de Janeiro",
			"São Paulo"
		]
		"Sul",
		"Centro-Oeste",
		"Nordeste",
		"Norte"
	]
}
```


Ou objetos dentro de objetos:

```js
{
	"Nome": "João",
	"Área_de_Interesse": {
		"Front End"
		"Backend"
	}
	"Nome": "Maria",
	"Vagas_de_Interesse": {
		"FullStack"
	}
}
```

Os arquivos JSON podem ser configurados, ainda, para conter listas de objetos a serem utilizados nos mais variados sistemas. Para montá-los, basta seguir o exemplo abaixo:

```js
{ "Cidades visitadas": [
		{"Céara": "Fortaleza", "Região": "Nordeste"}
		{"Bahia": "Porto Seguro", "Região": "Nordeste"}
		{"São Paulo": "São José dos Campos", "Região": "Sudeste"}
	]
}
```

## Quais as vantagens do JSON?

A **simplicidade durante o acesso e o armazenamento de diferentes tipos de dados é uma das principais características dos arquivos JSON**. A facilidade em se trabalhar com esse formato reside muito na sua independência em relação a qual linguagem vai processá-lo. Isso faz dele uma das melhores escolhas ao precisarmos manipular dados em diferentes modelos de aplicações — sem a necessidade de reestruturar todo o código.

Quando falamos de Sistemas Web, as vantagens de usar JSONs durante o desenvolvimento de aplicações ficam ainda mais nítidas. **A interoperabilidade do formato entre tantos frameworks e linguagens diferentes**, sem o uso excessivo de conexões e tráfegos de dados repetitivos, faz do JSON uma das principais escolhas pelas pessoas desenvolvedoras mais experientes em atuação no mercado.

## Quais as desvantagens do JSON?

Existem algumas ocasiões nas quais as melhores pessoas especializadas não recomendam que você utilize o JSON em suas aplicações. **A principal delas, com certeza, é a segurança**.

Para esses casos, existem recursos como o [JWT — JSON Web Token](https://blog.betrybe.com/tecnologia/jwt-json-web-tokens/), um dos métodos mais seguros da atualidade para trabalharmos entre dois sistemas que usam arquivos JSON com maior segurança. Além dele, existem alguns frameworks com a mesma função.

Os **tipos de dados suportados pelo JSON** **são uma limitação que também vale a pena ser apontada**. Devido à necessidade de trabalhar apenas com textos e números, sem possibilidade de usar tabelas, imagens, entre outros tipos de dados, algumas pessoas desenvolvedoras poderão encontrar problemas com o JSON, precisando optar por outras soluções ou modelos de notação, como o XML, na maioria dos casos.



**JSON**  | **XML**
------- | --------
As ações de serialização do JavaScript é automatizada em JSON   | É necessário escrever o código JavaScript para realizar as ações de serialização de um arquivo XML
JSON pode suportar diversos tipos de dados: conjuntos de caracteres (Strings), números inteiros e decimais (Integers, Doubles, Floats) arrays e booleanos   | Qualquer dado contido em um XML deve ser do tipo String
O suporte para objetos é nativo do JSON   | O uso de estrutura de objetos no XML é feito por meio de convenções — e é muito comum vermos objetos em XML estruturados de maneira incorreta ou incompleta
O modelo de notação do JSON é suportado pela grande maioria dos browsers e sistemas web   | Podemos ter problemas ao processar um XML entre diferentes browsers
Os dados estão prontamente acessíveis por meio de um objeto JSON   | Os dados XML sempre precisam ser analisados pelo sistema a cada execução
Os objetos JSON tem uma tipagem específica   | Dados em XML são “typeless” — sem tipagem
Muitas ferramentas Ajax suportam o uso de JSON   | Nem todas as ferramentas Ajax são capazes de manipular um XML.
Um arquivo em JSON suporta somente dados como números e caracteres   | Arquivos XML são polivalentes neste sentido, podem agregar números, textos, imagens, gráficos e tabelas, por exemplo.
Um JSON não possibilita a exibição dos dados contidos em seus arquivos   | Com XML é possível a exibição de dados — já que é uma linguagem de marcação

Além disso, é importante saber que o XML também possibilita opções avançadas de transferência do modelo da estrutura de dados atual para aquela que será utilizada pelo sistema, função que o JSON não tem.

Mesmo assim, existem diversos processos que minimizam essa falta — como na linguagem Python, em que o JSON é processado e transformado em um dicionário para ser utilizado em sistemas escritos nessa linguagem.

## JSON.stringify(): converta um objeto em uma string

Explicando de maneira bem resumida, **JSON.stringify()** é um método da linguagem JavaScript. Ele, basicamente, **converte valores contidos em aplicações JavaScript para uma String JSON.**

Tais valores podem ser manipulados — é possível usarmos funções como “replace” para substituir determinado dado —, entre outros métodos para realizar a transformação de valores em uma string. Neste link, você encontrará um guia detalhado sobre esse método, com exemplos práticos de uso e explicados em uma linguagem de fácil acesso. Bons estudos!

## **JSON.parse(): analise dados e converta JSON em objetos JavaScript**

Outro método nativo do JavaScript, o JSON.parse(), tem seu uso concentrado na análise de **dados de uma Aplicação Web**, resumidamente. Usando esse método, os dados do arquivo JSON são analisados, transformando-o em um objeto JavaScript.

A função desse método operam somente em dados do tipo string — ou coleção de caracteres, como também pode ser chamado. 


## **Como usar o JSON, na prática, com JavaScript?**

Como o observado, podemos acessar os valores e chaves de um JSON e utilizá-los em nossas aplicações. A seguir, você poderá conferir uma configuração bem básica de um HTML — use-a em sua máquina para ajudar a colocar em prática o que aprendemos, e entenda melhor sobre os processos que envolvem o JSON:

```html
<!DOCTYPE html>
<html>
<body>

<h2>Criar objetos por meio de Strings</h2>
<p id="parag"></p>
</body> 
</html>
```

Agora, precisamos dos scripts. Usaremos o JavaScript para acessar os dados, analisá-los e, posteriormente, usá-los para imprimir o que queremos em nossa página. Usaremos o seguinte código:

![[json1.webp]]
Vale pontuar que o JSON, caso estivesse em um arquivo à parte, seria escrito dessa maneira:

![[json.webp]]
O resultado que veremos gerado do código que usamos de exemplo será assim:


## Criar objetos por meio de Strings##

As aplicações desenvolvidas no cotidiano, certamente, são mais complexas e utilizam as estruturas JSON hospedadas nos servidores em arquivos para acesso mais simples e rápido. Por exemplo, você pode tentar **salvar um JSON igual ao mostrado no exemplo abaixo e fazer o upload dele diretamente no GitHub** ou qualquer outro servidor que possibilite essa tarefa:

![[json5.webp]]
Aqui, representamos um arquivo JSON contendo os dados de três pessoas selecionadas como os melhores colaboradores do mês de nossa empresa fictícia. Mas como usamos essas informações em um sistema?

Saiba que, ao fazer o upload, você acessa o arquivo a partir de um link que, quando usado a partir do Github, se parece com isso:

https://seu-usuário.github.io/suapasta/nome_do_arquivo.json — AQUI ficaria melhor usar o próprio arquivo hospedado. Como não sei os procedimentos internos do cliente, vou deixar essa nota aqui para ser lida — chamem nos comentários da tarefa quando decidirem a melhor solução e retrabalhamos este H2 caso seja necessário. Do contrário, é só apagar este trecho.

Com esse método, você simplificará a maneira com que seu sistema manipula esses dados. Para isso, você poderá recorrer a funções e métodos da própria linguagem, realizando requisições de acesso desse arquivo.

Construtores do JavaScript, como request() e fetch(), atuam muito bem nessa parte. Confira o exemplo, em que trazemos uma função — requestURL — para preencher a partir desses dados o cabeçalho de uma página HTML:
![[json6.webp]]
Com esses dados carregados em nosso sistema, podemos preencher tudo em uma página HTML, como parágrafos, títulos, subtítulos e tudo o mais — até mesmo, é possível alterarmos detalhes do CSS dessas páginas.

Um exemplo de como ficaria um código utilizando dos dados desse mesmo JSON que apresentamos, para preenchimento de um H1 e um parágrafo da página, seria assim:

![[json7.webp]]
