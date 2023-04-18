[[JavaScript]]
[[HOF's]]
[[For...In]]
[[React]]

Objetos em JavaScript, assim como em muitas outras linguagens de programação, podem ser comparados com objetos na vida real. O conceito de objetos em JavaScript pode ser entendido com objetos tangíveis da vida real.

Em JavaScript, um objeto é uma entidade independente, com propriedades e tipos. Compare-o com uma xícara, por exemplo. Uma xícara é um objeto, com propriedades. *Uma xícara tem uma cor, uma forma, peso, um material de composição, etc. **Da mesma forma, objetos em JavaScript podem ter propriedades, que definem suas características.**

Um objeto em JavaScript tem propriedades associadas a ele. Uma propriedade de um objeto pode ser explicada como uma variável que é ligada ao objeto. Propriedades de objetos são basicamente as mesmas que variáveis normais em JavaScript, exceto pelo fato de estarem ligadas a objetos. As propriedades de um objeto definem as características do objeto. Você acessa as propriedades de um objeto com uma simples notação de ponto:

```
nomeDoObjeto.nomeDaPropriedade
```

Um objeto em JavaScript tem propriedades associadas a ele. Uma propriedade de um objeto pode ser explicada como uma variável que é ligada ao objeto. Propriedades de objetos são basicamente as mesmas que variáveis normais em JavaScript, exceto pelo fato de estarem ligadas a objetos. As propriedades de um objeto definem as características do objeto. Você acessa as propriedades de um objeto com uma simples notação de ponto:

```JavaScript
var meuCarro = new Object();
meuCarro.fabricacao = "Ford";
meuCarro.modelo = "Mustang";
meuCarro.ano = 1969;
```

Propriedades de objetos em JavaScript podem também ser acessadas ou alteradas usando-se notação de colchetes. Objetos são às vezes chamados de _arrays associativos_, uma vez que cada propriedade é associada com um valor de string que pode ser usado para acessá-la. Então, por exemplo, você poderia acessar as propriedades do objeto `meuCarro` como se segue:

```JavaScript
meuCarro["fabricacao"] = "Ford";
meuCarro["modelo"] = "Mustang";
meuCarro["ano"] = 1969;
```

## **Criando novos objetos**

JavaScript possui um número de objetos pré-definidos. Além disso, você pode criar seus próprios objetos. Você pode criar um objeto usando um objeto inicializador. Alternativamente, você pode primeiro criar uma função construtora e depois instanciar um objeto usando aquela função e o operador `new`.

Além de criar objetos usando uma função construtora, você pode criar objetos usando um inicializador de objeto. O uso de inicializadores de objeto é às vezes conhecido como criar objetos com notação literal. A sintaxe para um objeto usando-se um inicializador de objeto é:

```JavaScript
var obj = { propriedade_1:   valor_1,   // propriedade_# pode ser um identificador...
            2:            valor_2,   // ou um numero...
            // ...,
            "propriedade n": valor_n }; // ou uma string
```

onde `obj` é o nome do novo objeto, cada `propriedade_i` é um identificador (um nome, um número, ou uma string literal), e cada `valor_i` é uma expressão cujo valor é atribuído à `propriedade_i`. O `obj` e a atribuição são opcionais; se você não precisa fazer referência a esse objeto em nenhum outro local, você não precisa atribuí-lo a uma variável. (Note que você pode precisar colocar o objeto literal entre parentêses se o objeto aparece onde um comando é esperado, de modo a não confundir o literal com uma declaração de bloco.)


###### Fontes:
https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Working_with_Objects


