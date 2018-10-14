# React

### General

* **React elements** are the HTML tags created using JSX such as `<MyComponent />` or `<div />`
* **Arrays and Fragments** help you return multiple elements from render (don't need one root element)
* **Portals** let you render children into a different DOM subtree
* If you don't initialize state and you don't bind methods, you don't need to implement a constructor for your React component.

### Lifecycle methods

* `componentWillReceiveProps` is used to fetch information from API endpoint when a component receives new props so that the page is appropriately updated. The reason it is necessary to fetch the new information in this lifecycle method, is because the component does not unmount when its props change. Therefore if a user navigates from '/posts/2' to '/posts/4' the component remains mounted throughout, and will only render correctly if the post information is re-fetched in `componentWillReceiveProps` for the new post.
  * `componentWillReceiveProps` is now considered outdated - instead use `componentDidUpdate` which takes in `prevProps`, and compare to new props to determine whether component should update
* order of methods when component is created and inserted into the DOM
  * `constructor()`
  * `static getDerivedStateFromProps()`
  * `render()`
  * `componentDidMount()`

  *Note - `componentWillUnmount` is deprecated and no longer considered safe to use*
* order of methods when component is updating
  * `static getDerivedStateFromProps()`
  * `shouldComponentUpdate()`
    * defaults to true - used for optimization to prevent unnecessary re-renders
  * `render()`
  * `getSnapshotBeforeUpdate()`
  * `componentDidUpdate()` (*Note - this method is NOT called during initial render)*
    * will not be invoked if `shouldComponentUpdate()` returns false - however `shouldComponentUpdate()` defaults to true

  *Note - `componentWillUpdate()` and `componentWillReceiveProps()` are deprecated and no longer considered safe to use*

* `componentWillUnmount()` called when component is being removed from the DOM
* `componentDidCatch()` is called if there is an error during rendering, in a lifecycle method, or in the constructor of any child component
