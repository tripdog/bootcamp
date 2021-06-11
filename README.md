# A JSX Primer Module#76 :skull:

[![hackmd-github-sync-badge](https://hackmd.io/mCh4Q1KMRdiSjC7U-xrA7w/badge)](https://hackmd.io/mCh4Q1KMRdiSjC7U-xrA7w)


Defining an H1 conataining a string looks like the below snippet. It does look like a strange combination of JavaScript and HTML, but it's actually all JS.
`const element = <h1>Hello, world!`

Expressions in JSX can easily take HTML attributes:
```
const myId = 'test'
const element = <h1 id={myId}>Hello, world!</h1> 
```


---

There are 2 things we need to be aware of. Attributes with a - dash are converted to camelCase syntax instead. And for becomes htmlFor. Examples below.

1. class becomes className (reserved word in JS)
2. for becomes htmlFor (for also reserved word in JS)


**If you want to render two siblings, they need to be wrapped into a div or any other singular container. Example below:** 

```
<div>
    <BlogPostList />
    <Sidebar />
</div>
```
Note, a browser **cannot** execute javascript files contanining JSX. Therefor it must be transpiled in order for this to happen.

---

JSX is optional because to every JSX line, a corresponding plain JS alternative is available. Here are two examples showing how they relate to each other.

**Plain JS**
```
ReactDOM.render(
  React.DOM.div(
    { id: 'test' },
    React.DOM.h1(null, 'A title'),
    React.DOM.p(null, 'A paragraph')
  ),
  document.getElementById('myapp')
)
```
**JSX**
```
ReactDOM.render(
  <div id="test">
    <h1>A title</h1>
    <p>A paragraph</p>
  </div>,
  document.getElementById('myapp')
)
```
As you can see, the JSX is quite a bit more friendly.

## HTML in JSX

Basics:
1. All tags need to be closed /.
2. Use camelCase
3. class becomes className

---
## CSS in JSX

The easiest way to add CSS to JSX is to simply use classes. 

Here's an example of how it will look when you apply classes to a bit of JSX with html syntax:
```
const Button = () => {
  return <button className="button">A button</button>
}
```
