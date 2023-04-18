[[React]]
[[JavaScript]]

Os **métodos ágeis** são uma alternativa à gestão tradicional de projetos. Eles nasceram nos braços do desenvolvimento de software, mas hoje são aplicados a qualquer tipo de projeto. Esses métodos vêm ajudando muitas equipes a encarar as imprevisibilidades de um projeto por meio de entregas **incrementais e ciclos iterativos**.

Os **métodos ágeis** buscam promover um processo de gerenciamento de projetos que incentiva a inspeção e a adaptação frequentes. É uma filosofia que acaba por incentivar o maior trabalho em equipe, a auto-organização, a comunicação frequente, o foco no cliente e a entrega de valor.

Basicamente, os **métodos ágeis** são um conjunto de práticas eficazes que se destinam a permitir a entrega rápida e de alta qualidade do produto, tendo uma abordagem de negócios que alinha o desenvolvimento do projeto com as necessidades do cliente e os objetivos da empresa.

O nascimento dos métodos ágeis dá-se com o lançamento do **_Manifesto Ágil_**. Esse manifesto traz princípios para o desenvolvimento de software que tem como objetivo colocar clientes no centro do desenvolvimento, buscando entregar softwares que satisfaçam suas dores e necessidades. Com isso, os produtos respondem mais rapidamente às mudanças, entregando com maior frequência versões novas do software com melhorias incrementais.

O desenvolvimento tradicional, forma predominante antes da publicação do manifesto ágil, tinha como centro a documentação completa do projeto. O cliente só era envolvido quando o produto estava pronto. Esta forma tradicional, também chamada de cascata, tem um tempo muito mais lento de resposta à mudança, aprendizado e feedback, o que pode comprometer a entrega de valor e a relevância do produto. Sem envolver o cliente desde o início, corremos o risco de não atender nenhuma dor e entregar um produto obsoleto.

