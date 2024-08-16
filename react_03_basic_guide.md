# React Notes
## React Basics - Component Lifecycle, useEffect, Forms
###### Written @ 2024.aug.16 by [Viktor Synek](https://github.com/viktorsynek)

## Component Lifecycle

- In React, components have a lifecycle that consists of different phases. Each phase has a set of lifecycle methods that are called at specific points in the component's lifecycle. These methods allow you to control the component's behavior and perform specific actions at different stages of its lifecycle.

- A component's lifecycle has three main phases: the Mounting Phase, the Updating Phase, and the Unmounting Phase. 

### Mounting Phase

- The mounting phase refers to the period, when a component gets created by the DOM.

- During this phase, several lifecycle methods are invoked by React, which allows the developers to configure the component - this involves event listeners, and other initialization tasks.

Let's mention some lifecycle methods, that occur during the ``Moutning phase``.

##### The ``constructor()`` lifecycle method

The ``constructor()`` lifecycle gets called, when the component is created. You use it to initialize the component's state and bind methods to the component's instance.

Example code:

```javascript
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
    this.handleClick = this.handleClick.bind(this);
  }
```

In this example, the ``constructor()`` method sets the initial state of the component to an object with a count property set to ``0``, and binds the ``handleClick`` method to the component's instance.

[NOTE:Tthe constructor is the only place where you should directly assign state using ``this.state = {...}`` rather than using ``this.setState()``]

##### The ``render()`` lifecycle method

The ``render()`` method is responsible for generating the component's virtual DOM representation based on its current props and state. It is called every time the component needs to be re-rendered, either because its props or state have changed

Example code:

```javascript
render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    );
  }
}
```

In this example, the ``render()`` method displays the current ``count`` value and a button. When the button is clicked, the ``handleClick`` method is invoked. This triggers a state update, causing a re-render, and the updated ``count`` is displayed.

##### The ``componentDidMount()`` lifecycle method

The ``componentDidMount()`` method is called once the component has been mounted into the DOM. It is typically used to set up any necessary event listeners or timers, perform any necessary API calls or data fetching, and perform other initialization tasks that require access to the browser's DOM API. 

Example code:

```javascript
constructor(props) {
    super(props);
    this.state = {favoritefood: "rice"};
}

componentDidMount() {
    setTimeout(() => {
      this.setState({favoritefood: "pizza"})
    }, 1000)
}

render() {
    return (
      <h1>My Favorite Food is {this.state.favoritefood}</h1>
    );
}
```

- In this example, we used ``constructor()`` to initialize the value of favoritefood to "rice".

- With the help of the ``render()`` method it gets rendered showing a Header1 element saying ```My Favorite Food is rice```

- Then after 1sec the favoritefood's state value changes to "pizza" via ``componentDidMount()``. 

- And the ``render()`` method re-renders the h1 element, which now will say ```My Favorite Food is pizza```

[NOTE: Keep in mind, without the setTimeout, the value of favoritefood would've been pizza right after it is mounted into the DOM.]

### Updating Phase

- This phase occurs when a component's props or state changes, and the component needs to be updated in the DOM.

##### The ``componentWillUpdate()`` lifecycle method

The ``componentWillUpdate()`` is a lifecycle method in React that gets called just before a component's update cycle starts. It receives the next prop and state as arguments and allows you to perform any necessary actions before the component updates. 

But this method is not recommended for updating the state, as it can cause an infinite loop of rendering. It is primarily used for tasks such as making API calls, updating the DOM, or preparing the component to receive new data.

##### The ``componentDidUpdate()`` lifecycle method

The ``componentDidUpdate()`` method is a lifecycle method in React that is called after a component has been updated and re-rendered. It is useful for performing side effects or additional operations when the component's props or state have changed.


### Unmounting Phase

- The unmounting phase refers to the lifecycle stage when a component is being removed from the DOM (Document Object Model) and is no longer rendered or accessible.

- During this phase, React performs a series of cleanup operations to ensure that the component and its associated resources are properly disposed of.

- The unmounting phase is the last stage in the lifecycle of a React component and occurs when the component is being removed from the DOM tree. 

##### The ``componentWillUnmount()`` lifecycle method

The ``componentWillUnmount()`` is called just before the component is removed from the DOM. It allows you to perform any necessary cleanup, such as canceling timers, removing event listeners, or clearing any data structures that were set up during the mounting phase.

After the method is called, the component is removed from the DOM and all of its state and props are destroyed.


## useEffect

So I already mentioned ``useEffect`` when we talked about hooks, so let's actually explain the basic usage of it.

useEffect is a React Hook that lets you synchronize a component with an external system. In a Full-Stack environment, the most used external system would be fetching data, which I will show later in a more advanced guide.

Here is an example of ``useEffect`` usage:

```javascript
  useEffect(() => {
    console.log(`You clicked ${count} times`);
  }, [count]);
```

So let's break it down:

- The function inside useEffect runs after the component renders (after it returns JSX) - in our case the function is ``console.log()``.

- As you can see we have a dependency array in this case: ``[count]``, it tells React when to run the effect. Specifically this effect will only run when the ``count`` variable's data changes (e.g: it's increased).

- If the dependency array is empty ``[]`` The effect will only run once after the initial render.


#### Things to avoid

- **Infinite Loops:** If you don't use correct dependency array values, or don’t manage it correctly, you could trigger an infinite loop, where the effect continually runs and updates state.

- **Stale Closures:** Always include all variables or props that the effect depends on in the dependency array. Failing to do so can cause the effect to reference outdated variables, leading to bugs.

#### Effect timing

``useEffect`` runs asynchronously and doesn't block the browser from updating the screen. This is important for keeping the UI responsive, especially for effects that might take time to complete (like data fetching).

#### Multiple useEffect hooks

You can use multiple useEffect hooks in a single component, each for different purposes. React will handle them independently, allowing you to better organize your side effects.


## Forms

Just like in HTML, React uses forms to allow users to interact with the web page.

Example of a React form:

```javascript
function MyForm() {
  return (
    <form>
      <label>Enter your name:
        <input type="text" />
      </label>
    </form>
  )
}
```

This will work as normal, the form will submit and the page will refresh. But this is generally not what we want to happen in React. We want to prevent this default behavior and let React control the form.

#### Handling Forms

- Handling forms is about how you handle the data when it changes value or gets submitted.

- In HTML, this gets handled by the DOM. In React, form data is usually handled by the components.

- When the data is handled by the components, all the data is stored in the component state. (using ``useState``)

- You can control changes by adding event handlers in the onChange attribute.

Example of a React form handle via ``useState``:

```javascript
import { useState } from 'react';
import ReactDOM from 'react-dom/client';

function MyForm() {
  const [name, setName] = useState("");

  return (
    <form>
      <label>Enter your name:
        <input
          type="text" 
          value={name}
          onChange={(e) => setName(e.target.value)}
        />
      </label>
    </form>
  )
}
```



