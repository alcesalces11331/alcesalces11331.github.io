---
layout: post
title:      "Hoisting, Scope, and ES6"
date:       2019-04-27 17:27:03 -0400
permalink:  hoisting_closures_and_es6
---

When beginning to seriously develop using Javascript, it is inevitable the concepts of *hoisting* and *scope* will  be grappled with. Depending on the developer's level of expertise, this can either be head-scratchingly difficult or a cool summer breeze. While the concepts themselves are simple to grasp, their full implications are affected by particular ES6 syntax. How fundamentally we understand ES6 syntax is foundational to understanding these two powerful concepts. Moreover, it is imperative to grasp a Javascript's internal execution chain to more deeply understand *hoisting* and *scope*. 
### Javascript ES6 Syntax
By now, familiarity with this syntax is second nature. What is referred to here is how variable assignment and declaration is read by Javascript. We're talking about:
```
var a = "hoisted"
let b = "hoisted"
const c = "hoisted"
d = "hoisted"
```
where the last one is a global variable. They all have differing affects upon *how* Javascript hoists them. But first, let's briefly explain each one below.

* **var**: used sparringly, this variable assigner may or may not be reassigned. 

* **let**: Utilized when the variable may need to be reassigned (think loops). Note: this assigner signals Javascript the variable will only be used in the block it's defined in -- which is not always what we want. 

* **const**: the go-to variable assigner. Once the variable is assigned with const, it cannot be reassigned. Use this by default.

* *global*: When not assigning a variable using any of the above three, the variable is assigned as a global variable and has potentially serious security implications.

* **fn()**: Functions within Javascript have their own hoisting rules. 

Furthermore, before Scope and Hoisting can be properly understood, it is necessary to explain the Javascript execution context.
### Execution Context
The Javascript execution context is the process by which Javascript code is read. First, Javascript will read through the code present in what is called the **Global Execution Context**. This step has two phases: the creation phase and the execution phase. Let's look at an example (ignore the use of *var* below, we'll get to those differences down below):
```
var name = 'Rollin'
var handle = '@rollinmetzger'

function getUser () {
  return {
    name: name,
    handle: handle
  }
}
```
In the above example, during the *Creation* phase, Javascript reads through the code allocating memory for the variables, functions, objects ... etc. At this phase the above code will read:
```
name = undefined
handle = undefined

getUser: fn()
```
All this means is it knows *name* and *handle* are variables but doesn't know what it points to. Similarly, it knows getUser() is a function but doesn't know exactly what it does. It has only allocated memory for them. Now, after the *Creation* phase, Javascript has an *Execution* phase. What does this do? It then assigns the values specified. This is when the variables *name*, *handle*, *getUser* have their associated values, i.e., when `name = 'Rollin'`. To review the **Global Execution Context** has two phases **Creation** and **Execution**. Before we continue into the other *context*, let's define one of the reasons for writing this blog post: hoisting.

#### Hoisting: [The process of assigning variable declarations a default value of *undefined* during the creation phase](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)

The idea is simple, but has implications when the code read by Javascript becomes more complex. For instance, it is time to introduce the next context Javascript executes in. The **Function Execution Context** is created when Javascript begins *executing* over the code its **hoisted** to begin the process of assignment. When Javascript gets to a function its created, it adds the function to the **Function Execution Stack**.  Now, let's define *scope*.

#### Scope: [The current context of execution. The context in which values and expressions are "visible," or can be referenced.](https://developer.mozilla.org/en-US/docs/Glossary/Scope)

What exactly does MDN mean by this defintion? It's certainly vague. To break it down, the first definition is *The current context of execution*. If we think about the environment of where the variables are first declared, we have what MDN means by the current context of execution. Remember what we defined above? This means the current context of execution is *either* the **Global Execution Context** *or* a **Function Execution Context**. Here is a link to a CodePen.io [example](https://codepen.io/alcesalces11331/pen/xeMoZR?editors=0101) ( or a link exists at the bottom of the post ) on how hoisting and scope is affected by execution context. The important elements to take away are what contexts do variables have access to?
### Bread and Butter: Putting it all Together
To bring it back around, the tricky aspects are exactly *how* the variables get defined. This is why it was important to grasp the differences between var, let, and const. More importantly, it is fundamental to grasp the meaning of an execution context. Let's provide an example. The below example is pulled from the CodePen I created (links above and below).
```
var a = 'hoisted';
let b = 'hoisted';
const c = 'hoisted';
d = 'hoisted';

if (true) {
    var a = 'scope';
	  let b = 'scope';
	  const c = 'scope';
	  d = 'scope';
};

console.log(a);
console.log(b);
console.log(c);
console.log(d);
```
The execution context is going to declare the variables a, b, c, and d as 'hoisted' during the **Global Execution Context** execution phase. Without running the `if (true) {}` block, logging the values of the variables would present:
```
console.log(a): "hoisted"
console.log(b): "hoisted"
console.log(c): "hoisted"
console.log(d): "hoisted"
```
What happens if the `if (true) {}` block gets executed as well? Well, what do we know about execution context now?
...
Exactly! When Javascript begins the **Function Execution Context** it's going to come across variables which will either already be declared or will be reassigned. Here's what happens in this case:
```
console.log(a): "scope"
console.log(b): "hoisted"
console.log(c): "hoisted"
console.log(d): "scope"
```
Variables 'a' and 'd' were reassigned *because* of how we declared them: with `var` and without a declaration. Var can be reassigned and since 'd' is a global variable, it too becomes reassigned. With, `let` and `const` since these are declared and *exist* within a **Function Execution Context**, their assignments never leave the block they're in. Essentially, a set of variables 'b' and 'c' exist: one in the **Global Execution Context** and the **Function Execution Context**. If the values of the variables were logged while still inside the **Function Execution Context** they would be different:
```
console.log(a); "scope"
console.log(b); "scope"
console.log(c); "scope"
console.log(d); "scope"
```
See the difference?
###### Bonus: Function Hoisting
As the last amount of knowledge dropped in this blog post, **Function Hoisting** is an extrapolation of all above data. During the whichever phase the execution context is in -- **Creation or Execution** -- functions *always* get hoisted to the top of the context. 
### Thanks
Thanks for taking the time to read this post. I hope this helps everyone understand the concepts covered here. 

<p class="codepen" data-height="642" data-theme-id="0" data-default-tab="result" data-user="alcesalces11331" data-slug-hash="xeMoZR" style="height: 642px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="ES6 Hoisting and Scope Eg.">
  <span>See the Pen <a href="https://codepen.io/alcesalces11331/pen/xeMoZR/">
  ES6 Hoisting and Scope Eg.</a> by Rollin Metzger (<a href="https://codepen.io/alcesalces11331">@alcesalces11331</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

#### Special Thanks
* [This blog post from Tyler McGinnis](https://tylermcginnis.com/ultimate-guide-to-execution-contexts-hoisting-scopes-and-closures-in-javascript/) for filling in the gaps of my knowledge and educating me further on these necessary concepts. 
* [MDN Hoisting](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
* [MDN Scope](https://developer.mozilla.org/en-US/docs/Glossary/Scope)
