[[Soft Skills]]

Gerentes não querem pensar mais do que já precisam. Eles utilizam [princípios simples e básicos](http://www.informit.com/articles/article.aspx?p=1984066) para olhar para os problemas e direcionar os resultados. Quanto mais simples, melhor.

Um desses princípios que é muito útil é a [regra 80:20, ou Regra de Pareto](http://pt.wikipedia.org/wiki/Princ%C3%ADpio_de_Pareto):

> 80% das consequências advêm de 20% das causas, e 80% dos resultados advêm de 20% de esforço.

É o outro lado da moeda da [diminuição de retornos](http://swreflections.blogspot.com.br/2011/11/diminishing-returns-in-software.html): ao invés de ter menos ao fazer mais, você pode ter mais ao fazer menos, ao trabalhar de maneira mais inteligente.

Você pode ver alguns casos óbvios de como a regra 80:20 se aplica a software. Por exemplo, 80% de melhorias de desempenho podem ser feitas para otimizar 20% do código – apesar de a taxa ser, na verdade, muito mais próxima de 90:10 ou mesmo de 99:1, quando falamos de otimização de desempenho. Mas não importa se é 80:20, 90:10 ou mesmo 70:30, é basicamente tudo a mesma coisa.

## 80:20 quem usa o quê; o que você realmente tem que entregar

Outra aplicação da regra em software é que 80% dos usuários utilizam apenas 20% das features. Essa afirmação é de uma pesquisa de 2002 do Standish Group, que também fala que:

-   45% das características de um sistema nunca são utilizadas;
-   19% são usadas raramente;
-   16% às vezes;
-   Apenas 20% são usadas com frequência ou sempre.

Assim como a [curva de custos de mudança](https://imasters.com.br/desenvolvimento/software/o-custo-real-da-mudanca-em-desenvolvimento-de-software/), esse é um outro exemplo de uma “grande verdade” em desenvolvimento de software que é baseada em uma evidência limitada – seria muito bom se tivéssemos mais pesquisas que reforçassem isso.

Isso foi altamente influenciado por [Agile](http://pragprog.com/magazines/2011-02/way-of-the-agile-warrior) e Lean, encorajando as pessoas a focarem no [menor entregável possível](http://www.jamesshore.com/Articles/Business/Software%20Profitability%20Newsletter/Phased%20Releases.html) ([Minimum Viable Product – MVP](http://www.startuplessonslearned.com/2009/08/minimum-viable-product-guide.html)), até mesmo em [projetos de grande porte](http://www.infoq.com/news/2013/01/enterprise-MVP). Em vez de tentar desenhar e planejar tudo o que o sistema pode precisar, você faz pequenas entregas com maior frequência, [priorizando o que é mais urgente](http://www.romanpichler.com/blog/agile-product-innovation/the-vision-the-product-backlog-and-the-minimal-viable-product/).

Uma [pesquisa mais recente](http://versionone.com/assets/img/files/ChaosManifesto2013.pdf) do Standinsh Group mostra que pensar em tamanhos menores e entregar menos é a chave para aumentar o sucesso de projetos de software: enquanto mais de 70% dos pequenos projetos têm uma entrega bem-sucedida, projetos grandes têm “chance de virtualmente não alcançar nenhum sucesso:… mais que duas vezes a chance de atraso, ultrapassar o orçamento ou ficar sem features críticas”.

> Em resumo, não há dúvidas de que focar nos 20% de features que vão entregar 80% de valor vai maximizar o investimento em desenvolvimento de software e aumentar a satisfação do usuário. Afinal, nunca há tempo ou dinheiro suficientes para se fazer tudo. A expectativa natural é que executivos e stakeholders queiram tudo, e queiram já. Portanto, reduzir o escopo e não fazer 100% dos recursos e funções não só é uma estratégia válida, mas uma bastante prudente.

Mas pensar em entregas entregas pequenas e menos rápidas também tem um lado negativo: uma “redução no valor e na inovação”, quando se trabalha em um nível de segurança muito grande e o limite colocado é baixo. Entregar 20% ou 50% de um sistema [nem sempre será o suficiente](http://www.startupblender.com/product-planning/minimum-viable-product-vs-minimum-delightful-product) para atingir sucesso, mesmo supondo que você possa calcular qual é a porcentagem necessária – algumas vezes, alguns desses “recursos extras” [ainda são necessários para alguém](http://www.joelonsoftware.com/articles/fog0000000020.html), mesmo que não sejam muito utilizados. Você vai precisar de [mais que um MVP](https://medium.com/lets-make-things/308d8f009b13) para redefinir um mercado ou como as pessoas trabalham ou jogam.

## 80:20 bugs e testes

Qualidade de código, bugs e testes são outra área na qual a regra 80:20 é útil:

-   80% dos bugs estão em 20% do código
-   90% de downtime vêm de 10% (ou menos) de defeitos

Bugs [formam clusters em algumas partes do código](https://www.youtube.com/watch?v=zXRxsRgLRZ4), especialmente bugs sérios. A maior parte dos seus [problemas mais sérios virá de um pequeno número de bugs](http://www.cs.umd.edu/projects/SoftEng/ESEG/papers/82.78.pdf).

> 80% dos erros e quebras no Windows e no Office foram causadas por 20% de todos os bugs detectados – [Microsoft’s CEO: 80-20 Rule Applies to Bugs, Not Just Features Oct 2002](http://www.crn.com/news/security/18821726/microsofts-ceo-80-20-rule-applies-to-bugs-not-just-features.htm)

Entender onde estão os seus bugs mais sérios e por que eles estão ali e o que você precisa fazer para evitá-los é em que você precisa gastar muito do seu tempo.

Alguns estudos mostram que [metade do seu código pode não ter nenhum bug](http://www.cs.umd.edu/projects/SoftEng/ESEG/papers/82.78.pdf), enquanto a [maioria deles será encontrada em 10% ou 20% do código](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.12.7165&rep=rep1&type=pdf) – geralmente os 10%-20% que são mudados com mais frequência (veja abaixo o subtítulo “80:20 – Que código deve ser mudado e com qual frequência).

Cada vez que você encontra um bug nesse código, são grandes as chances de que existam outros. Quanto mais bugs você encontrar, há mais chances de que ainda existam outros.

Capers Jones diz que ter que trabalhar em [código com alto risco de erros](http://books.google.ca/books?id=_t5l5Cn0NBEC&pg=PA408&dq=capers+jones+error-prone+modules&hl=en&sa=X&ei=ooRyUouRAsPt2QWup4G4Aw&ved=0CDAQ6AEwAA#v=onepage&q=capers%20jones%20error-prone%20modules&f=false) é o [maior dreno de produtividade de um desenvolvedor no ciclo de vida de um sistema](http://www.crosstalkonline.org/storage/issue-archives/2007/200712/200712-Jones.pdf), e que não encontrar o que está causando o problema e fazer algo sobre isso é um dos erros mais caros que um time de desenvolvimento pode fazer.

Cada vez que você mexe nesse código, mesmo se estiver tentando consertá-lo, há uma grande chance de que você o deixará pior, e não melhor: há mais de 20% de chance de que um desenvolvedor, ao tentar consertar um bug em um código propenso a isso, vai, acidentalmente, fazer um novo bug. É como um efeito colateral. Grande parte do esforço colocado em entender o código e consertá-lo e entender e corrigir de novo e de novo é um grande desperdício. “A maioria das partes suscetíveis a erros são tão complexas e difíceis de entender que não podem ser reparadas após criadas”.

Quando um código se torna ruim, ele precisa de um “[refatoramento grande e brutal](http://www.markhneedham.com/blog/2011/05/11/xp-2011-michael-feathers-brutal-refactoring/)”, de forma a se tornar novamente compreensível e seguro para trabalhar, ou então ser “removido e recolocado cirurgicamente” com um novo código escrito do zero por alguém que saiba o que está fazendo.

Não é difícil de identificar quais partes do código são ruins se você tem as mesmas pessoas trabalhando nele por um tempo – pergunte a qualquer um do time e eles saberão onde é problemático. Em grandes sistemas e grandes organizações, com um grande volume de negócios, você provavelmente vai precisar [procurar bugs ao longo do tempo](https://imasters.com.br/desenvolvimento/bug-e-algo-terrivel-para-se-desperdicar/) e minar dados defeituosos em clusters de bugs, mais do que apenas corrigir os bugs e seguir com a vida.

> 80% do tempo gasto resolvendo bugs estão em 20% dos bugs

Alguns bugs são muito mais difíceis de serem corrigidos do que outros. Às vezes, porque o código é tão ruim (veja a regra acima). Às vezes, porque os problemas são difíceis de ser reproduzidos e debugados. Ou porque eles são muito mais profundos do que parecem ser. Estejam preparados para esses tempos quando até mesmo o seu melhor desenvolvedor não vai conseguir te dizer quando – ou se – alguns bugs serão resolvidos.

## 80:20 – que código deve ser mudado e com qual frequência

Michael Feathers encontrou outras aplicações do princípio 80:20 ao observar mudanças na base do código ao longo do tempo (veja o vídeo “[Discovering Startling Things from your Version Control System](http://www.youtube.com/watch?v=0eAhzJ_KM-Q)”):

> 80% das mudanças são feitas em 20% do código

Muitos códigos são escritos uma vez e nunca mais modificados: interfaces estáticas e padronizadas, configurações básicas, funções de back office. Então, há outro código que muda o tempo todo: 20% das features que são usadas em 80% do tempo e precisam de algumas modificações e até mesmo reformulações; código do core que precisa ser otimizado; e outros, que precisam ser constantemente arrumados porque contêm muitos bugs (de novo a regra dos clusters de bugs que vimos acima).

Feathers percebeu que códigos que são constantemente mudados também tendem a se tornarem maiores com o tempo, por conta de uma [tendência implícita](http://www.markhneedham.com/blog/2009/09/30/book-club-design-sense-michael-feathers/): é mais fácil acrescentar código a um método existente do que criar um novo método, e é mais fácil acrescentar um método a uma classe existente do que criar uma nova classe.

Como resultado, muitos sistemas terminam com algumas [poucas classes grandes que contêm alguns poucos métodos grandes](http://michaelfeathers.typepad.com/michael_feathers_blog/2012/12/behavioral-economics-and-code.html), e que continuam crescer à medida que o código é modificado.

[Hot spots em códigos](http://en.wikipedia.org/wiki/Hot_spot_%28computer_programming%29) são facilmente encontrados ao se revisar o histórico de áreas de churn e através de análises estáticas simples da base do código. É aí que você tem as maiores vantagens de um refatoramento, onde você pode fazer o máximo para evitar que seu código perca a estrutura e se torne perigosamente insustentável de ser mantido – e também é o código que deveria ser refatorado mais frequentemente como parte de fazer mudanças (mais mudanças = mais refatoração, se você fizer isso direito).

## 80:20 e o tempo de programação

[Os primeiros 80% do código são feitos em 20% do tempo](http://stackoverflow.com/questions/608748/how-to-avoid-the-80-20-rule-in-software-development)… os 20% restantes do código levam os 80% restantes do tempo.

Geralmente não leva muito tempo para que algo quase funcione, [ou ao menos aparente que funciona](http://www.unwesen.de/2010/09/30/8020-rule-in-software-development-revisited/), especialmente se você estiver trabalhando de maneira iterativa e incremental, entregando frequente e rapidamente.

Mas há muito trabalho que ainda precisa ser feito nos “bastidores” para terminar tudo, para acertar as arestas e garantir que o sistema tenha bom desempenho e boa escalabilidade, encontrar e corrigir todos os pequenos bugs, melhorar o código antes de fazer o deploy. Product Owners/Clientes (e gerentes) geralmente não entendem por que leva tanto tempo para finalizar os “últimos 20%” do trabalho. E os programadores geralmente esquecem isso, e não incluem isso nas suas estimativas. É por isso que o tempo estimado por um desenvolver é geralmente errado. E porque fazer uma prototipagem pode ser tão perigosa, ao apresentar expectativas irreais.

## 80:20 e o gerenciamento de desenvolvimento de software

Ter sempre em mente a regra 80:20 vai te poupar tempo e dinheiro, e melhorar as suas chances de sucesso, ao te manter focado no que realmente é importante: as características necessárias, as partes do código onde estão os seus bugs mais sérios (e os que levam mais tempo para serem consertados); as partes do código que mudam com frequência; e como e onde o seu time gasta o tempo.

Fonte: [imasters.com.br](https://imasters.com.br/desenvolvimento/aplicando-regra-8020-ao-desenvolvimento-de-software)
