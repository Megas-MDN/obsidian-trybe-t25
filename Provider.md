[[React]]
[[Redux]]
[[State]]


O `<Provider>` componente disponibiliza o Redux `store` para quaisquer componentes aninhados que precisem acessar a store do Redux.

Como qualquer componente React em um aplicativo React Redux pode ser conectado à loja, a maioria dos aplicativos renderizará um `<Provider>` no nível superior, com toda a árvore de componentes do aplicativo dentro dele.

Os [Hooks](https://react-redux.js.org/api/hooks) e [`connect`](https://react-redux.js.org/api/connect)APIs podem então acessar a instância de armazenamento fornecida através do mecanismo Context do React.

### [Adereços](https://react-redux.js.org/api/provider#props "Link direto para o título")[](https://react-redux.js.org/api/provider#props "Link direto para o título")

```jsx
interface ProviderProps<A extends Action = AnyAction, S = any> {  
/**  
* The single Redux store in your application.  
*/  
store: Store<S, A>  
  
/**  
* An optional server state snapshot. Will be used during initial hydration render  
* if available, to ensure that the UI output is consistent with the HTML generated on the server.  
* New in 8.0  
*/  
serverState?: S  
  
/**  
* Optional context to be used internally in react-redux. Use React.createContext()  
* to create a context to be used.  
* If this is used, you'll need to customize `connect` by supplying the same  
* context provided to the Provider.  
* Initial value doesn't matter, as it is overwritten with the internal state of Provider.  
*/  
context?: Context<ReactReduxContextValue<S, A>>  
  
/** The top-level React elements in your component tree, such as `<App />` **/  
children: ReactNode  
}
```

Normalmente, você só precisa passar `<Provider store={store}>`.

Você pode fornecer uma instância de contexto. Se você fizer isso, também precisará fornecer a mesma instância de contexto para todos os seus componentes conectados. A falha em fornecer o contexto correto resulta neste erro de tempo de execução:

> Violação invariável
> 
> Não foi possível encontrar "loja" no contexto de "Connect(MyComponent)". Envolva o componente raiz em um `<Provider>`, ou passe um provedor de contexto React personalizado `<Provider>`e o consumidor de contexto React correspondente para Connect(Todo) nas opções de conexão.



