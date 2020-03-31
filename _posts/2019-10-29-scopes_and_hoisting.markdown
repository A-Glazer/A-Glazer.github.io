---
layout: post
title:      "Scopes and Hoisting"
date:       2019-10-29 11:27:32 -0400
permalink:  scopes_and_hoisting
---

## Scope

Scoping is a fundamental part of JavaScript. It allows the application to have access to variables, functions, and objects while running the code. Scoping is important since it provides security for your application. If everyone has access to everything, it would make it challenging to pinpoint the location of a bug. Additionally, scoping helps avoid naming issues. If you call a variable by the same name in a different function, it won’t override each other since they technically “don’t know about the other one”. 

Think of a scope like an office hierarchy. Everyone has access to the main office, which in JavaScript terminology would be equivalent to a `global scope`. If you are a general employee, you would have access to whatever the employees have access to, as well as the main office. That would be equivalent to a `function scope`, which is more specific. The innermost and elitist position would be the manager, who would have access to more exclusive things as well as what the employees and the main office are privileged to. The manager would be equivalent to a `block scope`. 
JavaScript variables work the same way. If a variable is called in the innermost block, JavaScript uses the `scope chain` to define it. A `scope chain` is when the application looks at the innermost scope first to see if the variable is defined. If not, it will look at the level above it, all the way up until the `global scope`. This means if you define the variable twice, both in the `global scope` and `function scope` and call it in the `function scope`, it will only give you the `function scope` definition. If you call it in the `global scope`, it will give you the `global` definition. 
For example:

```
let TestVar = “outer location”
console.log(testVar) => “outer location”
function testFunct() {
	let testVar = “inner location”
	console.log(testVar) => “inner location”
}
console.log(testVar) => “outer location”
```

If you only define a variable inside a `function scope` and then try to call it in the `global scope`, you will receive an `uncaught ReferenceError`, since it will only look at the current scope and above it (and a `function scope` is inside of a `global scope`). 

The innermost scope is called a `block scope`. A `block statement` is an ` if/else`, `for` or `while loop` etc. For the `block scope` it makes a difference which variable you call. There are 4 types of variables: `var`, `let`, `const`, `unnamed` – which becomes a `global variable`.

```
var a
let b
const c
d
```

`Const` and `let` are both `block-scoped`. This means that if you call them outside of the block, you will get an `uncaught ReferenceError`. This differs from `var`, which is not `block-scoped` and allows you to call it outside the block. For example:



```
if (true) {
		var testVar = “this is var”
		let testLet = “this is let”
		const testConst = “this is const”
	}
	
	console.log(testVar) => “this is var”
	console.log(testLet) => Uncaught ReferenceError: testLet is not defined
	console.log(testConst) => Uncaught ReferenceError: testConst is not defined	
```
	
	
	
The variable that doesn’t have a prefix (ex: `d = “global”`) will always be `globally scoped`, no matter its location. Here is an example to explain the difference of `var`, `let`, `const`, and `unnamed`.


```
function testScope() {
  const testConst = “outermost”
  let testLet = “outside”
  var testVar = “outer”
  testUnnamed = “out”
	
  if (true) {
    const testConst = “innermost”
    let testLet = “inside”
    var testVar = “inner”
    testUnnamed = “in”

  console.log(testConst) => “innermost”
  console.log(testLet) => “inside”
  console.log(testVar) => “inner”
  console.log(testUnnamed) => “in”
}

console.log(testConst) => “outermost”
console.log(testLet) => “outside”
console.log(testVar) => “inner”
console.log(testUnnamed) => “in”
}
```

In summary,  scoping allows the application to have access to variables specifically where they are defined. When the application looks for the variable, it will start with the innermost scope - first the `block scope`, then the `function scope`, and then the `global scope`. It is important to use the `const` or `let` variables since they are `block-scoped`, as opposed to `var` which is not and is easily overwritable. 

## Hoisting

**What is Hoisting?**
According to the Merriam-Webster dictionary, hoist is a verb that means to “to lift or raise”. In JavaScript, hoisting does exactly that. It raises a variable or function to the top of the scope, before the code is executed. 


**Why is hoisting important?**
In order to call a variable, it needs to be defined first. If you only define it afterwards, it will return as `undefined`. For example:

```
console.log(testVar)
var testVar = “After”
// testVar => undefined
```

vs 

```
var testVar = “before”
console.log(testVar) 
// testVar => “before”
```

This can potentially cause a lot of bugs in your code since you may think you’ve declared the variable properly, but it returns `undefined` because of its location. You may be wondering why it returns `undefined` as opposed to  the assignment. The reason is hoisting only hoists the declaration, not the assignment. It is as if the program took the variable or function declaration and hoisted it to the top of the scope and assigned it to `undefined`.Then as the code runs through, it assigns the variable once it reaches the original assignment location. Therefore, if the variable is called before it reached the assignment location, it will return `underfined`.  

**How to avoid errors with hoisting**

The best way to avoid hoisting errors is by declaring all the variables at the top of their scope. This means that if you are declaring a `global variable`, it should be declared at the very top of the code. A variable in a `function scope` should be called at the top of the function etc. 

Another way to avoid issues is by using `const` and `let`. Why? JavaScript doesn’t allow `const` or `let` to be invoked before they are initialized. If they are called before initialization, they will return a `referenceError`. (If you declare the variable using `let`, but don’t define it immediately, then you will still return `undefined`.) 

**What about a function?**

Unlike variables, functions get hoisted - both the definition and assignment. Therefore, if you call on a function before it was assigned, the code will read it as if it was both defined and assigned at the top of the scope. For example:

```
testFunct()

function testFunct(){
  return “Does this work?”
}

// testFunct() => “Does this work”
```

However, if you save the function to a variable, then it would need to be defined before calling. 
```
testVar()

var testVar = function() {
  return “This will not work”
}
// testVar() => undefined
```

A `class variable` is similar to `var` and needs to be declared before invoking.

**In summary**, the most important rule to remember regarding hoisting, is to always define your variables at the beginning of the scope. Additionally, use only `let` and `const` to avoid all errors. 
