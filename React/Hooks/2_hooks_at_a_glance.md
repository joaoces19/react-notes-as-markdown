# [Hooks at a Glance – React](https://reactjs.org/docs/hooks-overview.html)

* We call it inside a function component to add some local state to it. React will preserve this state between re-renders. `useState` returns a pair: the current state value and a function that lets you update it.

```jsx
  import React, { useState, useEffect } from 'react';

  function Example() {
    const [count, setCount] = useState(0);

    // Similar to componentDidMount and componentDidUpdate:
    useEffect(() => {
      // Update the document title using the browser API
      document.title = `You clicked ${count} times`;
    });

    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
          Click me
        </button>
      </div>
    );
  }
```

* The only argument to `useState` is the initial state.

* The array destructuring syntax lets us give different names to the state variables we declared by calling `useState`.

* The Effect Hook, `useEffect`, adds the ability to perform side effects from a function component. It serves the same purpose as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`

* When you call `useEffect`, you’re telling React to run your “effect” function after flushing changes to the DOM.

* Effects may also optionally specify how to “clean up” after them by returning a function.

```jsx
  import React, { useState, useEffect } from 'react';

  function FriendStatus(props) {
    const [isOnline, setIsOnline] = useState(null);

    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    useEffect(() => {
      ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);

      return () => {
        ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
      };
    });

    if (isOnline === null) {
      return 'Loading...';
    }
    return isOnline ? 'Online' : 'Offline';
  }
```

* **Rules of Hooks** 
    * Hooks are JavaScript functions, but they impose two additional rules:  
    * Only call Hooks at the top level. Don’t call Hooks inside loops, conditions, or nested functions. Only call Hooks from React function components. 
    * Don’t call Hooks from regular JavaScript functions. (There is just one other valid place to call Hooks — your own custom Hooks. We’ll learn about them in a moment.) We provide a linter plugin to enforce these rules automatically. We understand these rules might seem limiting or confusing at first, but they are essential to making Hooks work well.

* Hooks are a way to reuse stateful logic

* Custom Hooks are more of a convention than a feature. If a function’s name starts with ”use” and it calls other Hooks, we say it is a custom Hook

```jsx
  import React, { useState, useEffect } from 'react';

  function useFriendStatus(friendID) {
    const [isOnline, setIsOnline] = useState(null);

    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    useEffect(() => {
      ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
      return () => {
        ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
      };
    });

    return isOnline;
  }
```