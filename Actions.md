
[[React]]
[[Redux]]
[[Objeto]]
[[State]]

**Ações** são objetos JavaScript simples que possuem um `type` campo. **Você pode pensar em uma ação como um evento que descreve algo que aconteceu no aplicativo** .

```jsx
// Action para Incrementar nosso contador:
const action = {
  type: 'INCREMENT_COUNTER'
};
```

Da mesma forma que projetamos a estrutura de estado com base nos requisitos do aplicativo, também devemos ser capazes de apresentar uma lista de algumas das ações que descrevem o que está acontecendo:

-   Adicionar uma nova entrada de tarefas com base no texto que o usuário digitou
-   Alternar o status concluído de uma tarefa
-   Selecione uma categoria de cor para uma tarefa
-   Excluir uma tarefa
-   Marcar todos como concluídos
-   Limpar todos os afazeres concluídos
-   Escolha um valor de filtro "concluído" diferente
-   Adicionar um novo filtro de cor
-   Remover um filtro de cor

Normalmente colocamos quaisquer dados extras necessários para descrever o que está acontecendo em `action.payload`campo. Pode ser um número, uma string ou um objeto com vários campos dentro.

A loja Redux não se importa com o texto real do `action.type`campo. No entanto, seu próprio código analisará `action.type`para ver se uma atualização é necessária. Além disso, você verá frequentemente as strings de tipo de ação na extensão Redux DevTools durante a depuração para ver o que está acontecendo em seu aplicativo. Portanto, tente escolher tipos de ação que sejam legíveis e descrevam claramente o que está acontecendo - será muito mais fácil entender as coisas quando você as analisar mais tarde!

Com base nessa lista de coisas que podem acontecer, podemos criar uma lista de ações que nosso aplicativo usará:

-   `{type: 'todos/todoAdded', payload: todoText}`
-   `{type: 'todos/todoToggled', payload: todoId}`
-   `{type: 'todos/colorSelected', payload: {todoId, color}}`
-   `{type: 'todos/todoDeleted', payload: todoId}`
-   `{type: 'todos/allCompleted'}`
-   `{type: 'todos/completedCleared'}`
-   `{type: 'filters/statusFilterChanged', payload: filterValue}`
-   `{type: 'filters/colorFilterChanged', payload: {color, changeType}}`

Nesse caso, as ações têm principalmente um único dado extra, para que possamos colocá-lo diretamente no `action.payload`campo. Poderíamos ter dividido o comportamento do filtro de cores em duas ações, uma para "adicionado" e outra para "removido", mas neste caso faremos isso como uma ação com um campo extra dentro especificamente para mostrar que podemos ter objetos como uma carga útil de ação.

Assim como os dados de estado, as **ações devem conter a menor quantidade de informações necessárias para descrever o que aconteceu** .

######: Fonte: https://redux.js.org/tutorials/fundamentals/part-3-state-actions-reducers