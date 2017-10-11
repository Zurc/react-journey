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