Ou seja, a partir de uma versão publicada, que atende um problema da forma mais simples e objetiva possível, pode-se evoluir o software de acordo com as necessidades dos clientes da empresas. Caso queira, pode ler o **_[Manifesto Ágil](https://agilemanifesto.org/iso/ptbr/manifesto.html)_** na íntegra, mas seu principais pilares são:

> 1.  Indivíduos e interações mais que processos e ferramentas
> 2.  Software em funcionamento mais que documentação abrangente
> 3.  Colaboração com o cliente mais que negociação de contratos
> 4.  Responder a mudanças mais que seguir um plano

É importante frisar que os itens da direita possuem valor no manifesto, mas os da esquerda devem estar em posição de destaque.

Pouco tempo após a publicação do manifesto e a consolidação da metodologia ágil no mercado, as fronteiras das empresas de desenvolvimento de software foram ultrapassadas. Hoje, as técnicas e filosofias dessa nova escola são aplicadas em empresas e organizações de diversas outras áreas. Essa popularização acabou por criar subtipos para a gestão ágil, cada um com suas peculiaridades: os chamados “_frameworks_“ ágeis.

Os _frameworks_ são ferramentas que têm como base os princípios ágeis e podem ser implantados em times ou empresas que desejam incorporar o **Agile** em suas práticas. Entretanto, nem sempre é possível seguir as regras dos _frameworks_ ao pé da letra. Por isso, há quem advogue que os princípios ágeis devem ser adaptados à realidade de cada área ou organização. Afinal, o mais importante é que os princípios fundamentais se mantenham e cumpram com o objetivo de facilitar e agilizar os processos e as entregas da equipe, sem gerar complexidade desnecessária.

### Scrum

**Scrum** é um _framework_ para gestão e planejamento de projetos. As equipes que trabalham neste método, geralmente, são divididas em **Product Owner (PO)**, **Scrum Master** e **Scrum Team** (ou **Time de Desenvolvimento**). Você, como pessoa desenvolvedora, deverá, geralmente, integrar a equipe desta última parte da divisão.

As **Metodologias ágeis** de desenvolvimento de software são iterativas, ou seja, o trabalho é dividido em iterações (ciclos). No Scrum, os projetos são divididos em ciclos chamados de **Sprints**.

O _Sprint_ representa um espaço de tempo, normalmente de 2 a 4 semanas, no qual um conjunto de atividades deve ser executado. As funcionalidades a serem implementadas em um projeto são mantidas em uma lista que é conhecida como **Product Backlog**. Este material contém todas as funcionalidades que foram elencadas como importantes para quem usa o produto, e é responsabilidade do _PO_ definir seu conteúdo. Estas informações não precisam necessariamente estar disponíveis no início de um projeto, podendo ser acrescidas, alteradas e melhoradas à medida que se aprende mais sobre o produto e quem o usa.

O próximo passo é conectar o que foi priorizado pela pessoa _PO_ com o _Scrum Team_. Para isso, no início de cada _Sprint_, faz-se um **Sprint Planning Meeting**, ou seja, uma reunião de planejamento na qual a pessoa _PO_ prioriza os itens do _Product Backlog_ e a equipe seleciona as atividades que ela será capaz de implementar durante o _Sprint_ que se inicia, originando o **Sprint Backlog**.

O status das tarefas do _Sprint Backlog_ será atualizado pela pessoa que for _Scrum Master_. Este papel entra para fazer a gestão dos valores e das práticas do _Scrum_, assegurando sua funcionalidade e garantindo que o que foi selecionado pode e deve ser entregue ao final do ciclo. É comum observar que, em algumas empresas, o papel de Scrum Master é desempenhado pela mesma pessoa que é liderança técnica do time de desenvolvimento (Tech Lead). Nestes casos, não existe uma pessoa que faz exclusivamente o papel de Scrum Master. Nas empresas que possuem uma pessoa com função exclusiva de Scrum Master, os papéis de Scrum Master e Tech Lead são separados. Isso quer dizer que, apesar da pessoa Scrum Master assumir uma responsabilidade importante de gestão das práticas ágeis do time, a liderança do time de desenvolvimento continua sendo o(a) Tech Lead.

Além das tarefas citadas, a pessoa Scrum Master atuará como facilitadora da **Daily Meeting** (ou **Daily Scrum** ou **DM**), uma reunião diária como o objetivo de disseminar a evolução do projeto, e identificar impedimentos que podem ser resolvidos com ajuda dos membros da equipe. A _Daily_ deve ser breve, e cada integrante deve basicamente responder à três perguntas:

-   O que você fez ontem?
-   O que fará hoje?
-   Há algum impedimento no seu caminho?

Ao final de um _Sprint_, a equipe apresenta as funcionalidades implementadas em uma **Sprint Review Meeting**. Devem participar desta reunião a pessoa _PO_, a pessoa _Scrum Master_, o _Scrum Team_ e, opcionalmente, clientes, a gerência e, se pertinente, pessoas técnicas de outros projetos. Serão avaliados se os objetivos da _Sprint_ foram cumpridos e o que isso representa no projeto em si.

Na última etapa da sprint no _Scrum_, faz-se uma **Sprint Retro Meeting** (ou **Sprint Retrospective**), onde são apontados os pontos positivos e negativos do último _Sprint_, assim como ações para mitigar os pontos negativos e evitar que se repitam. Após essa reunião, a equipe parte para o planejamento do próximo _Sprint_.

A figura abaixo ilustra o ciclo de uma `Sprint` no _Scrum_:
![[Pasted image 20221024190331.png]]
> Framework Scrum


### Kanban

O método `Kanban` foi criado pela japonesa _Toyota_ na década de 1960 e faz parte da metodologia **Just in Time**, um sistema de administração da produção que determina que deve ser feito somente o imprescindível para realização da etapa seguinte do processo, em um fluxo de trabalho contínuo. Em outras palavras: fazer apenas o que é necessário, quando necessário e na quantidade necessária.

Em meio à falta de recursos e diante da necessidade de se modernizar para acompanhar as mudanças do mercado, a empresa precisava mudar sua metodologia de gestão e procurar por uma **Gestão por Resultados**, ou seja um modelo que priorizasse os resultados de todos os colaboradores que nele atuam, permitindo que os gestores e seus times avançassem cautelosamente, porém de forma contínua e produtiva.

Era preciso agir rápido e urgentemente para criar um novo sistema de manufatura. Assim, inspirados pelo livro _Today and Tomorrow_, de Henry Ford, a diretoria da _Toyota_ desenvolveu o `Kanban`.

Diante das dificuldades da época, o fato do `Kanban` ser bastante visual facilitou muito o trabalho das equipes de produção e montagem. O sistema melhorou a comunicação entre as pessoas que trabalhavam na empresa, bem como o entendimento de quais peças precisavam ser repostas no momento correto. A padronização também foi auxiliada pelo sistema, assim como a redução de desperdícios.

A metodologia `Kanban` propõe a utilização de cartões ou `post-its` em um quadro para indicar e acompanhar, de maneira visual, prática e utilizando poucos recursos, o andamento dos fluxos de produção nas empresas. De um lado do quadro, ficam as tarefas que precisam ser executadas, o que pode ser chamado de **Backlog**, que são as funcionalidades e objetivos do projeto como um todo, podendo ou não estarem completamente prontos nos processos iniciais de desenvolvimento. E, do outro, as etapas de execução: em andamento e entregue. Você pode alterar o nome dessas etapas de acordo com seus processos internos. Conforme as tarefas são desempenhadas, o cartão ou `post-it` é colocado no campo correspondente ao status da tarefa.

#### Os benefícios do sistema Kanban

O `Kanban` nada mais é que uma maneira simples e visual de organizar as tarefas e o fluxo de trabalho, tornando tudo muito mais eficiente. Os benefícios do sistema `Kanban` são:

-   Visão do todo;
-   Simplicidade;
-   Acesso a informações;
-   Facilitação do fluxo de trabalho;
-   Incentivo à comunicação;
-   Prioridade e metas claras.

**Visão do todo**

Seja físico ou digital, o `Kanban` é visual. Isso é especialmente útil em situações em que várias pessoas ou grupos coordenam e cooperam em um mesmo projeto, ou processo, permitindo que essas pessoas planejem suas tarefas atuais e as seguintes. O `Kanban` oferece uma visão do todo, ou seja, uma perspectiva holística de um processo. Ao invés de fazer com que as pessoas trabalhem isoladamente, o sistema `Kanban` permite que todas as pessoas na organização tenham uma melhor compreensão e apreciação do que outras pessoas e equipes estão fazendo. A liderança de área, por sua vez, consegue ter uma visão concreta de quem está fazendo o quê e quantas etapas faltam para um projeto ser finalizado.

**Simplicidade**

A ideia e o conceito por trás do `Kanban` são simples. É isso que o torna atraente para quase todas as áreas de uma organização. A simplicidade permite que todas as pessoas participem com mais facilidade e comprem a ideia.

**Acesso à informação**

O `Kanban` tem processos inclusivos, que permitem que as pessoas tenham acesso a mais informações. Ele dá às pessoas mais conhecimento corporativo, o que é particularmente útil para aquelas que têm pouco entendimento de um sistema complexo, como, por exemplo, as pessoas recém-contratadas. No fim da cadeia, ele dá poder às pessoas e incentiva a autonomia.

**Facilitação do fluxo de trabalho**

O `Kanban` contribui para que haja menos desperdício nas operações, tornando tudo mais prático e conciso. Partes redundantes ou desnecessárias de um processo podem ser removidas, enquanto outras podem ser simplificadas. Ou seja, o fluxo de trabalho pode ser facilitado, sem comprometer a qualidade. Isso significa uma constante melhora na produtividade.

**Incentivo à comunicação**

Como o uso do `Kanban` fornece uma visão do todo, isso incentiva uma melhor cooperação e comunicação entre pessoas e equipes. As pessoas que trabalham na empresa poderão ajustar melhor seus cronogramas e prazos, porque sabem exatamente o que as outras pessoas estão fazendo. Por extensão, isso também serve como meio de controle e equilíbrio, no qual as ineficiências e gargalos ao longo do processo podem ser eliminados.

**Prioridades e metas claras**

O `Kanban` aprimora a capacidade de foco, pois, além do uso do `WIP limit`, o time tem uma visão ampla dos processos e do fluxo de trabalho, e a gerência fica mais capacitada para decidir o que de deve ser priorizado para atingir os objetivos e metas estabelecidas.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/095ebb0d-1932-4d37-933b-9e1d721646fb/section/dd1541c9-6ad1-4d6a-8344-48388e7262bc/day/691bd777-725c-4598-ad44-c08d79380b4c/lesson/e5477b27-45d7-4fe9-9c97-f43d6dc2bd1d)
