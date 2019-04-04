# [Hooks - FAQ](https://reactjs.org/docs/hooks-faq.html)

**Are Hooks slow because of creating functions in render?**
* No. In modern browsers, the raw performance of closures compared to classes doesn’t differ significantly except in extreme scenarios.

* In addition, consider that the design of Hooks is more efficient in a couple ways:

    * Hooks avoid a lot of the overhead that classes require, like the cost of creating class instances and binding event handlers in the constructor.

    * Idiomatic code using Hooks doesn’t need the deep component tree nesting that is prevalent in codebases that use higher-order components, render props, and context. With smaller component trees, React has less work to do.

* Traditionally, performance concerns around inline functions in React have been related to how passing new callbacks on each render breaks shouldComponentUpdate optimizations in child components. Hooks approach this problem from three sides.

    * The useCallback Hook lets you keep the same callback reference between re-renders so that shouldComponentUpdate continues to work:

```jsx
// Will not change unless `a` or `b` changes
const memoizedCallback = useCallback(() => {
    doSomething(a, b);
}, [a, b]);
```

* The useMemo Hook makes it easier to control when individual children update, reducing the need for pure components.

* Finally, the useReducer Hook reduces the need to pass callbacks deeply, as explained below.