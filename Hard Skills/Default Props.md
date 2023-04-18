[[React]]
[[Props]]
[[PropTypes]]

A defaultProps será usada para garantir que this.props.name tenha um valor caso não tenha sido especificado pelo componente pai. A checagem de tipos de propTypes acontece após defaultProps ser resolvida, logo a checagem também será aplicada à defaultProps.

```jsx
import React, { Component } from 'react'
import PropTypes from 'prop-types';

Class UserName extends Component {
	render() {
	const name = this.props.name
	return (<span className="name">{name}</span>)
	}
}
UserName.propTypes = {
	name: propTypes.string
}

UserName.defaultProps = {
	name: 'Stranger'
}
```

**No exemplo acima definimos que a prop Name será uma string e caso ela não receba nenhum valor, o valor padrão a ser exibido será a palavra Stranger.**

