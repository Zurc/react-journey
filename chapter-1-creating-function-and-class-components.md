## Chapter 1 - creating function and class components

Function comps: Sometimes this have different names, like presentational components, dumb componentes

Class comps: other names... container components, smart components... etc



You can read the creator of Redux \([Dan Abramov](https://medium.com/@dan_abramov?source=post_header_lockup)\) talking about this [here](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)

You can try this code on [jscomplete/repl](https://jscomplete.com/repl)

```
// class comps can be defined by extending the React.Component class 
// and defining a render function inside of that.
// the render function returns the react element

class Button extends React.Component {

  handleClick = () => {
    	counter: this.props.onClickFunction(this.props.incrementValue)
  }
  
  render() {
    return (
      <button onClick={this.handleClick}>
      	+{this.props.incrementValue}
      </button>
    )	
  };
}

// function comps can be defined with simple functions that receive a props obj and returns a react elem
const Result = (props) => {
  return (
    <div>{props.counter}</div>
  )
}

class App extends React.Component {
  state = { counter : 0 }
  
  incrementCounter = (incrementValue) => {
    this.setState((prevState) => ({
      counter: prevState.counter + incrementValue
    }));
  }
  
  render() {
    return (
      <div>
        <Button incrementValue={1} onClickFunction={this.incrementCounter}/>
        <Button incrementValue={5} onClickFunction={this.incrementCounter}/>
        <Button incrementValue={10} onClickFunction={this.incrementCounter}/>
        <Button incrementValue={100} onClickFunction={this.incrementCounter}/>
        <Result counter={this.state.counter}/>
      </div>
    );
  }
}

// syntax to mount a react component in the browser
ReactDOM.render(<App />, mountNode);
```








