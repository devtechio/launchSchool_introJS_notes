Before using a function, you must define it with a reserved keyword `function` followed by function's name parenthesis and then create a function body by placing curly braces.

```js
function say() { 
	console.log('Hi!');
}
```

```js
say() // this is a function call
```

### Arguments & Parameters

Arguments let you pass data from outside the function's scope into the function so it can access the data.  You don't need arguments if the function definition doesn't need access to outside data.

The names between parentheses are called **parameters**. You can think of parameters as placeholders, while arguments refer to the values assigned to those placeholders.

**Function names and parameters are both considered variable names in JavaScript.**

Parameters, in particular, are **local variables**

They are defined locally within the function's body. Function names are either global or local, depending on whether the function is at the program's top level or nested inside a class, object, or another function.

Function names are usually global variables, but they can also be local variables if the function is nested inside another function.

The additional arguments will be ignored if you provide too many arguments when calling a function. If you provide too few arguments, the parameters and variables that correspond to the missing arguments will receive a value of `undefined`


### Return Values

All js function calls evaluate to a value, by default that value is `undefined`; this is the **implicit return value**, but when you use a `return` statement, you can return a specific value from a function; this is an **explicit return value**.

```js 
function add(a,b){
	return a + b;
}

add(2,3); // returns 5
```

When js encounters a `return` statement, it evaluates the expression, terminates the function, and returns the expression's value to the location where we called it. 

```js 
let twoAndThree = add(2,3);
console.log(twoAndThree); // => 5
```

functions that always return a boolean value are called `predicates`. 

#### Default Parameters

When a function is defined, you may want to structure it so you can call it without an argument.  
```js
function say(text = 'hello') {
	console.log(text + '!');
}
say("Howdy"); // => Howdy!
say(); // => hello!
```


### Nested Functions

```js
function foo(){
	function bar(){
		console.log('BAR');
	}
	
	bar(); // => BAR
	bar(); // => BAR
}

foo(); 
bar(); // ReferenceError: bar is not defined
```

#### Functions & Scope

Global Variables

Global variables are available anywhere within a program where they can be reassigned and read at any time. 

```js

let greetingMessage = 'Good Morning'; // global 

function greetPeople() { 
  console.log(greetingMessage); // has access to global
}

function changeGreetingMessage(newMessage) { 
  greetingMessage = newMessage;
}

changeGreetingMessage("Good Evening");
greetPeople(); // => 'Good Evening'

/* 
greetingMessage is a global variable which means it can be accessed and reassigned anywhere in the code at anytime.

the function greetPeople when invoked will log the message assigned to the greetingMessage variable.

The function changeGreetingMessage has a new parameter labeled newMessage, within the function body the greetingMessage variable is being reassigned to the argument passed into that parameter when invoked.

On line 11, the changeGreetingMessage function is being called / invoked with the message "Good Evening", reassigning the global variable greetingMessage now now reflect the newMessage.

when greetPeople() is invoked it will now log "Good Evening". 
*/
```

Most developers discourage the use of global variables since they often lead to bugs.  Limiting scope of variables as much as possible is preferred since they limit the risk that an outer scope might misuse the variable.

Local Variables

Local variables can not be accessed outside the function that declares them; where they are declared is where their scope is.

```js

function greetPeople() { 
  let greetingMessage = 'Good Morning!';
  console.log(greetingMessage);
}

greetPeople();

/*
the greetingMessage variable is declared within the function body, since the console.log is being called within the same block of code, it will display the string 'Good Morning!' to the console when greetPeople() is invoked.

If you were to run console.log(greetingMessage) you would get a RefferenceError: greetingMessage is not defined.  
*/
```

```js
function greetPeople(greetingMessage) {
  console.log(greetingMessage);
}

greetPeople('Good Morning!');
```

<mark class="hltr-red">Parameters have local scope within a function.</mark>

Local variables are short-lived. They 'go away' when the function corresponding to their scope stops running.  When the last bit of code in that scope finishes, the locally scoped variables disappear.  

#### Functions vs. Methods

Method invocation occurs when you prepend a variable name or value followed by a period for example `'xyzzy'.toUpperCase()`; these functions are called **methods**.   

