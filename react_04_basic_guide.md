# React Notes
## React Basics - React Router
###### Written @ 2024.aug.17 by [Viktor Synek](https://github.com/viktorsynek)

## Client Routes

For our last basic guide, I left the *React Router* as our main topic.

By default, the ``create-react-app`` doesn't include page routing.

So the most commonly used method is: **React Router**.

**React Router:** is fast, optimized, and the implementation is not difficult.

For this we will need the ``react-router-dom`` package to be installed via ``npm``.

In this tutorial let's imagine that I'm using ``App.js`` to store the routes, which is where people store in most cases.

Here is an example route setup:

```javascript
import { BrowserRouter, Routes, Route } from "react-router-dom"; // import necessary components from the package
// some people like to use Router instead of BrowserRouter, so you might also see it like this:
import {BrowserRourter as Router, Routes, Route} from "react-router-dom";
// in this case we would need to import the Components we want to show for each route:
import Home from "./pages/Home";
import Blogs from "./pages/Blogs";
import Contact from "./pages/Contact";
import NotFound from "./pages/NotFound";


export default function App() {
  return (
    // Every Route has to be inside a <Routes> element, and the <Routes> element has to be inside <Router> or in this case <BrowserRouter>
    <BrowserRouter>
      <Routes>
          <Route path="/" element={<Home />}> // The default route will load the Home component
          <Route path="home" element={<Home />}> // /home will load the Home component
          <Route path="blogs" element={<Blogs />} /> // /blogs will load the Blogs component
          <Route path="contact" element={<Contact />} /> // /contact will load the Contact component
          <Route path="*" element={<NotFound />} /> // Any other route for example: /login will load the 404 notfound error component
        </Route>
      </Routes>
    </BrowserRouter>
  );
}
```

## Link

React also does not have a support for ``<a>`` (anchor) elements, which are used for page / url linking.

For this, we use the same package ``react-router-dom``. And use the ``Link`` component.

Example code of ``Link`` usage (Navbar):

```javascript
import {Link} from "react-router-dom"; // import Link from react-router-dom

import '../css/navbar.css' // import navbar styling if needed 

const Navbar = () => {
  return (
    <>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/blogs">Blogs</Link>
          </li>
          <li>
            <Link to="/contact">Contact</Link>
          </li>
        </ul>
      </nav>
    </>
  );
};

export default = Navbar;
```
