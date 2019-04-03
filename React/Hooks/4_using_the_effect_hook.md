# [Using the Effect Hook – React](https://reactjs.org/docs/hooks-effect.html)

* Data fetching, setting up a subscription, and manually changing the DOM in React components are all examples of side effects.

* If you’re familiar with React class lifecycle methods, you can think of `useEffect` Hook as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` combined.

* In React class components, the render method itself shouldn’t cause side effects. We put side effects into `componentDidMount` and `componentDidUpdate`.

* We have to duplicate the code between these two lifecycle methods in class.

* **What does `useEffect` do?** By using this Hook, you tell React that your component needs to do something after render. React will remember the function you passed (we’ll refer to it as our “effect”), and call it later after performing the DOM updates.

* **Why is `useEffect` called inside a component?** Hooks embrace JavaScript closures and avoid introducing React-specific APIs where JavaScript already provides a solution.

* **Does `useEffect` run after every render?** Yes! By default, it runs both after the first render and after every update.

* Instead of thinking in terms of “mounting” and “updating”, you might find it easier to think that effects happen “after render”. React guarantees the DOM has been updated by the time it runs the effects.

* Unlike `componentDidMount` or `componentDidUpdate`, effects scheduled with `useEffect` don’t block the browser from updating the screen.

* In the uncommon cases where they do (such as measuring the layout), there is a separate `useLayoutEffect` Hook with an API identical to useEffect.

* In a React class, you would typically set up a subscription in `componentDidMount`, and clean it up in `componentWillUnmount`.

* **Why did we return a function from our effect?** This is the optional cleanup mechanism for effects. Every effect may return a function that cleans up after it. This lets us keep the logic for adding and removing subscriptions close to each other. They’re part of the same effect!

* **When exactly does React clean up an effect?** React performs the cleanup when the component unmounts. However, as we learned earlier, effects run for every render and not just once. This is why React also cleans up effects from the previous render before running the effects next time.

**Tips for Using Effects**

* **Tip: Use Multiple Effects to Separate Concerns**

* Just like you can use the State Hook more than once, you can also use several effects. This lets us separate unrelated logic into different effects.

```jsx
    function FriendStatusWithCounter(props) {
    const [count, setCount] = useState(0);
    useEffect(() => {
        document.title = `You clicked ${count} times`;
    });

    const [isOnline, setIsOnline] = useState(null);
    useEffect(() => {
        function handleStatusChange(status) {
        setIsOnline(status.isOnline);
        }

        ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
        return () => {
        ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
        };
    });
    // ...
    }
```

* Hooks lets us split the code based on what it is doing rather than a lifecycle method name. React will apply every effect used by the component, in the order they were specified.

* **Tip: Optimizing Performance by Skipping Effects**

* You can tell React to skip applying an effect if certain values haven’t changed between re-renders. To do so, pass an array as an optional second argument to useEffect.

```jsx
    useEffect(() => {
    document.title = `You clicked ${count} times`;
    }, [count]); // Only re-run the effect if count changes
```

* All items in the array are the same.

* If you use this optimization, make sure the array includes all values from the component scope (such as props and state) that change over time and that are used by the effect.

* If you want to run an effect and clean it up only once (on mount and unmount), you can pass an empty array ([]) as a second argument.

* We recommend using the `exhaustive-deps` rule as part of our `eslint-plugin-react-hooks` package. It warns when dependencies are specified incorrectly and suggests a fix.