There is no easy way to determine whether you should use a function or a method, you need to read the documentation or source code.

### Reassignment and Mutation

Reassignment makes the variable refer to a completely different place in memory, a different value.

Mutation changes the value that is actually stored in the memory that the name refers to. After mutating the value, the variable continues to refer to the same place in memory.

If a variable refers to an array or object, using that variable to reassign an element in the array or a property in the object **does not reassign the variable**. It mutates the array or object referenced by that variable. 

```js

let num = 3;             // variable assigned to primitive value
let arr = [1, 2, 3];     // variable assigned to an array
let obj = { a: 1, b: 2}; // variable assigned to an object

num = 42; // Reassignment
arr[1] = 42 // Ressaignment of array element, not variable.  The array referenced by arr is mutataed (changed)

obj.a = 42 // Reassigment of the object property, not the variable.  The object referenced by obj is mutated (changed)

// You can still reassign the variables

arr = 42 // Reassignment; array is lost
obj = { b: 1, c: 2 } //Reassignment, now refers to a different obj.
```

### Mutating the Caller

Sometimes a method permanently mutates the object that invokes the method; it **mutates the caller**

```js
let name = 'Pete Hanson';
console.log(name.toUpperCase()); // => 'PETE HANSON'
console.log(name);               // => 'Pete Hanson'
```

toUpperCase string method performs a non-mutating non-destructive operation, it preserves the previous value of the string. 

Some methods mutate the object.

```js
let oddNumbers = [1, 3, 5, 7, 9];
oddNumbers.pop();
console.log(oddNumbers) // => [1, 3, 5, 7]
```

The pop() method removes the last element from an array but does it destructively / the change is permanent.

Destructive array function:
```js
function changeFirstElement(array) {
  array[0] = 9;
}

let oneToFive = [1, 2, 3, 4, 5];
changeFirstElement(oneToFive);
console.log(oneToFive) // => [9, 2, 3, 4, 5]
```

Non-destructive array function:

```js
function addToArray(array) { 
  return array.concat(10);
}

let oneToFive = [1, 2, 3, 4, 5];
console.log(addToArray(onToFive)); // [1, 2, 3, 4, 5, 10]
console.log(oneToFive)             // [1, 2, 3, 4, 5]
```

`concat` method returns a new array that contains a copy of the original array combined with the additional elements. 

<mark class="hltr-red">primitive values are immutable </mark>
However, there's no way to tell whether or not a function mutates an array or object, you have to use the docs or memorize it through repetition.

JavaScript use pass by value when dealing with primitives
JavaScript uses pass by reference when dealing with objects and arrays

### Function Composition

```js

function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

let sum = add(20, 45);
console.log(sum); // => 65

let differenece  = subtract(80, 10);
console.log(difference); // => 70
```

In a process called **function composition** JavaScript lets us use a function call as an argument to another function: we can pass `add(20, 45)` and `subtract(80, 10)

```js
console.log(add(20, 45)); // => 65
console.log(subtract(80, 10)); // => 70
```

It's more interesting when you pass function call results to a function that does something more complicated: 

```js

function times(num1, num2) {
  return num1 * num2;
}
console.log(times(add(20, 45), subtract(80, 10))); // => 65 * 70 = 4550
```

```js
add(subtract(80, 10), times(subtract(20, 6), add(30, 5)));

add(70, 490) // => 560;
```

Function calls always return a value, and we can pass that function call as an argument to another function call. 


### Three Ways to Define a Function

**Function Declaration**
```js
function functionName(zeroOrMoreArgs...) {
  // function body;
}
```

<mark class="hltr-red">Function declarations allow you to call the function before you declare it.</mark>

```js

greetPeople();

function greetPeople() {
  console.log('Good Morning!');
}
```
This code will run without throwing any errors.

**Function Expression**: 

```js
let greetPeople = function () {
  console.log('Good Morning!');
};

