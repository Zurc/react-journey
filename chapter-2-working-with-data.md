## Chapter 2 - working with data

First decision: your app components architecture, structure. Things like how many components to use and what each component should describe.

So, let's create an app using real data from github api \(api.github.com\)

Let's create a Card component to display that info... \(you can test on the go with jscomplete\)

As there will be no interaction or state \(at the moment\) with this component, so make sense to create it as a function component

```
const Card = function(props) {
    return (
      <div>
        <img src="http://placehold.it/75" />
      <div>
        <div>Name: ...</div>
        <div>Company Name: ...</div>
      </div>
      </div>
  );
}

ReactDOM.render(<Card />, mountNode);
```

So that returns something like this...

![](/assets/Screen Shot 2017-10-11 at 12.09.27.png)

Let's style that, there is a couple of options to style a component with react:

* Include a stylesheet file with your classes and add a class attribute to your element

```
<div className="info">
```

we use className as it is the javascript api using it

then we style our class 'info' on the css

```
.info {
  color: red;
```

* Use a style \(react property\) to add javascript code on it \[use de JS api for styles\]

```
<div style={{display: 'inline-block'; marginLeft: 10px;}}>
```

So, after adding some styles our card could look something like this:

```
const Card = function(props) {
    return (
      <div style={{margin: '1em'}}>
        <img src="http://placehold.it/75" />
      <div style={{display: 'inline-block', marginLeft: 10}}>
        <div style={{fontSize: '1.25em', fontWeight: 'bold'}}>Name: ...</div>
        <div>Company Name: ...</div>
      </div>
      </div>
  );
}
```

Let's create another component 'CardList' that will hold our list of cards

```
const CardList = (props) => {
    return (
      <div>
        <Card />
      </div>
  );
}
```

Now try using real data. go to github api users, copy the avatar url, name... etc and replace on your code

That will give you an idea on how the card will look like

At this stage, if we pass multiple Card comps to our CardList comp they will all display the same content

so, to fix that we pass the info as props into each card

This makes the Card component reusable, however, still we are hardcoding the values into each card.

we want to add them dynamically, so \(for the moment\) we will add them as an array of objects 'data' where every object represent the data for each card

```
let card = [
  { name: '...', ... }, {...}
]
```

we want the CardList comp to render a card for each component on the array, so we pass this data as a prop

```
 ReactDOM.render(<Card card={data}/>, mountNode);
```

Inside de CardList component we can get the data as props.data and we can map each card to display the Card component

Because every Card comp renders data through its props so we want to pass the data as it is from the array data

Using the spread operator we avoid the necessity of writing each prop \( name={card.name} ... \)

```
const CardList = (props) => {
    return (
      <div>
        {props.cards.map(card => <Card {...card}/>)}
      </div>
  );
}
```

Let's create a new 'Form' component with an input and a button...

```
class CardForm extends React.Component {
  render() {
    return (
        <form>
          <input type="text" placeholder="github username"/>
          <button type="submit">Add card</button>
        </form>
    );
  }
}
```

In order to make it work we could add the &lt;Form /&gt; component inside the card and that should work... but that's not entirely right... because the form shouldn't be part of the Card component

To fix this we create a parent App component which will include both...

```
class App extends React.Component {
    render() {
      return (
        <div>
          <CardForm />
        <CardList cards={data}/>
        </div>
    );
  }
}
```

and we pass that to the render function for ReactDOM

```
ReactDOM.render(<App />, mountNode);
```

The data array is still a global array, which is bad, it should be part of the app itself to make the whole app reusable, otherwise, multiple instances of the App component will use the same global data. We can maintain the data inside the instance property of the app component or  we can use react internal state object

we want our app to re-render our app every time a new record is added we need to put it on the state component, so we only need to add a record to this data array and automatically it will render

To allow both the Form and the CardList to access to that state we will put the array on the state of the parent component App

We will rename data as 'cards' array

```
class App extends React.Component {
  state = {
    cards: [
    { name: "Cruz",
          avatarUrl: "https://avatars2.githubusercontent.com/u/3543715?v=4",
          companyName: "Open Energi"},
        { name: "John",
          avatarUrl: "https://avatars1.githubusercontent.com/u/1668?v=4",
          companyName: "Wordie"},
        { name: "Jack",
          avatarUrl: "https://avatars1.githubusercontent.com/u/3663558?v=4",
          companyName: "Jack's own"}
     ]
```

in order to use this inside our CardList component we will use this.state.cards







So, we have this code for the moment...

```
const Card = function(props) {
	return (
  	<div style={{margin: '1em'}}>
  	  <img width="75" src={props.avatarUrl} />
      <div style={{display: 'inline-block', marginLeft: 10}}>
        <div style={{fontSize: '1.25em', fontWeight: 'bold'}}>{props.name}</div>
        <div>{props.companyName}</div>
      </div>
  	</div>
  );
}

let data = [
	{ name: "jack",
  	avatarUrl: "https://avatars1.githubusercontent.com/u/3663558?v=4",
    companyName: "Jack's own"
  },
  { name: "jack",
  	avatarUrl: "https://avatars1.githubusercontent.com/u/3663558?v=4",
    companyName: "Jack's own"
  }
]

const CardList = (props) => {
	return (
		<div>
			{props.cards.map(card => <Card {...card}/>)}
		</div>
	);
}

class CardForm extends React.Component {
	render() {
		return (
			<form>
				<input type="text" placeholder="github username"/>
				<button type="submit">Add card</button>
			</form>
		);
	
  }
}

class App extends React.Component {
  state = {
    cards: [
      { name: "Cruz",
      avatarUrl: "https://avatars2.githubusercontent.com/u/3543715?v=4",
      companyName: "Open Energi"},
      { name: "John",
      avatarUrl: "https://avatars1.githubusercontent.com/u/1668?v=4",
      companyName: "Wordie"},
      { name: "Jack",
      avatarUrl: "https://avatars1.githubusercontent.com/u/3663558?v=4",
      companyName: "Jack's own"}
    ]
  }
	render() {
		return (
			<div>
				<CardForm />
				<CardList cards={this.state.cards}/>
			</div>
		);
	}
}

ReactDOM.render(<App />, mountNode);
```



