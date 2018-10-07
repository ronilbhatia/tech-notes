# React

### Lifecycle methods

* `componentWillReceiveProps` is used to fetch information from API endpoint when a component receives new props so that the page is appropriately updated. The reason it is necessary to fetch the new information in this lifecycle method, is because the component does not unmount when its props change. Therefore if a user navigates from '/posts/2' to '/posts/4' the component remains mounted throughout, and will only render correctly if the post information is re-fetched in `componentWillReceiveProps` for the new post. 
