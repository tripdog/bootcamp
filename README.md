# A JSX Primer Module#76 :rocket:

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

🟢 The easiest way to add CSS to JSX is to simply use classes. 

Here's an example of how it will look when you apply classes to a bit of JSX with html syntax:
```
const Button = () => {
  return <button className="button">A button</button>
}
```
🟢 A second method is to write the CSS inline by attaching it directly to the JSX element.

```
const Button = () => {
  return <button style={{ backgroundColor: 'yellow' }}>A button</button>
}
```
The mustache (double curly braces) signifies that we are passing in a JS object.


🟢 Yet another way is to create a variable for the style and pass it into an element like this:

```
const buttonStyle = { backgroundColor: 'yellow' }
const Button = () => {
  return <button style={buttonStyle}>A button</button>
}
```
:fire: Styles have the benefit of being local to the component, and they cannot leak to other components in other parts of the app, something that using classes and an external CSS file can’t provide.

For more advanced needs, CSS-in-JS solutions like Styled Components or Emotion are optimal.

:large_blue_diamond: [Styled Components](https://styled-components.com/)

:large_blue_diamond: [Emotion](https://emotion.sh/)

## JSX auto escapes

JSX forces automatic escapes to prevent the danger posed from cross site scripting attacks. Because of this, sometimes issues arise when using HTML entities.

In order to overcome these issues we need to move HTML entities outside the expression.
```
<p>{'&copy; 2017'}</p>
```
This doesn't work, because it's escaped.

So we take this approach to fix the issue. the entity is moved outside the expression.
```
<p>&copy; 2017</p>
```


Probably the best way, is to just look up the Unicode string and use that instead.
```
<p>{'\u00A9 2017'}</p>
```
## White space in JSX

To add white space in JSX there are 2 rules:

1.If you have a bunch of spaces between elements in the same line, it's trimmed to 1 single space.

2.Verical spaces are totally eliminated

Examples:
```
<p>
  Something
  becomes
  this
</p>
```
Becomes
```
<p>Somethingbecomesthis</p>
```
So what about when we NEED to add whitespace?
```
<p>
  Something
  {' '}becomes
  {' '}this
</p>
```
To address this we add space inside of the expression as in the above example.
Adding comments in JSX

Comments in JSX are the same as in regular Javascript //
Spread attributes

It's common to assign variables to attributes in JSX have a look at the examples below:

Instead of doing it manually:
```
<div>
  <BlogPost title={data.title} date={data.date} />
</div>
```
Use the spread operator to clone the data into your element.
```
<div>
  <BlogPost {...data} />
</div>
```
## Writing Loops in JSX

If you have a set of elements you need to loop through to generate a JSX partial, you create a loop, and then add JSX to an array.

```const elements = [] //..some array

const items = []

for (const [index, value] of elements.entries()) {
  items.push(<Element key={index} />)
}
```

When rendering JSX you can embed the items array simply by wrapping it up with curly braces:
```
const elements = ['one', 'two', 'three'];

const items = []

for (const [index, value] of elements.entries()) {
  items.push(<li key={index}>{value}</li>)
}

return (
  <div>
    {items}
  </div>
)
```
Now instead of using a for loop we can use the .map metho instead and reduce the amount of code written. It's much cleaner now.
```
const elements = ['one', 'two', 'three'];
return (
  <ul>
    {elements.map((value, index) => {
      return <li key={index}>{value}</li>
    })}
  </ul>
  ```
)

---