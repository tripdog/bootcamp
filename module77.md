# React Components and State Management #77

## Introduction to Components
A component is a chunk of an interface. For example, a typical blog usually has a sidebar component and the **blog posts list** component. They are both comprised of other components. 

![](https://i.imgur.com/QHVwEeZ.png)

In react, everything is a component and there are 2 ways to define a component:
1. A function based component

```
const BlogPostExcerpt = () => {
return (
    <div>
      <h1>Title</h1>
      <p>Description</p>
    </div>
    )
}
```
