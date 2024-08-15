# React Notes
## React Basics - Hooks, ReactDOM, More state management
###### Written @ 2024.aug.16 by [Viktor Synek](https://github.com/viktorsynek)

## Hooks

- Hooks are essentially functions that start with ``use`` for example: ``useState()`` or ``useEffect()`` these are built-in Hooks, which are built-in in the React API.

- You can also write your own Hooks, by combining the existing ones - we store these at ``/src/hooks/`` and use them inside of our components.

- We will talk about built-in hooks later such as: ``useEffect()``

## Sharing data between components

In the last guide, we already learnt how we can store dynamic data, which we store using states, but these are only but they don't share between components, so how do we fix that?

Well we simply move the state from the component, "upwards" to the component you want to store them. In our case this would be the App.

So instead of having MyButton handle the state management, we will do this inside of our App:

```javascript
function MyButton() {
    // ... we're moving code from here ...
}


export default function MyApp() {
    // ... To here ...
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <MyButton />
      <MyButton />
    </div>
  );
}
```

Then pass the state to each ``MyButton`` component:

```javascript
export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update together</h1>
      <MyButton count={count} onClick={handleClick} />
      <MyButton count={count} onClick={handleClick} />
    </div>
  );
}
```

The information you pass down like this is called *props*. Now the MyApp component contains the ``count`` state and the ``handleClick`` event handler, and passes both of them down as **props** to each of the buttons.

For this we also have to change our ``MyButton`` component so it has the necessary parameters, like so:

```javascript
function MyButton({ count, onClick }) {
  return (
    <button onClick={onClick}>
      Clicked {count} times
    </button>
  );
}
```

When you click the button, the ``onClick`` handler fires. Each button’s onClick prop was set to the ``handleClick`` function inside MyApp, so the code inside of it runs. That code calls ``setCount(count + 1)``, incrementing the ``count`` state variable. The new ``count`` value is passed as a prop to each button, so they all show the new value. This is called **“lifting state up”**.

## ReactDOM

- Before starting with the ReactDOM, first let's discuss what DOM in general means in web development.

- The *DOM* is an Object Model for HTML, it provides structure for HTML and XML document.

- The *DOM* is an API (Programming Interface) for JavaScript, it can manage HTML elements, etc.

###### DOM Image Reference
[!dom](https://www.w3schools.com/whatis/img_htmltree.gif)

#### Okay, so what is ReactDOM?

ReactDOM is a package in React that provides DOM-specific methods that can be used at the top level of a web app to enable an efficient way of managing DOM elements of the web page. ReactDOM provides the developers with an [API Reference](https://react.dev/reference/react-dom) containing the various methods to manipulate DOM. 

#### Why ReactDOM is used ?

Earlier, React Developers directly manipulated the DOM elements which resulted in frequent DOM manipulation, and each time an update was made the browser had to recalculate and repaint the whole view according to the particular CSS of the page, which made the total process to consume a lot of time.

#### Virtual DOM

To solve this issue, React brought into the scene the virtual DOM. The Virtual DOM can be referred to as a copy of the actual DOM representation that is used to hold the updates made by the user and finally reflect it over to the original Browser DOM at once consuming much lesser time.

``render()`` - This is one of the most important methods of ReactDOM. This function is used to render a single React Component or several Components wrapped together in a Component or a div element. 


