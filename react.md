## INTRODUCTION TO REACT
​
#### Basic React Component. 
​
React is used to show content to users and handle user interactions. 
​
1. At the top of any of our JSX pages, will always import React, and the dependedcies of react that we are looking to use. 
2. We will want to have a render method in order to return something to the page. 
3. And we will want to have export the page that we have created so that it can be rendered. 
​
#### What is JSX? 
​
JSX is syntactical sugar for normal JS code. Basically, what happens is that our code which looks like HTML is converted into JavaScript, and this is what actually renders using babel. The reason we use JSX is that it is really useful when we are dealing with complex HTML. The beauty of JSX is that we can write HTML like syntax and it gets traspiled into JS for us! 
​
There are a couple more differences  between JSX and HTML. Adding in line styling uses a different syntax. Adding classes uses a different syntax. Other HTML properties that use a different syntax. We can put any valid expression indside of JSX (an expression is any valid unit of code that resolves to a value) For example, variables, functions and operations.
​
In order to embed JS expressions inside of JSX, we use curly braces. For example, 
​
​
const App = () => { 
  const message = "The App is still running";
​
  return (
      <div>
        {message}
      </div>
  );
};
​
#### Components
​
In react, a component is a function or a class, that produces HTML and handles feedback from the user through the use of event handlers. 
​
#### Functional Components
​
Functional Components are components that have been created through the use of a function. The first step to creating a functional component is to assign to it a function. For example, 
​
const Greeting = () => {
    return <p> G'day Mate!" </p>
}
​
ReactDOM.render(
    <Greeting />, 
    document.getElementbyId("root")
)
​
We wrap all our components in <>, turning it into JSX, which is then made into JS which our browser can read. 
​
#### Component Nesting 
​
If we want to render multiple components, we need a single top level component and we need to nest our components within this parent. For example, 
​
ReactDOM.render(
<div> 
    <Greeting />
    <Greeting />
    <Greeting />   
</div>
document.gertElementById("root)
);
​
With React we can abstract away JSX components into other JSX components. This helps us manage our code. For example, we can create our JSX component which holds all the other components of our application. 
​
const Greeting = () => {
    return <p> G'day Mate!" </p>
}
​
const App = () => { 
    return (
    <div>
        <Greeting />
        <Greeting />
        <Greeting />
    </div>
    )'
}
​
ReactDOM.render(
    <App />, 
    document.getElementById("root")
)
​
Here we are only passing a single component into our render method. This is much noicer that manually rendering every single element.
​
## JSX DEEP DIVE AND CONDITIONAL RENDERING 