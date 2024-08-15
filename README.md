# React Notes 
## React Basics - Components & Syntax
###### Written @ 2024.aug.15 by [Viktor Synek](https://github.com/viktorsynek)


## Components

- Components are basically blocks of the UI, that can be as small as a button, or as big as a whole page.

- React components always start with capital letter, and you can nest components together.

```javascript
function MyButton() {
  return (
    <button>I'm a button</button>
  );
}
```

Let's nest this to your App component:

```javascript
export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```

## Syntax

- React uses the JSX syntax by default - it is stricter than HTML so for elements that are written in the following format: ``<br/>`` (self-closed tags) - are needed to be wrapped in either a ``<div>...</div>``, or an empty ``<>...</>`` wrapper

- To add class to an element, we use **className** instead of class, like in HTML.

- Rendering is straight forward, you put elements inside the return() function.

You can put more complex expressions inside the JSX curly braces too, for example:


```javascript
return (
  <h1>
    {user.name} // user obviously have to be declared beforehand 
  </h1>
);
```

## Conditional rendering

- You can use an if statement to conditionally include JSX: example code:

```javascript
let content;
if (isLoggedIn) {
  content = <AdminPanel />;
} else {
  content = <LoginForm />;
}
return (
  <div>
    {content}
  </div>
);
```

- When you don't need else branch, you can use && logical operators instead:

```javascript
<div>
  {isLoggedIn && <AdminPanel />} // In this context it basically means, if isLoggedIn true, then render AdminPanel.
</div>
```

## Rendering Lists

You can use JavaScript features like ``for`` loop or array ``map()`` function to render a list of componenets.

Let's say you have an array of products:

```javascript
const products = [
  { title: 'Cabbage', id: 1 },
  { title: 'Garlic', id: 2 },
  { title: 'Apple', id: 3 },
];
```

Inside your component, you could use ``map()`` to transform the array into ``<li>`` items, like so:

```javascript
const listItems = products.map(product =>
  <li key={product.id}>
    {product.title}
  </li>
);

return (
  <ul>{listItems}</ul>
);
```

Notice how ``<li>`` has a key attribute. For each item in a list, you should pass a string or a number that uniquely identifies that item among its siblings. Usually, a key should be coming from your data, such as a database ID.


## EventHandlers in React

Let's say you would need an alert on a button click. Using HTML and JavaScript, would require an EventListener to this, in React we just simply add a ``onClick`` attribute to our button, passing in a function, which was defined beforehand. Example:

```javascript
function MyButton() {
  function handleClick() {
    alert('You clicked me!');
  }

  return (
    <button onClick={handleClick}>
      Click me
    </button>
  );
}
```

## Updating the screen

Sometimes you want your component to be dynamically changed and displayed. Let's say we want a counter that get's increased every time we click the button. For this we could use the ``useState()`` function - we first import this from 'React':

```javascript
import {useState} from 'react';
```

Let's declare a state variable inside your component:

```javascript
const [count, setCount] = useState(0); // The default value of count is 0
```

Let's look at count as a variable, and we change the value of that variable with the ``setCount()`` function. So the whole code would look something like this:

```javascript
import {useState} from 'react';

function MyButton() {
  const [count, setCount] = useState(0); // The default value of count is 0

  function handleClick() {
    setCount(count + 1); // Increase the value by one "count += 1"
  }

  return (
    // Call the handleClick function on click
    <button onClick={handleClick}> 
            Clicked {count} times
    </button>
  );
}
```
