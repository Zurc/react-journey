## Chapter 1 - creating function and class components

#### Functional components

Sometimes this have different names, like presentational components, dumb componentes

#### Class Components

Class comps: other names... container components, smart components... etc

Every single class in react needs **at least one method: render() {}** which determines what HTML/DOM elem renders out to the page. We need to import the render method from react-dom for that

```javascript
import { Render } from 'react-dom';
```

We need to touch the real DOM **at least once** to mount the entire app to the page

the first argument passed into render method define WHAT we want to pass (HTML or JSX component)
the second argument is WHERE, which DOM point to mount to page

```javascript
render(<h1>Hi there!</h1>, document.querySelector('...'));

//or 

render(<h1>Hi there!</h1>, document.getElementById('...'));

//or 
render(ComponentNameHere, document.querySelector('...'));
```


To create a Class component there is two main ways (they are the same, use the one you are more comfortable with), by importing React and using React.Component property...

```javascript
import React from ‘react’;

class Button extends React.Component {
  // ...code here
}
```

...or by importing the 'named property' Component and use it directly...

```javascript
import React, { Component } from ‘react’;

class NameOfTheClass extends Component {
  // ...code here
}
```



You can read the creator of Redux \([Dan Abramov](https://medium.com/@dan_abramov?source=post_header_lockup)\) talking about this [here](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)

You can try this code on [jscomplete/repl](https://jscomplete.com/repl)

```javascript
import React from ‘react’;

// **class comps** can be defined by extending the React.Component class 
// and defining a render method inside of that which returns the react element.
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

// **function comps** can be defined with simple functions that receive a props obj and returns a react elem
const Result = props => {
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









