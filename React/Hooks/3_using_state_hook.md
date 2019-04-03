# [Using the State Hook – React](https://reactjs.org/docs/hooks-state.html)

* Hooks don’t work inside classes. But you can use them **instead** of writing classes.

* **What is a Hook?** A Hook is a special function that lets you “hook into” React features. For example, useState is a Hook that lets you add React state to function components. We’ll learn other Hooks later.

* **When would I use a Hook?** If you write a function component and realize you need to add some state to it, previously you had to convert it to a class. Now you can use a Hook inside the existing function component

* **What does calling useState do?** It declares a “state variable”. Our variable is called count but we could call it anything else, like banana. This is a way to “preserve” some values between the function calls — useState is a new way to use the exact same capabilities that this.state provides in a class. Normally, variables “disappear” when the function exits but state variables are preserved by React.

* **What do we pass to `useState` as an argument?** The only argument to the useState() Hook is the initial state. Unlike with classes, the state doesn’t have to be an object. We can keep a number or a string if that’s all we need

* **What does useState return?** It returns a pair of values: the current state and a function that updates it. This is why we write const `[count, setCount] = useState()`

**Reading State**

* When we want to display the current count in a class, we read this.state.count
```jsx
    <p>You clicked {this.state.count} times</p>
```
* In a function, we can use count directly
```jsx
    <p>You clicked {count} times</p>
```

**Updating State**

* In a class, we need to call this.setState() to update the count state
```jsx
    <button onClick={() => this.setState({ count: this.state.count + 1 })}>
        Click me
    </button>
```

* In a function, we already have setCount and count as variables so we don’t need this

```jsx
    <button onClick={() => setCount(count + 1)}>
        Click me
    </button>
```