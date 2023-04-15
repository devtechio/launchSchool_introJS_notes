Programs need to store information in memory so it can use and manipulate that information.  Variables are the means for doing that.

Variables provide a way to label data with a descriptive name that helps us and other readers understand a program.

<mark class="hltr-cyan">Variables</mark> can be though of as containers that hold information: their <mark class="hltr-cyan">purpose is to label and store data in memory so that your program can use it.</mark>


### Variable Naming 

A variable name must accurately and succinctly describe the data that the variable contains.

Javascript variable names are often referred by the term identifiers
-   Variable names declared by `let` and `var`
-   Constant names declared by `const`
-   Property names of global objects
-   Function names
-   Function parameters
-   Class names


#### Declaring and Assigning Variables

A variable declaration is a statement that asks the JavaScript engine to reserve space for a variable with a particular name.

```js
let first name
= undefined 
```

```js
let firstName = 'Farshad'
= undefined

> firstName
'Farshad'

// we can reassign the variable to any value, not just strings

> firstName = 'Joe'
= 'Joe'

> firstName = 42
= 42

// variable declarations with or without an initial value always return `undefined`.
```

## Declaring Constants

The `const` keyword allows you to declare and initialize constant identifiers

```js
> const firstname = 'Mitchell'
= undefined

> firstName
= Mitchell
```

Unlike an ordinary variable, once you declare a constant, you cannot assign it a new value. Using constants is a great way to label a value with a name that makes your code more descriptive and easier to understand.

A standard convention when naming constants is to use all uppercase letters and digits in the name, if the name contains multiple words, use underscores to separate the words.

Const declarations require a value.


### Variable Scope

A variable's scope determines where it is available in a program. The location where you declare a variable determines its scope.

Variables declared with `let` or `const` have **block scope** 

```js
if (expression) {     // block starts at {
	doSomething();  // block body
}                   // block ends here
```

The term _block_ usually refers to executable code between braces.

```js
{
  // this is a block
  let foo = 42;
  console.log(foo);
}

if (answer === 'yes') {
  // this is a block
  console.log('yes');
} else {
  // so is this
  console.log('nope');
}

while (answer !== 'no') {
  // this is a block
  doSomething();
}

function foo() {
  // not technically a block. However, we can treat it as a block.
  let foo = 42;               // foo has block scope
  console.log(foo);
}

let foo = {
  // this is not a block
  bar: 42,
};
```

Constants declared with `const` have the same scope as variables declared with `let`.

```js
p = 'foo'
```

JavaScript has bizarre rules when working with undeclared variables, most notably all undeclared variables get global scope ignoring block scope entirely. 


# Exercises 

1. Write a program named `greeter.js` that greets `'Victor'` three times. Your program should use a variable and not hard code the string value `'Victor'` in each greeting. Here's an example run of the program:

```js
let name = 'Victor';
console.log(`Good morning, ${name}.`);
console.log(`Good afternoon, ${name}.`);
console.log(`Good evening, ${name}.`);
```

2. Write a program named `age.js` that includes someone's age and then calculates and reports the future age in 10, 20, 30 and 40 years. Below is the output for someone 20 years old.
   
   ```js
   let age = 33;
   console.log(`You are ${age} years old.`);
   console.log(`In 10 years, you will be ${age + 10} years old.`);
   console.log(`In 20 years, you will be ${age + 20} years old.`);
   console.log(`In 30 years, you will be ${age + 30} years old.`);
   console.log(`In 40 years, you will be ${age + 40} years old.`);
```

3. What happens when you run the following program? Why do we get that result?

```js
{ let foo = 'bar'; } 
console.log(foo);
 ```
If you run this code you will get an `uncaught reference error`, because the variable `foo` is block scoped, `console.log()` does not have access to the same scope, it would search the global scope and not find the variable.

4. What happens when you run the following code? Why?

```js
const NAME = 'Victor';
console.log('Good Morning, ' + NAME);
console.log('Good Afternoon, ' + NAME);
console.log('Good Evening, ' + NAME);

NAME = 'Joe';
console.log('Good Morning, ' + NAME);
console.log('Good Afternoon, ' + NAME);
console.log('Good Evening, ' + NAME);
```

The program would greet Victor three times, but it would run into an error when trying to greet Joe as constants cant be reassigned after defining it.  You would use a regular variable defined by `let` to make both work.

5. What does this program log to the console? Why?
```js
   let foo = 'bar';
   {
     let foo = 'qux';
   }
   console.log(foo);
```

Since within the code block, foo is being declared again with let and not reassigned, console.log will access the global variable foo and log 'bar' to the console.

6. Will this program produce an error when run? Why or why not?

```js
const FOO = 'bar';

{
	  const FOO = 'qux'
}

console.log(FOO);
```

Same as previous exercise, 'bar' will be logged because the of the same code scope conventions mentioned in question 5.