greetPeople();
```

Most of it seems like a standard function declaration, however, we save it to a variable.   One major difference: <mark class="hltr-red">you can't invoke a function expression before it appears in your program.</mark>

JavaScript functions are first-class functions, meaning you can treat them like any other value.

<mark class="hltr-cyan">All JavaScript functions are objects</mark> which means you can assign them to variables, pass them as arguments to other functions, and rturn them from a function call.

```js
function makeGreeter(name) {
  return function greeter() {
    console.log(`Hello ${name}`)
  }
}
```

Arrow functions are similar to function expressions, but they use a different syntax. 

```js
let greetPeople = () => console.log('Good Morning!');
greetPeople();
```


```js
let add = (a, b) => a + b;
```

We can omit a `return` statement in arrow functions when the function body contains a single expression / evaluates to a single value.

When an arrow function requires one parameter you can omit the parenthesis. 

### The Call Stack / Stack

The call stack 'stack' helps js keep track of what function is executing as well as where execution should resume when the function returns.

It works like a stack of books: you can put a new book on the top or remove the topmost book from the stack; it puts information about the current function on the top of the stack, then removes that information when the function removes.

```js
function first() {
  console.log('first function');
}

function second() {
  first();
  console.log('second function');
}

second();
```

When this program starts, it has one item: **stack frame**, that represents the global ). The initial stack frame is sometimes called the `main` function. JavaScript uses the frame to keep track of what part of the main program it is currently working on.

```bash
Call Stack

-

-

-

main
```

When the program execution gets to the function invocation on line 10, it first updates the `main` stack frame with the current program location. JavaScript 

Then JavaScript creates a new stack frame for the `second` function and places it on top of the call stack: we say that the new frame is **pushed** onto the stack:

```bash
Call Stack

-

-

second

main: line 10
```


`second` function is now _stacked_ on top of the `main` frame. While the `second` frame is still on the stack, `main` remains stuck, inaccessible and dormant while `second` function becomes _active_.

The `second` function calls the `first` function on line 6, causing JavaScript to update the `second` frame with the location of where to resume execution later.  New stack frame for the `first` function and pushes it to the call stack.

```bash
Call Stack

-

first

second: line 6

main: line 10
```

Once the `first` function begins executing, it invokes the `console.log` method. 

All JavaScript functions and methods, including the built-in ones like console.log share the same call stack, meaning we need to record our current location and then push a new frame to the stack:

```bash 
Call Stack

console.log

first: line 2

second: line 6

main: line 10
```

When `console.log` returns, JavaScript removes -- **pops** -- the top frame off the stack, leaving the previous stack frame exposed, JavaScript uses this frame to determine where execution should resume, in this case it resumes immediately after line 2. 

```bash
Call Stack

-

first: line 2

second: line 6

main: line 10
```

`first` function will return, then it gets popped from the stack, exposing the `second` telling JavaScript to resume execution on line 6.
```bash
Call Stack

-

-

second: line 6

main: line 10
```


Eventually the `main` function has no more code to run when this happens, the `main` frame gets popped off rom the stack and the program ends:

```bash
Call Stack

-

-

-

-
```

The call stack has a limited size and varies based on the JavaScript implementation, the size is usually sufficient for more than 10k stack entries, if the stack runs out of room, you will see a RangeError exception with a message that mentions the stack.

#### Summary 

* Functions and methods are fundamental concepts in JavaScript
* Understanding variable scope 
* Function composition and mutation helps you catch and avoid bugs
* Multiple ways to declare functions: declaration, expression, arrow.

# Exercises

1. What does this code log to the console?  Does executing the `foo` function affect the output? Why or why not?
```js
let bar = 1; 
function foo() { 
  let bar = 2; 
  } 

foo(); 
console.log(bar);
```

console.log(bar) will log 1 to the console since it's the global variable.  Executing the `foo` function will not affect the output because within the function local scope the bar variable is being declared with block scope and wont be accessible outside the brackets.

2. In the exercises for the previous chapter, you wrote a dynamic greeter program named `greeter.js`. Add a function to this program that solicits the user's first and last names in separate invocations; the function should return the appropriate name as a string. Use the return values to greet the user with their full name.

```js
let readlineSync = require('readline-sync');
let firstName = readlineSync.question('What is your first name? ');
let lastName = readlineSync.qurstion('What is your last name? ');
console.log(`Hello, ${firstName} ${lastName}!`);
```

```js
function getName(prompt){
  let readlineSync = require('readline-sync');
  let name = readLineSync.question(prompt);
  return name;
}

