[[React]]
[[Funções]]


## O que são Hooks?

A primeira pergunta que precisamos responder é: **afinal de contas, o que são Hooks?**

De forma objetiva, Hooks são funções. Todo e qualquer Hook sempre deverá ser uma função. Entretanto, os Hooks são funções especiais, uma vez que eles permitem _enganchar_ funcionalidades aos componentes de função. Daí o nome _Hook_ (gancho, em inglês). Por exemplo, podemos “enganchar” gerenciamento de estado com o Hook `useState` e gerenciar o ciclo de vida do componente com o Hook `useEffect`.

#### Regras dos Hooks

Existem algumas regras que você deverá seguir ao utilizar Hooks.

#### Nomenclatura

Como você deve ter notado, todos os Hooks começam com a palavra `use`. Isso é importante para diferenciar Hooks de funções _comuns_.

Da mesma forma que, quando encontramos um componente React com a primeira letra maiúscula (`MyComponent`) já sabemos que ele irá nos retornar `jsx`, quando encontramos uma função que começa com `use`, sabemos que se trata de um Hook. Também é importante para que outras ferramentas auxiliares (por exemplo ESLint) saibam identificar Hooks.

#### Como deverão ser invocados

Você nunca poderá chamar um Hook dentro de um `if`. Também não poderá chamá-lo dentro de um _loop_ ou uma função aninhada. Os Hooks **precisam** ser chamados no _top level_ (raiz) do componente funcional.

#### Onde deverão ser invocados

Você apenas poderá chamar um Hook dentro de um componente funcional ou dentro de outros Hooks. Você não pode utilizar Hooks em componentes de classe.

###### Fonte: [Curse](https://app.betrybe.com/learn/course/5e938f69-6e32-43b3-9685-c936530fd326/module/095ebb0d-1932-4d37-933b-9e1d721646fb/section/94fad02a-cf1d-4277-871d-1553af1aded4/day/8afaccae-ee94-4334-9d10-2f51359f061f/lesson/52b65a56-c103-44a5-bd16-bd2fcaf68680)
