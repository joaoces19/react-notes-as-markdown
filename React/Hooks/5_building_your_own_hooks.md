
# [Building Your Own Hooks – React](https://reactjs.org/docs/hooks-custom.html)

**Extracting a Custom Hook** 

* When we want to share logic between two JavaScript functions, we extract it to a third function. Both components and Hooks are functions, so this works for them too!

* A custom Hook is a JavaScript function whose name starts with ”use” and that may call other Hooks.

* Extract some common code between two functions into a separate function. Custom Hooks are a convention that naturally follows from the design of Hooks, rather than a React feature.

* **Do I have to name my custom Hooks starting with “use”?** Please do. This convention is very important. Without it, we wouldn’t be able to automatically check for violations of rules of Hooks because we couldn’t tell if a certain function contains calls to Hooks inside of it.

* **Do two components using the same Hook share state?** No. Custom Hooks are a mechanism to reuse stateful logic (such as setting up a subscription and remembering the current value), but every time you use a custom Hook, all state and effects inside of it are fully isolated.
