[[Docker]]


Ao falar de Microsserviços estamos falando, antes de tudo, **de uma decisão de arquitetura geral para aplicações**.

Essa arquitetura promove o desmembramento da aplicação toda em partes menores, que funcionam como serviços desse aplicativo.

Isso pode contribuir para a agilidade de times de desenvolvimento, dado que uma parte não é necessariamente dependente da outra. Por exemplo, em uma rede social, o serviço de atualizações de feed não é dependente do serviço de chat, mas ambos fazem parte do mesmo aplicativo.

Nesse sentido, a arquitetura mais popular para produção de sistemas em larga escala é a de **microsserviços**, e essa ilustração mostra como é um ambiente simples desse tipo:

![Diagrama de um ambiente simples](https://content-assets.betrybe.com/prod/Diagrama%20de%20um%20ambiente%20simples.png)

Diagrama de um ambiente simples

Aqui, nosso sistema possui dois front-ends (dois níveis de acesso diferentes), e essas duas frentes possuem acesso ao total de 3 serviços (sendo que um deles compartilha do mesmo banco de dados). No entanto, toda essa estrutura diz respeito à mesma aplicação: “TrybeTimes”.

Esse tipo de estrutura é amplamente escalável, ao ponto que podemos ter uma mega estrutura, como no exemplo abaixo:

![Diagrama de um ambiente complexo](https://content-assets.betrybe.com/prod/Diagrama%20de%20um%20ambiente%20complexo.png)

Diagrama de um ambiente complexo

Não é necessário focar em entender exatamente como é o fluxo desse sistema, basta compreender que cada uma das caixas verdes simboliza uma pequena API, **um microsserviço**.

> De forma bem básica, APIs são softwares dos quais consumimos alguma informação, algo no mesmo modelo do _Star Wars API (SWAPI)_ ou o _The Meal DB API_, utilizadas em projetos durante o curso.

Aqui esses pequenos softwares representam **partes específicas e isoladas de um software maior.**

> Por exemplo: imagine que esse fluxo todo representa uma rede social, você poderia pensar cada um dos microsserviços como um aspecto dessa rede social, então você poderia ter um serviço de feed de notícias, um chat, um serviço de perfis, etc.

Esse tipo de arquitetura é oposta àquela que chamados de **monolítica**, que por sua vez, **contém todos os aspectos de um software contidos em apenas uma aplicação**. Se ocorrer um problema nesse tipo de aplicação, todos os seus aspectos param de funcionar.

Imagine como seria pra uma pessoa desenvolvedora júnior ter que configurar cada um desses pequenos serviços que incluiriam desde sistema operacional a bibliotecas, softwares adicionais, banco de dados, etc, para só a partir daí conseguir rodar a aplicação e fazer alterações?

Para resolver esse problema, uma ferramenta como o _Docker_ para **empacotar** e **entregar** nosso _software_, da maneira mais simples e prática possível, é perfeita.

Com ele, **podemos colocar, num mesmo “pacote”, tudo que é necessário para nossa aplicação funcionar!**

Isso torna mais simples que possamos reproduzir o aplicativo de alguém sem a necessidade de fazer a configuração do ambiente toda vez. **Isso em qualquer ambiente!**

O **Docker** se encarrega de aproveitar tudo aquilo que ele tem em comum com o sistema em que ele está instalado **- o que chamamos também de** sistema hospedeiro **- criando aquilo que chamamos de** container **- o que seria nosso** sistema convidado**.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/f04cdb21-382e-4588-8950-3b1a29afd2dd/section/4a9c025a-d8d9-4a87-92ac-0903a07407b6/lesson/d2afe90a-6fb5-467d-98ad-2c66b315d0f6)

