
TDD é o Desenvolvimento Orientado por Testes (Test Driven Development). Isso mesmo! Desenvolvemos o nosso software baseado em testes que são escritos antes do nosso código de produção!

Se você nunca ouviu sobre TDD, ou já ouviu mas nunca tentou, sugiro ferozmente que você continue lendo o artigo e procure sobre o assunto! A ideia do TDD já é antiga e foi firmada com o mestreKent Beck([Autor também do famoso livro sobre TDD](https://www.amazon.com/Test-Driven-Development-Kent-Beck/dp/0321146530 "Test Driven Development: By Example"), que recomendo) e é um dos pilares (lê-se práticas) do [Extreme Programming](https://www.devmedia.com.br/introducao-ao-extreme-programming-xp/29249 "Introdução ao Extreme Programming")!

Basicamente o TDD se baseia em pequenos ciclos de repetições, onde para cada funcionalidade do sistema um teste é criado antes. Este novo teste criado inicialmente falha, já que ainda não temos a implementação da funcionalidade em questão e, em seguida, implementamos a funcionalidade para fazer o teste passar! Simples assim!

Calma! Não tão rápido pequeno samurai! Não podemos simplesmente escrever outro teste só por que já temos um teste passando. É preciso que esta funcionalidade que acabamos de escrever seja refatorada, ou seja, ela precisa passar por um pequeno banho de "boas práticas” de [Desenvolvimento de Software](https://www.devmedia.com.br/atividades-basicas-ao-processo-de-desenvolvimento-de-software/5413 "Atividades básicas ao processo de desenvolvimento de Software"). Estas boas práticas que garantirão um software com código mais limpo, coeso e menos acoplado.

### Ciclo de desenvolvimento

Red,Green, Refactor. Ou seja:

-   Escrevemos um Teste que inicialmente não passa (Red)
-   Adicionamos uma nova funcionalidade do sistema
-   Fazemos o Teste passar (Green)
-   Refatoramos o código da nova funcionalidade (Refactoring)
-   Escrevemos o próximo Teste

![Ciclo de desenvolvimento do TDD](https://arquivo.devmedia.com.br/marketing/img/18533/TDD.png)

**Figura 1**. Ciclo de desenvolvimento do TDD

Nós temos, neste tipo de estratégia, um feedback rápido sobre a nova funcionalidade e sobre uma possível quebra de outra funcionalidade do sistema. Assim tempos muito mais segurança para as refatorações e muito mais segurança na adição de novas funcionalidades.

### Motivos para o uso

Temos diversos ganhos com esta estratégia e vou citar alguns:

-   Feedback rápido sobre a nova funcionalidade e sobre as outras funcionalidades existentes no sistema
-   Código mais limpo, já que escrevemos códigos simples para o teste passar
-   Segurança no Refactoring pois podemos ver o que estamos ou não afetando
-   Segurança na correção de bugs
-   Maior produtividade já que o desenvolvedor encontra menos bugs e não desperdiça tempo com depuradores
-   Código da aplicação mais flexível, já que para escrever testes temos que separar em pequenos "pedaços" o nosso código, para que sejam testáveis, ou seja, nosso código estará menos acoplado.

### Mito

Muitos ainda não gostam da ideia do TDD pelo fato de termos mais código a ser desenvolvido, acarretando maior tempo no desenvolvimento de uma funcionalidade. Mas isto está errado. Com toda certeza você desenvolvedor já corrigiu um bug no sistema, mas criou outros dois no lugar. Isto acontece com muita frequência e muitas das empresas ainda pagam os desenvolvedores somente para corrigirem bugs e até reescreverem sistemas cuja manutenção é terrível, traumática e sangrenta!

### Reforçando os motivos

A médio prazo (e dependendo do sistema a curto prazo) este tempo de desenvolvimento com TDD é menor que o tempo de manutenção corrigindo bugs e mesmo para adicionar funcionalidades novas. Isto devido, resumidamente, a:

-   Confiança do desenvolvedor na correção de bugs, pois qualquer passo errado será mostrado pelos testes
-   Tempo de desenvolvimento menor na adição de funcionalidades, já que o sistema é mais flexível e o código mais limpo
-   Menor tempo do desenvolvedor ao corrigir bugs após aquelas incessantes brigas com o pessoal de qualidade depois da famosa frase "Mas na minha máquina funciona!"
-   Possibilidade de Integração Contínua, com builds automáticos e feedbacks rápidos de problemas.

**Nota**: Sendo chato, parte I

Sei que é chato, mas ainda falarei um pouco de teoria neste início, para que realmente possamos entender (leia-se lembrar!) sobre alguns conceitos e motivos do uso de TDD.

Como havia dito, o TDD se baseia no ciclo visto na Figura 1, Vamos entender um pouco sobre cada etapa:

### Novo Teste

Este primeiro passo é o pilar do TDD (não brinca!). Temos uma nova funcionalidade do sistema e fazemos o processo inverso ao tradicional: Testamos e Codificamos e não Codificamos e Testamos. No primeiro momento isto parece estranho, esquisito ou feio, mas não é. O fato de termos um teste primeiro que o código garante que daremos passos simples para a codificação da funcionalidade, afim de fazer o teste passar, ou seja, seremos "obrigados" a escrever uma implementação simples para que o teste passe.

No começo esta forma não é muito intuitiva e o gráfico de aprendizagem não é lá um dos melhores, mas com o tempo e aperfeiçoamento da técnica, esta será a forma mais intuitiva e segura de desenvolver que você encontrará.

### Teste Falhando

Neste momento, acabamos de escrever o teste e não temos a implementação. Óbvio que o teste falhará, pois ele espera uma resposta que ainda não temos implementada em lugar algum. Com um Teste falhando na nossa frente, temos um único objetivo na vida: Fazê-lo passar! Passamos para a próxima fase:

### Nova funcionalidade

Já ouviu falar no [KISS](https://pt.wikipedia.org/wiki/Keep_It_Simple "Wikipédia")? "Keep It Simple, Stupid", ou seja, devemos escrever o nosso código da forma mais simples possível. Código limpo, simples e funcional! Esta é a ideia. Assim, neste momento vamos esquecer as Boas práticas, a Inversão de Controle, os Patterns, etc e vamos codificar a nossa nova funcionalidade da forma mais simples possível para fazer o nosso Teste passar. Neste momento estamos simplesmente escrevendo alguma funcionalidade que faça o teste passar (sem quebrar outros testes) e também teremos segurança na Refatoração deste mesmo código daqui a alguns minutos. Vale lembrar também daquela sequência ótima de desenvolvimento que devemos ter na cabeça: Código que funciona -> Código simples e limpo -> Código rápido.

Agora com a nova funcionalidade implementada e o teste passando, seguimos para a próxima fase:

### Refatoração

Agora sim! Você purista da programação que condenou a minha geração por eu ter falado para abandonarmos as boas práticas de desenvolvimento, agora sim pode ficar tranquilo! Neste momento é que vamos analisar melhor aquele código que fizemos simplesmente para o nosso Teste passar. É neste momento que retiramos duplicidade, renomeamos variáveis, extraímos métodos, extraímos Classes, extraímos Interfaces, usamos algum padrão conhecido, etc. É neste momento que podemos deixar o nosso código simples e claro e o melhor de tudo: Funcional!

Temos um teste agora que indicará qualquer passo errado que podemos dar ao melhorar o nosso código. E não somente este código que acabamos de escrever. Após algum tempocom TDD, será criada uma Suite de Testes, onde poderemos refatorar sem a preocupação de atingir negativamente algum código já existente, pois já teremos Testes indicando qualquer falha.

Já ouviu falar no [SRP](https://www.devmedia.com.br/curso/curso-padroes-de-projeto-com-csharp/376 "Curso Padrões de Projeto com C#")? "Single Responsibility Principle". Este princípio nos diz que devemos ter somente um motivo para modificar uma classe. Ou seja, ele fala sobre termos uma classe com somente uma responsabilidade. Por que estou lembrando disso? Por que o TDD nos "força" a termos classes seguindo esta regra, pois facilita os Testes. Não podemos refatorar um trecho de código e quebrar vários Testes. Assim, este princípio acaba sendo utilizado, mesmo que você não perceba. Pronto! Como acabamos a refatoração, o próximo passo é o próximo Teste!

**Nota**: Sendo chato, parte II

No último passo aplicamos a Refatoração, que é a melhoria do código. Isto se faz necessário(leia-se bom) sim em relação às boas práticas já conhecidas, porém com TDD isso se torna obrigatório! Por que? Simples! Para escrevermos um Teste, escrevemos uma funcionalidade, mas esta funcionalidade não pode quebrar outro Teste. Ao quebrar outro Teste, temos que fazer um pequeno esforço para que o nosso novo código esteja menos acoplado ao código restante.

Viu o que aconteceu? Trocamos a forma de desenvolvimento. Em vez de projetarmos a nossa aplicação e tentarmos escrever um código (levando horas) pensando nas mudanças no futuro, já pensando nos Patterns, regras e etc, escrevemos um código de Teste que guiou a simplicidade do nosso código, que em seguida refatoramos para deixá-lo menos acoplado e com uma maior coesão, fazendo com que este código seja facilmente modificado no futuro, seja para correção de problemas ou para novas funcionalidades.

### Mudanças seguras no código

Muitos desenvolvedores ainda escrevem código pensando nas modificações no futuro que este código poderia ter e acaba escrevendo um código com Factory, Singleton, Template Method, Bridge, Strategy e todos os amigos do [GoF](https://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612 "Design Patterns: Elements of Reusable Object-Oriented Software"). Este pensamento, apesar de parecer seguro, contraria os princípios da Metodologia Ágil.

Claro que o software sempre sofrerá mudanças e a nossa preocupação de hoje é: Prever/Escrever um código/design para modificar no futuro quando precisarmos.

Mas deveria ser, escrever um código simples e claro, que seja fácil modificar e seguro.

Kent Beck, no seu livro também comenta sobre perdermos muito tempo imaginando um Design que seja perfeito para aplicação e acabamos escrevendo um código que na maioria das vezes não era necessário. Com TDD realmente abandonamos este pensamento, justamente por queremos que o Teste passe logo, ou seja, escrevemos o nosso código da forma mais simples possível.

-   Como conseguimos um código simples? - Fazendo um Teste passar
-   Como conseguimos um código claro? - Refatorando o código após ele passar
-   Como conseguimos um código seguro? - Com Testes

### Documentação para o limbo?

Não. Aquela documentação no papel, em uma wiki, em um doc, etc é desatualizada pois é muito custoso atualizá-la a cada Refatoração/Mudança de código. A melhor documentação e mais atualizada possível é a Suíte de Testes pois ela mostra de forma simples como está funcionando o sistema naquele exato momento. Se você percorrer os testes você entenderá o que o sistema realiza.

### Hello World do TDD

Sim. Pra você que está ansioso por algo um pouco mais complexo, realmente neste momento não vamos ter. Assim podemos nivelar o conhecimento com um exemplo trivial, a fim de não deixar ninguém perdido. Vamos lá!

### Ambiente

Para o nosso "sistema" vou utilizar [Java](https://www.devmedia.com.br/guia/programador-java/37809 "Cursos de Java") + Eclipse + [JUnit](https://www.devmedia.com.br/testes-automatizados-com-junit/30324 "Testes automatizados com JUnit"). Imagino que você já conheça um pouco de Java e Eclipse, portanto não mostrarei a instalação deles pois fugiremos do escopo do artigo. Caso tenham algum problema, é só entrar em contato.

Alexandre, posso fazer em C#? A vontade! Pode usar C# + NUnit. Posso usar Delphi? A vontade! Pode usar Delphi + [DUnit](https://www.devmedia.com.br/testes-unitarios-automatizados-no-delphi/28229 "Testes Unitários Automatizados no Delphi")!

#### Primeiro exemplo

Este será um exemplo bem trivial. No nosso "sistema" precisaremos criar uma Calculadora que calcula as 4 operações básicas: Adição, Subtração, Multiplicação e Divisão. Simples assim! Passos para a criação do projeto:

-   Crie um novo projeto no Eclipse com o nome de ArtigoTDD;
-   Crie um pacote com o nome artigotdd.calculadora.teste.

Com a estrutura básica criada, agora vamos criar a nossa primeira classe. A classe Calculadora Alexandre? Não! A classe CalculadoraTeste? Isso mesmo. Vamos fazer um Teste em algo que ainda não temos implementado. Assim, criamos a classe CalculadoraTeste no pacote criado:

```
package artigotdd.calculadora.teste;

public class CalculadoraTeste {

}
```

Tudo certinho por aqui. Agora devemos pensar sobre o nosso problema. Queremos fazer algumas operações nesta calculadora e para começarmos pensaremos em uma soma. Como podemos testar uma soma?

Simples e trivial: Dados dois valores, o resultado deveria ser a soma deles. Vamos então escrever exatamente este Teste! Vamos criar um método que indique este teste. Para o [JUnit](https://www.devmedia.com.br/junit-tutorial/1432 "JUnit Tutorial") entender que o método é "testável", temos a anotação @Test no método (Não esqueça do import do JUnit). Assim temos:

```
public class CalculadoraTeste {

public class CalculadoraTeste {
    @Test
    public void deveriaSomarDoisValoresPassados() throws Exception {

    }
}
```

Isso mesmo. O nome do nosso método deve mostrar exatamente o que ele está querendo fazer. É comum encontrar métodos de teste começando com "deveria" e inglês você também vai encontrar o "should". Agora que temos o método de teste, vamos indicar pra ele o que queremos. Vamos agora inserir duas variáveis e usar o método "assertEquals" do próprio JUnit.

Saiba mais: [Guia de Testes de Software](https://www.devmedia.com.br/guia/testes-de-software/34403 "Testes de Software")

Como o próprio nome diz, o assertEquals indica que estamos querendo afirmar algo. (Não esqueça do import: import static org.junit.Assert.*). Vamos ao código:

```
public class CalculadoraTeste {
    @Test
    public void deveriaSomarDoisValoresPassados() throws Exception {
        int valorA = 1;
        int valorB = 2;
        int soma = 0;

        assertEquals(3, soma);
    }
}
```

Pronto! Queremos o resultado 3 para a soma das variáveis valorA e valorB. Acabamos de escrever o Teste e óbvio que ele não passa. Vamos rodá-lo? Botão direito na classe de teste -> Run As -> JUnit Test. Barra vermelha, era o que temíamos!

![Teste falhou](https://arquivo.devmedia.com.br/marketing/img/18533/teste-tdd-1.png)

**Figura 2**. Teste falhou

Mas já esperávamos pois este é o ciclo: Test -> Red -> Green -> Refactor.

E o que o Trace nos diz? Você já ouviu essa frase do seu cliente? "Eu queria isso, mas está fazendo aquilo". É exatamente o que temos aqui:

![Trace com motivo do teste ter falhado](https://arquivo.devmedia.com.br/marketing/img/18533/failure-trace-tdd.png)

**Figura 3**. Trace com motivo do teste ter falhado

No nosso Trace, o JUnit indica que esperava o valor3porém foi encontrado o valor0. E agora o nosso objetivo é fazer o Teste passar! Colocamos agora a classe responsável pela implementação da funcionalidade:

```
public class CalculadoraTeste {
    @Test
    public void deveriaSomarDoisValoresPassados() throws Exception {
        int valorA = 1;
        int valorB = 2;
        Calculadora calculadora = new Calculadora();
        int soma = calculadora.soma(valorA, valorB);

        assertEquals(3, soma);
    }
}
```

Este código nem mesmo compila! Sendo bem ortodoxo em relação ao TDD, realmente este é o nosso próximo passo. Não criamos a classe pra depois usá-la e sim usamos a classe pra depois criá-la. Agora que o compilador gentilmente com uma linha vermelha e um "x" vermelho nos avisou do erro, basta criarmos a classe Calculadora. Vamos dar um passo um pouquinho maior agora e também criar o método "soma" na classe Calculadora, recebendo dois inteiros:

```
public class Calculadora {

    public int soma(int valorA, int valorB) {
        return 0;
    }
}
```

Ótimo! Se rodarmos o nosso Teste, vamos ver a barra vermelha novamente. Isso por que criamos o método mas ele não implementa o que precisamos. Vamos agora implementar:

```
public class Calculadora {

    public int soma(int valorA, int valorB) {
        return valorA + valorB;
    }
}
```

Agora sim! Rodando o nosso Teste temos a sonhada barra verde:

![Teste passou](https://arquivo.devmedia.com.br/marketing/img/18533/barraverde-tdd.png)

**Figura 3**. Teste passou

Agora temos a última etapa do ciclo: [Refatoração](https://www.devmedia.com.br/introducao-a-refatoracao/21377 "Introdução à Refatoração")! Como é um exemplo muito trivial não temos aqui alguma refatoração interessante, vamos deixar a refatoração para quando o nosso sistema crescer ou quando as funcionalidades forem modificadas e a refatoração aparecer naturalmente. Seguindo os mesmos passos anteriores, vamos criar agora o teste para a subtração. Desta vez não faremos passo a passo novamente, pois será idêntico ao método soma:

#### Teste da subtração

```
@Test
public void deveriaSubtrairDoisValoresPassados() throws Exception {
    Calculadora calculadora = new Calculadora();
    int valorA = 1;
    int valorB = 2;
    int soma = calculadora.subtrai(valorA, valorB);

    assertEquals(3, soma);
}
```

#### Método na classe Calculadora

```
public int subtrai(int valorA, int valorB) {
    return valorA - valorB;
}
```

A seguir falaremos sobre os Testes de Unidade em relação ao comportamento dos nossos objetos. Também falaremos sobre o conceito de Mock de Objetos, que é extremamente importante no TDD. Já vou adiantar que você ficará chateado com o que faremos para "Mockar" os nossos objetos, mas prometo que em seguida ficaremos muito felizes com uma solução bem mais bacana para isso. Calma! o conceito de "Mockar" objetos aparecerá logo!

Para iniciar este artigo, vamos fugir um pouco do conceito citado acima e fazer a funcionalidade de divisão de dois números para verificarmos a possibilidade de fazer Testes esperando que alguma Exceção ocorra. Isso mesmo! Por algum motivo você deseja lançar uma Exceção caso algo de errado aconteça e podemos fazer isso com o JUnit, apresentado no artigo anterior.

#### Teste da divisão

A funcionalidade é simples: Fazer a divisão de dois números. Lembrando: É um caso simples e isolado onde a intenção é você imaginar um caso real da sua aplicação. Então vamos para o Teste!

Mas aqui começaríamos com aquele conceito de BabySteps, onde faríamos passos curtos para chegarmos à solução, correto? Correto, porém os BabySteps não são uma regra xiita que devemos seguir à risca. Segundo o próprio Kent Beck em seu livro sobre TDD, os BabySteps são para quando realmente não temos confiança suficiente em escrever determinado código. Como ele cita também, não devemos desenvolver com BabySteps a todo momento e sim devemos ficar felizes por podermos fazê-lo quando desejarmos.

Agora que lembramos disso, vamos correr um pouquinho mais no código e escrever um pouco mais rápido que no artigo anterior, porém sinta-se à vontade para colocar a sua velocidade. Adicionando o método de Teste à nossa classe de CalculadoraTeste:

```
public class CalculadoraTeste {
    @Test
    public void deveriaDividirDoisValoresPassados() throws Exception {
        int valorA = 6;
        int valorB = 2;
        Calculadora calculadora = new Calculadora();
        int divisao = calculadora.divide(valorA, valorB);

        assertEquals(3, divisao);
    }
}
```

E na nossa classe Calculadora, vamos escrever o nosso método de produção:

```
public class  Calculadora {

    public int divide(int valorA, int valorB) {
        return valorA / valorB;
    }
}
```

Legal! Agora podemos rodar o nosso Teste e vê-lo passando. Uma observação simples: Não comentei nos artigos anteriores mas só para ter certeza que é de conhecimento de todos, vou comentar: Rodamos os nossos Testes clicando com o botão direito na classe de Teste, selecionando Run Ase em seguida selecionando o JUnit Test. >Agora temos um Teste verde na nossa frente!

![Teste passou após refatoração](https://arquivo.devmedia.com.br/marketing/img/18533/barraverdedivisao-tdd.png)

**Figura 4**. Teste passou após refatoração

Maravilha! Finalizamos? Não. E quando esperamos por uma exceção? Vamos atormentar os professores de matemática e fazer a seguinte alteração na nossa classe de Teste:

```
public class  CalculadoraTeste {
    @Test
    public void deveriaDividirDoisValoresPassados() throws Exception {
            int valorA = 6;
            int valorB = 0;  //divisão por zero!
            Calculadora calculadora = new Calculadora();
            int divisao = calculadora.divide(valorA, valorB);

            assertEquals(?, divisao);
    }
}
```

O que fizemos: atribuímos o valor zero à variável valorB. E o que esperamos no nosso assertEquals? Não tenho noção! Podemos esperar tudo, menos um valor! Sendo assim, na sua aplicação, você poderia mostrar uma mensagem para o usuário solicitando gentilmente que ele insira um valor coerente. E como podemos fazer um Teste esperando uma exceção? Vamos lá!

### Teste esperando por uma exceção

Podemos usar um parâmetro na própria anotação do JUnit (@Test) para indicar qual a exceção que estamos esperando receber. Assim teríamos o seguinte código para o nosso Teste:

```
public class  CalculadoraTeste {

    @Test
    public void deveriaDividirDoisValoresPassados() throws Exception {
            int valorA = 6;
        int valorB = 3;
        Calculadora calculadora = new Calculadora();
        int divisao = calculadora.divide(valorA, valorB);

        assertEquals(2, divisao);
    }

    @Test
    public void deveriaLancarUmaExcecaoIndicandoFalhaAoDividirUmNumeroPorZero()
             throws Exception {
        int valorA = 6;
        int valorB = 0;
        Calculadora calculadora = new Calculadora();
        int divisao = calculadora.divide(valorA, valorB);

        assertEquals(0, divisao);
    }
}
```

Mas infelizmente ao rodar, temos uma barra vermelha:

![Teste falhou após modificações](https://arquivo.devmedia.com.br/marketing/img/18533/barravermelhadivisao-tdd.png)

**Figura 5**. Teste falhou após modificações

Agora sim podemos fazer o nosso Teste passar adicionando o parâmetro à anotação do JUnit (@Test) :

```
public class CalculadoraTeste {

    @Test(expected = ArithmeticException.class)
    public void deveriaLancarUmaExcecaoIndicandoFalhaAoDividirUmNumeroPorZero()
            throws Exception {
        int valorA = 6;
        int valorB = 0;
        Calculadora calculadora = new Calculadora();
        calculadora.divide(valorA, valorB);
    }
}
```

E agora sim temos a barra verde para o nosso Teste:

![Teste aprovado após ajustes](https://arquivo.devmedia.com.br/marketing/img/18533/barraverdedivisaoporzero-tdd.png)

**Figura 6**. Teste aprovado após ajustes

Este foi um caso simples para mostrar como é possível trabalhar com Testes que devem verificar exceções. Podemos estender este conceito para outros momentos, como fazer um Teste que não deveria esperar uma exceção que já esta poderia ser tratada pela nossa classe Calculadora ,pois fazer da forma acima não é tão interessante. Agora vamos melhorar os nossos testes!

### Indo mais além

Até agora fizemos testes bem simples e a ideia é imaginarmos outras funcionalidades em nossas aplicações reais de forma a desenvolvê-las desta forma. Claro que uma classe do tipo Calculadora não é o melhor dos exemplos, mas optei pela simplicidade até agora. De qualquer forma, tenho certeza que sua aplicação poderá ter muitas funcionalidades que, se bem isoladas, serão também passíveis de testes semelhantes.

Agora podemos avançar um pouco mais! Começamos o artigo com uma nova palavra: "Mock".

-   Definição simples - Um Mocké basicamente um objeto falso, que é capaz de simular as dependências de um objeto e é capaz de simular determinadas ações desse objeto.
-   Por que é usado? - Para testar o comportamento de outros objetos desejados.
-   Por que gostaríamos de testar o comportamento de outros objetos? - Justamente para termos certeza de que tudo ocorreu conforme pensamos. Vamos imaginar a seguinte situação: Temos uma aplicação onde cada vez que excluímos uma pessoa, um log é gerado no banco no banco de dados com o nome da pessoa que foi excluída.
-   Como poderíamos ter certeza que a geração do log realmente vai ser chamada e que nada de ruim acontecerá no caminho? - Podemos fazer este teste usando exatamente um Mock da classe de Log. Vamos fazer o código mais simples que vier na nossa cabeça:

```
//Classe do nosso Teste
public class PessoaTeste {
    @Test
    public void deveriaCriarUmLogQuandoUmaPessoaForExcluida()
           throws Exception {
        Pessoa pessoa = new Pessoa();
        pessoa.setNome("Alexandre");
        PessoaController pessoaController = new PessoaController();
        pessoaController.exclui(pessoa);
        // Como saberemos se realmente o "criaLog" será chamado?
    }
}
//Nosso Controller
public class PessoaController {

    private PessoaDAO pessoaDAO;
    private Log log;

    public PessoaController() {
        pessoaDAO = new PessoaDAO();
        log = new Log();
    }

    public void exclui(Pessoa pessoa) {
        PessoaDAO.exclui(pessoa);
        log.criaLog(pessoa.getNome());
    }
}
//Nossa classe de criação de Logs
public class Log {

    public void criaLog(String nomeDaPessoa) {
        // Código para criar um Log no banco, em um txt, etc...
    }
}
```

Eu sei, eu sei. Abandonamos aqui algumas boas práticas mas é em prol de um entendimento melhor da situação. Logo logo vamos melhorar um pouco mais este código. Voltamos à mesma pergunta: Como vamos saber se a criação do Log foi chamada? Vamos criar um Mock da nossa classe de criação de Logs!

O nosso Mock deve simular o funcionamento da funcionalidade, ou seja, ele não conterá código algum, será apenas para verificarmos se ele foi chamado. Uma ideia seria criarmos uma classe que estende da nossa classe deLog, mas seremos um pouquinho melhores que isso e vamos criar uma Interface para implementarmos. Assim poderíamos ter:

```
//Nossa Interface de criação de Logs
public interface GeradorDeLog {
    public void criaLog(String nomeDaPessoa);
}
```

Podemos então ter a seguinte classe horrorosa:

```
//Mock da nossa classe de Log
public class LogMock implements GeradorDeLog {

    private String nome;

    @Override
    public void criaLog(String nomeDaPessoa) {
        this.nome = nomeDaPessoa;
    }

    public String getNome() {
        return nome;
    }
}
```

Mas temos um detalhe: O nosso Controller está com uma dependência forte que é a classeLog sendo instanciada diretamente pelo Controller. Isso impossibilita o uso do nosso Mock. Então vamos melhorar um pouquinho o Design da nossa aplicação. Opa! Olha o TDD nos "obrigando" a melhorar o Design da nossa aplicação!

Vamos então aplicar um princípio bem importante que é a [Inversão de Controle](https://www.devmedia.com.br/introducao-a-inversao-de-controle/29698 "Introdução à Inversão de Controle") através da Injeção de nossas Dependências. Vamos enviar então o nosso GeradorDeLogpara o Controller através do construtor. Assim teremos:

```
//Nossa classe de Teste
public class PessoaTeste {
    @Test
    public void deveriaCriarUmLogQuandoUmaPessoaForExcluida()
            throws Exception {
        Pessoa pessoa = new Pessoa();
        pessoa.setNome("Alexandre");

        LogMock nossoLogMock = new LogMock();
        PessoaController pessoaController = new PessoaController(nossoLogMock);
        pessoaController.exclui(pessoa);

        assertEquals(pessoa.getNome(), nossoLogMock.getNome());
    }
}
//Nosso Controller
public class PessoaController {

    private PessoaDAO pessoaDAO;
    private GeradorDeLog log;

    public PessoaController(GeradorDeLog log) {
        this.pessoaDAO = new PessoaDAO();
        this.log = log;
    }

    public void exclui(Pessoa pessoa) {
        PessoaDAO.exclui(pessoa);
        log.criaLog(pessoa.getNome());
    }
}
```

E olha que temos aqui, um teste passando!

![Novo teste aprovado](https://arquivo.devmedia.com.br/marketing/img/18533/barraverdeparamock-tdd.png)

**Figura 7**. Novo teste aprovado

### Recapitulando

Muitas vezes precisamos testar o comportamento dos nossos objetos. No nosso caso qual é o comportamento? A criação de um Log quando uma pessoa é excluída. Mas não queremos criar um Log de verdade quando fizermos o teste de exclusão e sim queremos verificar se o método da criação do Log foi chamado. Para fazermos isso, usamos um objeto "Mockado" que é um objeto que simula o comportamento do nosso objeto. É, a grosso modo, um objeto falso que não tem inteligência.

Assim, pelo Teste, na exclusão de uma pessoa um Log é gerado pois ao chamar o método de exclusão, o método de criação do Log também é chamado, ou seja, nada de errado acontece pelo caminho. Para uma visão geral do nosso Teste, vamos listar os nossos passos:

-   Criamos a nossa classe de Teste PessoaTeste;
-   Criamos as classes: PessoaController, Log, Pessoa;
-   Sentimos dificuldade para fazer o teste no Controller pois ele estava muito acoplado com a classe de Log;
-   Criamos a Interface GeradorDeLog para a nossa classe de Log implementá-la;
-   Fizemos a nossa classe LogMock também implementar a Interface GeradorDeLog;
-   Passamos para o nosso Controller a nossa classe de Log "Mockada", por Injeção de Dependência pelo construtor;
-   Identificamos pelo assertEquals se o método de geração de Log foi realmente invocado, verificando se o nome no Log era o mesmo nome da Pessoa.

### Finalizando

Legal! Conseguimos fazer o nosso Teste rodar, melhoramos um pouco o Design da nossa Aplicação aplicando a Inversão de Controle (mas podemos refatorar para algo bem melhor, claro!) mas acabamos ficando com essa classe horrorosa que é a LogMock.

Mas esta ideia não é só feia! Essa ideia só poderá ser usada caso tenhamos objetos simples. Imagine que temos um objeto que instância outro objeto e este também instancia outro objeto e cada um tem diversos métodos. A nossa vida se resumiria a criar classes de Mock e isso não é legal.

É neste ponto que podemos usar frameworks para isso. Podemos "Mockar" as nossas dependências através destes Frameworks sem precisar criar outras classes para isso! O desenvolvedor de hoje realmente tem que dominar a técnica que, apesar de parecer nova, é desde os primórdios da civilização Inca! O seu software funciona? Sim? Mas não tem testes? Então você não tem garantia alguma que ele funciona!

---

#### Saiu na DevMedia!

-   [Dê o próximo passo após o HTML/CSS!](https://www.devmedia.com.br/protocolo-http/ "Dê o próximo passo após o HTML/CSS!")
    
    Nesta série falamos sobre o que vem depois do HTML/CSS. Saiba o que é requisição, resposta e se prepare para os seus primeiros passos na programação back-end.
    
-   [API REST + Cliente web React + Mobile](https://www.devmedia.com.br/api-rest-react-mobile/ "API REST + Cliente web React + Mobile")
    
    Mesmo um programador experiente pode ter dificuldades em enxergar todos os passos para construir um software do início ao fim. Para a nossa sorte é o que mostramos na série dessa semana.
    
-   [Seja um mestre SQL](https://www.devmedia.com.br/sql/ "Seja um mestre SQL")
    
    Uma verdade sobre o SQL é que ou você já usa, estuda ou um dia, acredite, vai usar. Vem com a gente aprender passo a passo como conversar com o banco de dados nesta série.
    

---

#### Saiba mais sobre Engenharia de Software ;)

-   [Guias de Engenharia de Software](https://www.devmedia.com.br/guias/engenharia-de-software "Texto")
    
    Encontre aqui os Guias de estudo sobre os principais temas da Engenharia de Software. De metodologias ágeis a testes, de requisitos a gestão de projetos!
    
-   [Cursos de Engenharia de Software](https://www.devmedia.com.br/cursos/engenharia-de-software "Cursos de Engenharia de Software")
    
    Torne-se um programador, analista ou gerente de projetos com grandes habilidades de engenharia de software. Conheça metodologias e ferramentas como Scrum, XP, PMBOK, UML e muito mais.
    
-   [Últimas atualizações sobre Engenharia de Software](https://www.devmedia.com.br/engenharia-de-software/ "ÚLTIMAS ATUALIZAÇÕES ENGENHARIA DE SOFTWARE")
    
    Nesta página listamos os últimos artigos, vídeos e cursos sobre Engenharia de Software. Aprenda Gestão de Projeto, SCRUM, Requisitos, Modelagem e UML.


###### Fonte: [DevMedia](https://www.devmedia.com.br/test-driven-development-tdd-simples-e-pratico/18533)