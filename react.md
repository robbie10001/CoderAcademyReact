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

The way JSX knows we are about to write JavaScript is through the use of curly brackets. In JSX, inline styling must be written as an object of key/value pairs. The key is the style and the value is the value for that style. 

const App = () => {
    const message = "The App is still running!";

    return (
        <div style=>
            {message}
        </div>
    );
};

JSX knows we are going to write JS by the use of curly brackets. In order to set a style property to a JS object, we use curly braces. The we define our object within those curly braces. JS objects also use curly braces so we get double curly brace syntax is this situation. For example, we could add many different styling attirbutes to a div as follows, 

const App = () => {
    const message = "The App is still running!";
    const styles = {
        color: "red",
        fontSize: "30px",
        backgroundColor: "black",
        border: "5px solid yellow"
    };

    return (
        <div style={styles}>
            {message}
        </div>
    );
};

In order to use CSS classes in React the proper styntax is to use className="ourclassname". For example, 

return (
    <div style={styles} className="container">
        {message}
    </div>
);

We can embed a whole lot of different Javascript within our REACT. For example, we could create a function that will render the current time. 

function getCurrentTime() {
    const current = new Date();
    return current.toTimeString();
};

const App = () => {
    const message = "The App is still running!";
    const styles = {
        color: "red",
        fontSize: "30px",
        backgroundColor: "black",
        border: "5px solid yellow"
    };

    return (
        <div style={styles} className="container">
            {message} - {getCurrentTime()}
        </div>
    );
};

Or we could embed JS expressions. 

return (
    <div style={styles} className="container">
        {message} - {getCurrentTime()}
        <p>{1 + 10}</p>
        <p>{"hey" && "you"}</p>
        <p>{"hey" || "you"}</p>
        <p>{10 > 11 ? "bigger" : "smaller"}</p>
    </div>
);

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
document.getElementById("root)
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
    );
};
​
ReactDOM.render(
    <App />, 
    document.getElementById("root")
)
​
Here we are only passing a single component into our render method. This is much noicer that manually rendering every single element.

## JSX DEEP DEIVE AND CONDITIONAL RENDERING. 

### Component Design 

We should think about component resuability. We should also think about component configuration, we should be able to configure a component when it is create and we should also think about component nesting. Our components should be able to be displayed inside of another component. 

#### How to identify and create a resuable component. 
1. Identify and blocks of JSX that seem to be duplicated. 
2. Think of a descriptive name for what that block of JSX does. 
3. Create new file with the same name that you will be giving this new component. 
4. Create the new component and paste in the duplicated JSX. 
5. Make the component configurable by use of the React props system. 
For example, 

#### Comment.js

import React from "react";
import faker from "faker";

const Comment = () => {
    return (
        <div className="comment">
            <a href="/" className="avatar">
                <img alt="avatar" src={faker.image.avatar()} />
            </a>
            <div className="content">
                <a href="/" className="author">Mary Smith</a>
                <p className="date">11/12 6:00pm</p>
                <p className="text">I think you are really cool!</p>
            </div>
        </div>
    );
};

export default Comment;

#### App.js

import React from "react";
import Comment from "./Comment";

const App = () => {
    return (
        <div className="comments">
            <Comment />
            <Comment />
            <Comment />
        </div>
    );
};

export default App;

While this is a lot better, we still have the issue of having hardcoded values, this is where we use the React props system in order to make our components truely reusable. 

### Properties (pros)

In react, props is used for passing data from a parent component to a child component. They syntax for this is exactly that same as setting the value of an attribute. Lets start with passing through the comment authors name.

#### app.js 

const App = () => {
    return (
        <div className="comments">
            <Comment author="Mary Smith" />
            <Comment author="Jude Henry" />
            <Comment author="Bob Miller" />
        </div>
    );
};

A functional child component, recieves these props through the fist argument in the function. This argument is an object that hold all of the properties that have been passed down from the parent. 

#### Commment.js 

const Comment = (props) => {
    return (
        <div className="comment">
            <a href="/" className="avatar">
                <img alt="avatar" src={faker.image.avatar()} />
            </a>
            <div className="content">
                <a href="/" className="author">{props.author}</a>
                <p className="date">11/12 6:00pm</p>
                <p className="text">I think you are really cool!</p>
            </div>
        </div>
    );
};

IN ORDER TO PASS MULTIPLE PROBS FROM THE PARENT TO THE CHILD, DEFINE MORE PROPS ON THE PARENTS! For example, 

#### app.js 

const App = () => {
    return (
        <div className="comments">
            <Comment
                author="Mary Smith"
                avatar={faker.image.avatar()}
                date={"11/12 6:00pm"}
                text={"I think you are really cool!"}
            />
            <Comment
                author="Jude Henry"
                avatar={faker.image.avatar()}
                date={"09/12 1:30pm"}
                text={"Hey this is great!"}
            />
            <Comment
                author="Bobby Miller"
                avatar={faker.image.avatar()}
                date={"07/12 9:10am"}
                text={"Simply spectacular."}
            />
        </div>
    );
};

### Custom Component Children Rendering 

Let's say we wanted to wrap each of our components into a card which we could add some styling and functionality to. In order to do this we could do the following, 

#### App.js

<Card>
    <Comment
        author="Mary Smith"
        avatar={faker.image.avatar()}
        date={"11/12 6:00pm"}
        text={"I think you are really cool!"}
    />
</Card>
Ok lets create that component:

#### Card.js

import React from "react";

const styles = {
    backgroundColor: "gray"
};

const Card = (props) => {
    return (
        <div style={styles}>
        
        </div>
    );
};

export default Card;

At the moment, this will not work. In order to do it we need to use the props system. The way we would achieve this is, 

#### Card.js

const Card = (props) => {
    return (
        <div style={styles}>
            {props.children}
        </div>
    );
};

### Conditional Rendering

Conditional rendering is when we render some content based on an expression evaluation. There are 3 different ways to conditionally render your content. 
1. use an if statement within the component itself. 
2. adding short circuit logic directly within the JSX. 
3. Through the use of a tenary operator. 