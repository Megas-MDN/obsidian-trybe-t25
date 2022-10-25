[[JavaScript]]
[[DOM]]
[[React]]
[[IF...Else]]


Similar a o `if/else`, dentro do `switch`, o que deve ser analisado, e as condicionais vão dentro do `case`.

Se a condição for correspondida, o programa executa as instruções associadas. Se múltiplos casos corresponderem o valor, o primeiro caso que corresponder é selecionado, mesmo se os casos não forem iguais entre si.

## Sintaxe
>
`Switch` (variável) {
`case` conteúdoDaVariável/situação/caso' : 
`console.log`('mensagem a ser impressa')
`break`;
`case` 'Variável2' :
`console.log`('mensagem para variável 2')
`break`;
`default:`
`console.log`('mensagem para retorno padrão quando não se encaixar e nenhum dos cases')
}

O programa primeiro procura por um caso o qual a expressão avalie como tendo o mesmo valor que o input da expressão transferindo assim o controle para a cláusula encontrada e em seguida executando as instruções associadas. Caso nenhum caso seja correspondido, então o programa procura pela cláusula opcional `default`, que, se encontrado, tem o controle transferido a ele, executando suas instruções associadas. Se não houver uma cláusula `default`, o programa continua a execução da instrução seguindo para o final do `switch`. Por convenção, a cláusula default é a última, mas não é algo obrigatório.

## EX:

```JavaScript
mes = 'maio';
let estacaoDoAno = '?';
switch (mes) {
    case 'janeiro':
    case 'fevereiro':
    case 'março':
        estacaoDoAno = 'Verão';
        break;
    case 'abril':
    case 'maio':
    case 'junho':
        estacaoDoAno = 'Outono';
        break;
    case 'julho':
    case 'agosto':
    case 'setembro':
        estacaoDoAno = 'Inverno';
        break;
    case 'outubro':
    case 'novembro':
    case 'dezembro':
        estacaoDoAno = 'Primavera';
}
console.log(estacaoDoAno); // 'Outono'
```

