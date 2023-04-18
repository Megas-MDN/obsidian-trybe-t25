[[React]]
[[Props]]
[[State]]

### Sintaxe
```jsx
constructor(props)
```

**Se você não inicializar o estado e não vincular métodos, não precisará implementar um construtor para seu componente React.**
O construtor de um componente React é chamado antes de ser montado. Ao implementar o construtor para uma React.Componentsubclasse, você deve chamar super(props)antes de qualquer outra instrução. Caso contrário, this.propsficará indefinido no construtor, o que pode levar a bugs.

Normalmente, em construtores React são usados apenas para dois propósitos:

- Inicializando o estado local atribuindo um objeto a `this.state`.
- Vinculando métodos de manipulador de eventos a uma instância.

Você **não deve chamar`setState()`** no `constructor()`. Em vez disso, se seu componente precisar usar o estado local, **atribua o estado inicial`this.state`** diretamente no construtor:

```jsx
constructor(props) {
  super(props);
  // Não chame this.setState() aqui!
  this.state = { counter: 0 };
  this.handleClick = this.handleClick.bind(this);
}
```

Construtor é o único lugar onde você deve atribuir `this.state`diretamente. Em todos os outros métodos, você precisa usar `this.setState()`em vez disso.

Evite introduzir quaisquer efeitos colaterais ou assinaturas no construtor. Para esses casos de uso, use `componentDidMount()`em vez disso.

### Observação

**Evite copiar adereços no estado! Este é um erro comum:**

```jsx
constructor(props) {
 super(props);
 // Não faça isso!
 this.state = { color: props.color };
}
```

O problema é que é desnecessário (você pode usar `this.props.color`diretamente) e cria bugs (atualizações no `color`prop não serão refletidas no estado).

**Use este padrão apenas se você quiser ignorar intencionalmente as atualizações de prop.** Nesse caso, faz sentido renomear o prop a ser chamado `initialColor`ou `defaultColor`. Você pode então forçar um componente a “redefinir” seu estado interno alterando-o `key` quando necessário.