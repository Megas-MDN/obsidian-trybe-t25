[[For...Of]]
[[For...In]]
[[forEach]]
[[JavaScript]]
[[HOF's]]
[[Funções]]



A instrução `for` cria um loop que consiste em três expressões opcionais, dentro de parênteses e separadas por ponto e vírgula, seguidas por uma declaração ou uma sequência de declarações executadas em sequência.

________________________
## Sintaxe

>`for` ([inicialização]; [condição]; [expressão final])
   declaração

### **inicialização**

Uma expressão (incluindo expressões de atribuição) ou declarações variáveis. Geralmente usada para iniciar o contador de variáveis. Esta expressão pode, opcionalmente, declarar novas variáveis com a palavra chave `var` ou `let`. Essas variáveis não são locais no loop, isto é, elas estão no mesmo escopo que o loop `for` está. 

### **condição**

Uma expressão para ser avaliada antes de cada iteração do loop. Se esta expressão for avaliada para true, declaração será executado. Este teste da condição é opcional. Se omitido, a condição sempre será avaliada como verdadeira. Se a expressão for avaliada como falsa, a execução irá para a primeira expressão após a construção loop `for`.

### **expressão final**

Uma expressão que será validada no final de cada iteração de loop. Isso ocorre antes da próxima avaliação da condição. Geralmente usado para atualizar ou incrementar a variável do contador.

### **declaração**

Uma declaração que é executada enquanto a condição for verdadeira. Para executar múltiplas condições dentro do loop, use uma instrução de bloco `({...})` para agrupar essas condições. Para não executar declarações dentro do loop, use uma instrução vazia `(;)`.


__________________
## EX:
```JSX
let listaDeNomes = ["Gabriel", "Lorenzo", "Paula"];
for (let index =0; index < listaDeNomes.length; index += 1){
let mensagem = "Boas vindas, " + listaDeNomes[index] + "!")
console.log(mensagem)
}
```

