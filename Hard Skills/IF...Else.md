[[IF...Else]]
[[JavaScript]]
[[DOM]]
[[Operador Condicional Ternário]]


A condicional `if` é uma estrutura condicional que executa a afirmação, dentro do bloco, se determinada condição for verdadeira. Se for falsa, executa as afirmações dentro de `else`.

## Sintaxe

>`if` (condição) {
>	afirmação1
>	} `else`  {
>	afirmação2]
>	}

### **condição**

Uma expressão que pode ser avaliada como verdadeira (true) ou falsa (false), veja lógica de programação para entender melhor.

### **condição1**

Condicional que será executada caso a condição em `if` seja verdadeira (true). Pode ser qualquer instrução, incluindo mais condicionais `if` aninhadas à instrução. Para executar multiplas instruções, faça um agrupamento com uma instrução em bloco ({ ... }). Para não executar nenhuma instrução, utilize uma instrução vazia (empty).

### **condição2**

Condicional que será executada caso a condição em `if` seja avaliada como falsa (false) e a condição `else` exista. Pode ser qualquer instrução, incluindo instruões em bloco e mais condicionais `if` aninhadas.

## EX:
```JavaScript
if (x > 5) {

} else if (x > 50) {

} else {

}
```
