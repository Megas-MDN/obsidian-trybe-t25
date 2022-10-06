[[JavaScript]]
[[React]]
[[IF...Else]]
[[--DOM]]
[[ReactDOM]]


O operador condicional (ternário) é o único operador `JavaScript` que possui três operandos. Este operador é frequentemente usado como um atalho para a instrução `if`.

## Sintaxe

> condition `?` expr1 `:` expr2

### **condition**
Uma expressão que é avaliada como true ou false.

### **expr1**, **expr2**
Expressões com valores de qualquer tipo.

**Se condition é true, o operador retornará o valor de expr1; se não, ele retorna o valor de exp2.***

## EX:
```JavaScript
let firstCheck = false,
    secondCheck = false,
let access = firstCheck ? "Access denied" : secondCheck ? "Access denied" : "Access granted";

console.log( access ); // logs "Access granted"
```