let firstName = getName('What is your first name? ');
let lastName = getName('What is your last name? ');
console.log(`Hello ${firstName} ${lastName}!`);
```

3. Write a program that uses a `multiply` function to multiply two numbers and returns the result. Ask the user to enter the two numbers, then output the numbers and result as a simple equation.

```js
function multiply (num1, num2) {
	return num1 * num2;
}

function getNumber(prompt) {
  let readlineSync = require('readline-sync');
  return parseFloat(readlineSync.question(prompt));
}

let num1 = getNumber('Enter the first number: ');
let num2 = getNumber('Enter the second number: ');
console.log(`${num1} * ${num2} = ${multiply(num1, num2)}`);
```

4. What does the following code log to the console?
```js
function scream(words) { 
  words = words + '!!!!'; 
  return; 
  console.log(words); 
} 

scream('Yipeee');
```

The `return` terminates the function without anything being logged. 

5. What does the following code log to the console?
```js

function scream(words) { 
  return words + '!!!!'; 
} 

scream('Yipeee');
```

This returns the concatenated string of  'Yipeee!!!!'; but nothing is logged to the console.

6. In the code shown below, identify the following items:
```js
function multiplyNumbers(num1, num2, num3) { let result = num1 * num2 * num3; return result; } let product = multiplyNumbers(2, 3, 4);
```
-   the function arguments:  2, 3, 4
-   the function body: 
```js
//everything between the curly braces
{
  let result = num1 * num2 * num3; 
  return result;
}
```

-   the function declaration:
  ```js
  function multiplyNumbers (num1, num2, num3){
	  let result = num1 * num2 * num3; 
	  return result;
  }
  ```
-   the function invocation:
  ```js
  multiplyNumbers(2,3,4)
  ```
-   the function name: 
	`multiplyNumbers`
-   the function parameters
  `num1, num2, num3`
-   the function return value
`return result;`

-   the names of all variables in this program:
multiplyNumbers function variable
params: num1, num2, num3
result : local function variable
product: global variable

7. Without running the following code, what do you think it will output?
```js
function foo(bar, qux) { 
  console.log(bar); 
  console.log(qux); 
} 

foo('Hello');
```
The function foo has two params, neither set with a default value, on line 6 the function foo is being invoked with a single argument of 'Hello', which will be passed in for the first 'bar' param.

Therefore the console will log :
`'Hello'`
`undefined`

8. Without running the following code, what do you think it will output?
```js
function foo(bar, qux) { 
  console.log(bar); 
  console.log(qux); 
} 

foo(42, 3.1415, 2.718);
```
when foo function  is invoked with an extra argument which will be automatically ignored since the function only has two parameters.
```js
42
3.1415
```

9.Identify all of the variables named on each line of the following code. You may assume that `question` is the name of a built-in function in JavaScript (it is not, so this code won't work as written)
```js
function multiply(left, right) {
  let product = left * right;
  return product;
}

function getNumber(prompt) {
  return parseFloat(question(prompt));
}

let left = getNumber('Enter the first number: ');
let right = getNumber('Enter the second number: ');
console.log(`${left} * ${right} = ${multiply(left, right)}`);
```

```plaintext
Variable names line by line: 

line 1: multply, left, right
line 2: product, left, right
line 3: product

line 6: getNumber, prompt
line 7: parseFloat, question, prompt

line 10: left, getNumber
line 11: right, getNumber
line 12: console, left, right, multiply
```

10. Using the code from Exercise 9, classify each variable name as either global or local. For our purposes here, you may assume that the code from Exercise 9 is the entire program.
```plaintext

Global: multiply, left, right, getNumber, console, parseFloat, question

Local: left, right, product, prompt
```

11. Using the code from Exercise 9, are the `left` and `right` variables on lines 1 and 2 the same as the `left` and `right` variables on lines 10-12? Explain your reasoning.

No they are not the same variables.  lines 10-12 are global variables.  Line 1-2 are function params so they are local variables. 
