---
layout: post
title:      "Hoisting, Scopes and Objects: JS"
date:       2018-07-12 16:29:34 -0400
permalink:  hoisting_scopes_and_objects_js
---


**Hoisting**

What is hoisting? Hoisting is Javascript's approach to variable declarations. Variables that are declared are moved to the top. In JavaScript, a variable can be declared after it has been used. In other words; a variable can be used before it has been declared.

**Let's look at some examples!**

*Example 1*

```
var a = 1 

function foo(){
var b = 2;
}
foo();
console.log(b);
```

If you run this, the console will return `b is not defined`. Why?  The scope of the variable `b` is limited to the function `foo()`. 

*Example 2*

```
var a = 1;
function foo() {
var b = 2;
console.log(a);
}

foo();
console.log(b);
```

If you run this, the console will return `1` and `b is not defined`. Why?  We have access to `a`, but the root scope doesn't have access to `b`.

*Example 3*

```
var a =1 
function foo() {
var a = 2;
console.log(a)
}

foo();
```

If you run this, the console will return `2`. Why? because the scope of `a` that is logged to the console is limited to the function `foo()`. Notice how we're declaring the variable `a` twice! But because the context of a had a scope within the function, it affected what was logged onto the console.

*Example 4*

```
var a =1 
function foo() {
 a = 2;
console.log(a)
}

foo();
```

If you run this, the console will return `2`. Why? because the scope of `a` that is logged to the console is limited to the function `foo()`. Notice how we declared the variable `a` once. Because we did not declare it a second time inside of the function `foo()`, we are actually reassigning it value. This means when `console.log` was called on inside of `foo()`, it was actually accesses the variable `a` that was declared and set equal to `1`, before being reassigned to `2`.

**Scope**

What is scope? Scope is the context of your code. 

Scopes can be globally or locally defined. Scopes can have a root scope/be a window object. Understanding scope will help you understand where variables/functions are accessible, alter the scope of your code, debug quickly and much more. 

How is scope affected by arrow function? Arrow functions simplify function scope and allow us to use `this` in a straightforward manner. As a result, we must be mindful of what `this` binds to.


*The main takeaway for scope: * When a piece of code is running, what variables do you have access to?


*Example 5*

```
var a = 1;

function foo() {
var b = 2;
}
foo();
console.log(b);
```

If you run this, the console will return `b is not defined`. Why? Because the variable `b` does not have root scope. It's scope is limited to the function `foo()`. As a result, the console has the impression that the variable `b` was never declared to begin with.

*Example 6*

```
var a = 1;

function foo() {
var b = 2 ;
console.log(a);
}

foo();
console.log(b);
```

If you run this, the console will return `1` & `b is not defined`. Why? Because the variable `a` has root scope, so it is accessible within a function. On the other hand, because the variable `b` was declared inside of the function `foo`, we cannot access the variable `b` anywhere but inside of the function `foo`.

*Example 7*

```
console.log(b)
var b = 1 
```

If you run this, the console will return `undefined`. Why? Because we are logging the variable `b` to the console before it is defined. 

*Example 8*

```
var b = 1 
console.log(b)
```

If you run this, the console will return `2`. Why? Because we are logging the variable `b` to the console after it is defined. 

*Example 9*

```
console.log(b)
```

If you run this, the console will return `b is not defined`. Why? Because we are logging an undeclared variable to the console.

*Example 10*

```
eden()

function eden() {
console.log("hello world")
};
```

If you run this, it will return `hello world`. Why? Because we are calling on a function that is defined, which then logs the stirng to the console as a result of calling the function.

*Example 11*

```
var x = function eden() {
console.log("hello world")
}

x();

```

If you run this, it will return `hello world`. Why? Because by setting a variable equal to a function, and calling the variable as a function `x()`, we are inherently invoking the function that logs `hello world` to the console.

*Example 12*

```
x()

var x = function eden() {
console.log("hello world")
}
```

If you run this, it will return `undefined - is not a function`. why? Because we are calling a function before ever defining it. Remember: we need to define a function before we call it.



**Considerations: Var, Let, Const**

Here are some factors in variable/constant declaration that affect hoisting and scope;

* every time you use `var`, you are declaring a variable. When you set the variable equal to something (a string, for example), you are actually assigning it value. Notice how that effected the what a variable was intepretted in examples
> 3 and 4. According to a few [blogs](https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75), it's considered less reliable - `const` and `let` are preferrable for use. 
* `let` can be reassigned value, but often times because of that it's used within the context of a loop. As a result, it's often used within a specific context/scope (i.e., the loop or function)
* `const` signals that the constant will not be reassigned. 

`Var` is a useful tool for understanding hoisting and scope - It's really important to know these concepts because they can affect your ability to swiftly debug an issue. As you create large, complex apps, it become increasingly important to understand hoisting and scope.



 
