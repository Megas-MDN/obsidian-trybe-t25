

handleChange

handleChange = (event) => {

const { name } = event.target;

const { value } = event.target;

this.setState({ [name]: value });

};