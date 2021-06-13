# React Components and State Management #77

[![hackmd-github-sync-badge](https://hackmd.io/x3AjBTD7STKrg7uZQkL9dA/badge)](https://hackmd.io/x3AjBTD7STKrg7uZQkL9dA)


## Introduction to Components
A component is a chunk of an interface. For example, a typical blog usually has a sidebar component and the **blog posts list** component. They are both comprised of other components. 

![](https://i.imgur.com/QHVwEeZ.png)

In react, everything is a component and there are 2 ways to define a component:
1. A function based component

```{r, attr.source='.numberLines'}javascript
const BlogPostExcerpt = () => {
return (
    <div>
      <h1>Title</h1>
      <p>Description</p>
    </div>
    )
}
```
2. A class-based component

```jsx=
import React, { Component } from "react"

class BlogPostExerpt extends Component {
render(){
    return(
      <div>
        <h1>Title</h1>
        <p>Description</p>
      </div>
    )
  }
}
```
Function and class-based components differ in two ways according to how they're managed. 
**Class-based components are outdated, but it's still a good idea to know how class-based components work.**

---

## Component Props
Props = properties. It's how components get their properties. Starting with the parents at the top, children components inherit properties from the parents. 

With function components, properties are all that is passed, all you have to do is add the props as the argument to the function.

```jsx=
const BlogPostExcerpt = props => {
  return (
    <div>
      <h1>{props.title}</h1>
      <p>{props.description}</p>
    </div>
  )
}
```
🟢 A component either holds data (has state) or receives data through it's props.

---


### :warning: It gets complicated when:

🟠 You need to access the state of a component form a child that's several levels down. All of the previous children act as a pass-through, even if knowing the state is not necessary.

🟠 You need to access the state of a component from a completely unrelated component.

When intializing a component, we pass the props in a way that resembles HTML attributes:

```jsx=
const desc = 'A description'
//
<BlogPostExcerpt title="A blog post" description={ desc } />
```
In the above example a plain string is passed as the title and the description as a variable.(Only strings can be passed in this way)

---

## Children

A specil kind of prop are children. They contain the value of anything that's passed through the component. Consider this snippet:

```jsx=
<BlogPostExcerpt title="A blog post" description="{ desc }">Something, blah blah.</BlogPostExcerpt>
```
Here, inside BlogPostExcerpt we can access "Something, something else." by looking up props.children.

So "Something..." is the child property of the component(props.children)

While Props allow a component to receive properties from its parent with instructions to "print" some data, state allows a component to take on life itself, operating independently from the surrounding environment.

---
## State Management, state control. 
The state is the data set that is managed by the component. Much like a form, each input is responsible for managing its own state, i.e. **what is inside of the input.**

Another example is a button. Is it clicked or not? Is it on focus? A link has states too, how does it behave on a hover?

In React or any other component based framework or library, all of them require and use the concept of the 'state' of components.

**Important:**

:zap: We manage state in react by using **hooks.** The first hook we learn is the **useState.**

Import it from React like so:
```jsx=
import React, { useState } from 'react'
```
:bulb: **useState is an API** we use it to create a new state variable and once that is done, we have a way to alter it.
* useState() accepts the inital state value 
    * It then returns an array containing the state variable, and the function you call the alter the state. Use descrurcturing to access each individual item, like this: 


```jsx=
const [count, setCount] = useState(0)
```
Here's a more practical example:
```jsx=
import { useState} from 'react'

const Counter = () => {
const [count, setCount] = useState(0)

return (
<div>
  <p>You clicked {count} times.</p>
  <button onClick={() => setCount(count +1)}>Click me</button></div>
  )
}
```
* You can use as many useState( ) calls to create state variables as are needed.
    * Just remember to call it at the **top level** of the component state, not inside of an if or other kind of block.

---
## Moving the state up through the tree

🟢 State is always owned by one component. Any data that's affected by this state can only affect components below it: children.

🟢 Changing the state on a component will never affect the parent, siblings or other component in the app, just the children.

🟢 Because of the 'Unidirectional Data Flow rule', if two components need to share a state, that state muse be moved up to a common ancestor.

🟢 Often the colsest ancestor is the best place to mangage the state, but it's not a rule. It depends upon the situation.

**The state is passed down to the components that need that value via properties (props)**

---
## State vs Props

In a React component, props are variables passed to it by its parent component. **State** on the other hand is still variables, but directly initialized and managed by the component. 

The state can be initialized by the props. For example, a parent component might include a child component by calling:
```jsx=
<childComponent />
```
The parent can pass a prop by using this syntax:
```jsx=
<ChildComponent color=green />
```
Inside the ChildComponent constructor we could access the prop:
```jsx=
class ChildComponent = props => {
console.log(props.color)
}
```
Props should never be changed in a child component, so if there's something going on that alters some variable, that variable needs to belong to the component state.

Props are also used to allow child components to access methods defined in the parent component. This is a good way to centralize managing the state in the parent component, and avoid the need for children to have their own state.

Most of your components will just display some kind of information based on the props they receive and stat **stateless.**

---
## Component initialization and unmounting
The useEffect hook allows us to run specific code when the component is mounted or re-rendered. Consider the following snippet:
```jsx=
useEffect(()=>{
//your code
}, [])
```
When you call the hook, pass it to a function. The function will be run by React when the component is first rendered, and on every subsequent re-render/update.

For example, we can call a getData() function we have defined in the component to fetch some data every time the component is rendered. Example:

```jsx=
useEffect(()=>{
getData()
})
```
In this case, the getData( ) function is executed everytime the component is re-rendered, which is what happens when the props change.

You can add a second parameter to useEffect, an array, which says, "only run the function if the variables in the array are changed."

if you pass an empty array, the function will only be executed the first time the component is mounted, and not when the props change.
```jsx=
useEffect(()=>{
getData()
}, [])
```
This is useful for one-time initialization, **like fetching data from an API**

We can add into that array a list of variables, and the function will be run when the component is added to the page first, and when any of those variables change.
```jsx=
let name, address

useEffect(()=>{
getData()
},[name, address])
```
This lets us optimize our data fetching, because we perform something only when those variables change.

useEffect( )will be very useful in your React projects.
