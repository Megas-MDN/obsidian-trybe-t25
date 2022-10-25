#markdown #GitHub

# Titulo -> "#"
## Titulo 2 -> "##"
### Titulo 3 -> "###"
#### Titulo 4 -> "####"
##### Titulo 5 -> "#####"
###### Titulo 6 -> "######"


---------------------------------------------------------------------------
# Negrito, Itálico e Tachado
## Negrito:
**Texto** ou __Texto__ -> Texto entre 2 asterisco ou 2 anderescore

## Itálico:
*Texto* ou _Texto_  -> Texto entre 1 asterisco ou 1 anderescore

## Negrito e Itálico:
***Texto*** ou ___Texto___ -> Texto entre 3 asterisco ou 3 anderescore

## Tachado:
~~Texto~~ -> Texto entre ~~
________________________________________________________________
# Linha vertical:   
"=" ou "-" 
__________

# Bloco (Blockquote)
Basta colocar o sinal de maior ">" no inicio do paragrafo.
>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

Você poderá usar mais sinais de ">" para recuar o texto mais a direita.

_____________________________________________________

# Listas
Usa-se um número e o ponto para se fazer uma lista ordenada.
1. Segunda
2. Terça
3. Quarta
     1. Cortar cabelo
     2. Fazer compras
4. Quinta
5. Sexta

-----------------------------------------------------
Lista não ordenada você usa o "-" ou o sinal de "+"

- Primeiro elemento
- Segundo elemento
- Terceiro elemento
- Quarto elemento

\* A barra invertida antes do asterisco faz com que o processador Markdown interprete essa linha como um parágrafo e não um elemento de uma lista.
_______________________________________________________
# Links
Existem duas formas de inserir link em Markdown, através de um link direto ou usando um texto-âncora*:

-   **Texto-âncora**: utilize os caracteres `[]()`, adicionando entre chaves o texto que você quer que apareça, e entre os parênteses, o endereço de destino, no formato `[exemplo](https://exemplo.com/)`.

[Login trybe](https://app.betrybe.com/login)
    
-   **Link direto**: envolva o endereço da web em chaves `<>`. O endereço ficará visível e será clicável pelo usuário. O endereço em forma de link direto tem o formato `<https://exemplo.com/>`.

<https://app.betrybe.com/login>

Para criar um link de e-mail basta colocar entre os sinais de menor e maior.

<gabrielmatina@hotmail.com>

#### Enfatizando links
Ao adicionar asteriscos ao redor da formatação de link, ou seja, antes dos colchetes e depois dos parenteses, você indica para o processador Markdown que aquele link deve ser enfatizado.

Acesse meu e-mail: **[E-mail Gabriel Matina]<gabrielmatina@hotmail.com>**


____________________________________
# Imagens
O código para inserir uma imagem no conteúdo é semelhante ao código de inserir links-âncora, adicionando um ponto de exclamação `!` no início do código.

```
Imagem internet: ![title](link_da_imagem.png)
```

![Google](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)
```
Imagem Local: ![title](Images/example.png)
```

![Google](googlelogo.png)

------------------------------------------------
# Texto como código
Usando o Markdown nós podemos demarcar uma parte do conteúdo como código usando crases . Coloque uma crase antes e depois do texto que será interpretado pelo processador Markdown como código.


>`loop(food = 0; foodNeeded = 10) {
`  if (food = foodNeeded) {
   ` exit loop;
    // Nós temos comida o suficiente, Vamos para casa
  `} else {
    `food += 2;` // Passe uma hora coletando mais 2 alimentos(food)
    `// loop será executado novamente
  `}
`}

No exemplo acima além da crase foi usado o blockquote.

______________________________
# Criando Tabelas
Para criar uma tabela em Markdown nós usamos traços `–` e barras verticais `|` para separar linhas e colunas.

A primeira linha da tabela é onde construímos o cabeçalho, separando essa linha por três ou mais traços `---` para que o processador Markdown entenda a formatação.

A separação das colunas é feita usando a barra vertical `|`, também chamada de pipe por programadores.

Título  | Título
------- | --------
Texto   | Texto
Texto   | Texto








