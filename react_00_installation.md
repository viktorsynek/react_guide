# React Notes
## React Project Installation
###### Written @ 2024.aug.23 by [Viktor Synek](https://github.com/viktorsynek)

## Pre-Installation

Before we setup our project, you gotta have [Node](https://nodejs.org/en) installed.

Node comes with a package manager known as: ``npm`` (Node Package Manager)

We use ``npm`` to install package dependencies.

## React project setup

Node also comes with the React installation command, but first set up the project folder.

Create a folder named after your project. And inside of that you have to use 

- a.) your terminal

- b.) your git bash

- c.) an IDE that comes with a terminal, such as VS Code

In the terminal type the command ``npx create-react-app my-app`` - Replace ``my-app``, with your project name, or something like ``client``, or ``front-end``.

__NOTE:__ if you have troubles with running the npx command, run this command first: ``npm install -g create-react-app``.

## Post-Installation

React installation comes with some unit testing components, that you can remove, if you don't wanna do unit tests.

Navigate into your ``src`` folder, and delete the following:

- App.test.js 
- reportWebVitals.js 
- setupTests.js

Then open up ``index.js`` and remove line 5, and 17. - If you deleted reportVitals, otherwise you'd get errors.

After deletion, ``index.js`` should look like this:

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

You can also remove the ``logo.svg`` file, as this is only for the basic react app, and you will not need this at all.

Then open up ``App.js`` and remove the first line, and you can also remove everything inside ``return`` and replace it with something like 
```html 
<h1>hello world</h1>
```

So ``App.js`` should look like the following:

```javascript
import './App.css';

function App() {
  return (
    <>
        <h1>hello world</h1>
    </>
  );
}

export default App;
```


### That's pretty much it, hope I could help, if you're stuck throughout the process, you can hit me up on twitter or smth
