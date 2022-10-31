[[React]]
[[Redux]]

Esta é uma função que retorna o estado mais recente da _store_. Precisaremos disso para atualizar nossa interface do usuário sempre que o usuário clicar em um botão.

```jsx
const state = store.getState()
```

###### Fonte: https://www.freecodecamp.org/portuguese/news/como-implementar-o-redux-em-24-linhas-de-javascript/