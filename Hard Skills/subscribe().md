[[Store]]
[[Redux]]
[[Store]]
[[Callback]]



Geralmente iremos precisar fazer ações quando o estado global é atualizado. Por exemplo, toda a vez que o contador é incrementado, precisaremos renderizar o novo valor do estado na tela.

Para isso, o objeto `store` também disponibiliza a função `subscribe()`. Essa função recebe um callback que irá ser chamado toda vez que o estado global sofrer alterações:

```jsx
store.subscribe(() => {
    console.log(`O novo estado global é ${store.getState()}`)
})
```
