[[React]]
[[Redux]]
[[Actions]]
[[Objeto]]
[[Funções]]


Uma store contém toda a [árvore](https://redux.js.org/understanding/thinking-in-redux/glossary#state) de estado do seu aplicativo. A única maneira de alterar o estado dentro dele é despachar uma [ação](https://redux.js.org/understanding/thinking-in-redux/glossary#action) nele.  Uma loja não é uma classe. É apenas um objeto com alguns métodos nele. Para criá-lo, passe sua [função de redução](https://redux.js.org/understanding/thinking-in-redux/glossary#reducer) de raiz para [`createStore`](https://redux.js.org/api/createstore).

### Métodos da Sotore
- [[GetState()]]
- [[Dispatch(action)]]
- [[subscribe()]]
- replaceReducer(nextReducer)

###### Fonte: https://redux.js.org/api/store

