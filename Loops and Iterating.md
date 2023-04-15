JavaScript loops have several forms, but the main looping structures use a looping keyword, a condition, and a block which execute the loop's block/body for as long as the condition remains truthy.

**One iteration** executes the loop body once.  JavaScript also has two other loop mechanisms: array abstractions and recursion.

## while loop

A `while` loop uses the `while` keyword followed by a conditional expression in parenthesis and a block.  

The loop executes the block again and again for as long as the conditional expression remains truthy.  It needs to become falsy eventually or it results in an infinite loop that never stops repeating.
```js
let counter = 1;
while (counter <= 10) { 
  console.log(counter);
  counter = counter + 1;
}
```

The loop block must modify the counter in some way that ultimately makes the loop condition false, without doing so, the loop becomes an infinite loop which, in most cases, you don't want. 

Trick that's useful when incrementing values: 
```js
let counter = 1;
while (counter <= 10){
  console.log(counter);
  counter +=1 // counter = counter + 1
}

let a = 3;
a *= 4 //12
a /= 6 // 2
a -=2  // 0
```

Even more succinct 
```js 
let counter = 1;
while (counter <= 10) {
  console.log(counter);
  counter++ // increment operator | increases operand by 1 | -- decreases by 1
}
```

There are two forms of ++ :

* pre-increment operator = comes before the variable name 
* post-increment operator - comes after the variable name 

Both increment the variable but they differ in what gets returned by the expression, the pre returns the new value of the variable, while the post returns the previous value of the variable.

```js 
let a = 1;
++a;
2

a++
2

a
3
```

## Looping over Arrays with `while` 

Iterate we mean that we process each element in an array once at a time, in sequence from first to last element.

```js 
let names = ['Chris,' 'Kevin', 'Naveed', 'Pete', 'Victor'];
let upperNames = [];
let index = 0;

while (index < names.length) {
  let upperCaseNames = names[index].toUpperCase();
  upperNames.push(upperCaseNames);
  index += 1;
}

console.log(upperNames); // ['CHRIS', 'KEVIN,' 'NAVEED', 'PETE', 'VICTOR']
```

## `do/while` Loop

do/while code always execute the code in the block at least once, other than that it's almost identical to a `while` loop.  In a `do/while` loop the conditional check occurs at the end of the loop instead of the beginning which allows it to run code at least once, even if the condition is falsy when the loop begins.

```js
let answer;
do {
  answer = prompt('Do you want to do that again?');
} while (answer === 'y');
```

When you run this code the browser will display a prompt 'Do you want to do that again?' if you enter the lowercase `y` it displays the prompt again, it repeats this process until you enter anything other than `y` which would cause the loop to end and control moves to the first statement or expression after the loop. 

## for Loops

Same purpose as `while` but with condensed syntax that works well when iterating over arrays and other sequences.  A `for` loop combines variable initialization, loop condition, and the variable increment / decrement expression all on the same line: 

```js
for (initialization; conditoin; increment) {
  // loop body
}
```

This behaves almost the same as: 
```js
initialization;
while (condition) {
  // loop body
  increment;
}
```

The sole difference between the two loops is the scope of any variables declared by the initialization clause, in the `while` statement, the scope includes the code that surrounds the loop, in the `for` statement the scope is the `for` statement and its body.

```js 
let names = ['Chris', 'Kevin', 'Naveed', 'Pete', 'Victor'];
let upperNames = [];

for (let index = 0; index < names.length; index += 1) {
  let upperCaseName = names[index].toUpperCase();
  upperNames.push(upperCaseName);
}

console.log(upperNames); // => ['CHRIS', 'KEVIN', 'NAVEED', 'PETE', 'VICTOR']
```

What's happening here:
1. Declare and initialize the `index` variable to 0
2. If `index` is not less than the array length, go to step 6
3. Execute the loop body
4. Increment `body`
5. Go back to step 2
6. Log the results

Since for loops allow you to move the `index` variable from the global scope to the `for` statement, it's cleaner and more organized code.

## Controlling loops

JavaScript uses the keywords `continue` and `break` to provide more control over loops. 

* `continue` allows you start a new iteration of the loop
* `break` lets you terminate a loop early

### `continue`
```js
let names = ['Chris', 'Kevin', 'Naveed', 'Pete', 'Victor'];
let upperNames = [];

for (let index = 0; index < names.length; index += 1) {
  if (names[index] === 'Naveed') {
    continue;
  }

  let upperCaseName = names[index].toUpperCase();
  upperNames.push(upperCaseName);
}

console.log(upperNames); // => ['CHRIS', 'KEVIN', 'PETE', 'VICTOR']
```

The `upperNames` array will not contain 'NAVEED' because when the loop encounters the `continue` keyword, it skips the rest of the block and jumps to the next iteration.  So for this block it will skip 'Naveed'.

### `break`

You sometimes want to skip all remaining iterations of a loop.  For instance, when you search an array for a specific value.  

```js
let array = [3, 1, 5, 9, 6, 4, 7];
let indexOfFive = -1;

for (let i = 0; i < array.length; i += 1){
  if (array[i] === 5) {
    indexOfFive = i;
  }
}

console.log(indexOfFive);
```

The code above iterates over every element in the array, even if `5` is the first element.  This is where the `break` keyword is useful

```js 
let array = [3, 1, 5, 9, 2, 6, 4, 7]
let indexOfFive = -1;

for (let i = 0; i < array.length; i += 1) {
  if (array[i] === 5) {
    indexOfFive = i;
    break;
  }
}

console.log(indexOfFive);
```
The `break` system on line 7 tells JavaScript to terminate the loop once we find the desired element.


## Array Iteration 

JavaScript has several methods that iterate over elements without using looping syntax.  


### forEach
```js
let names = ['Chris', 'Kevin', 'Naveed', 'Pete', 'Victor'];

names.forEach(function(name) {
  console.log(name);
});
```

The code above will iterate over the elements of the area and log each element as is to the dev console.  An anonymous function expression is being passed into the forEach method as an argument, this is significant because <mark class="hltr-red">JavaScript uses **first-class** functions; which means functions are values, you can assign them to variables, pass them as arguments and use them to return values in other functions. </mark>

`forEach` loops through each element in an array, in sequence.  In the code above, when it encounters each name, it invokes the anon function with the name as an argument.

More concise: 
```js
let names = ['Chris', 'Kevin', 'Naveed', 'Victor'];

names.forEach(name => console.log(name));
```

## Recursion

Recursive functions are functions that call themselves.  Recursion is so close to looping that we can say it's another way to loop over data in JavaScript. 

```js

function doubler(number) {
  console.log(number * 2);
}

> doubler(2) // => 4 
> doubler(4) // => 8
> doubler(8) // => 16
> doubler(16) // => 32 
> doubler(32) // => 64

```
What if you wanted to call the function until it reaches a max without invoking the function in a clumsy way? 

Using recursion:
```js

function doubler(number) {
  console.log(number);
  
  if(number <= 50) {
    doubler(number *2);
  }
}


doubler(5);
5
10
20
40
80
```

```js
function fib(n){
  return (n === 0 || n === 1) ? n : fib(n-1) + fib(n-2);
}
```

Every recursive function has a **_baseline_** condition that marks the end of the recursion (num < 2 in the fib example) and some code that recursively calls the function with a new argument.         

Recursion, the ability to call a method inside of itself, can solve some complex problems.


## Exercises

1. Modify the `age.js` program you wrote in the exercises for the _Input/Output_ chapter. The updated code should use a `for` loop to display the future ages.
```js
let readlineSync = require('readline-sync');
let age = readlineSync.question('How old are you? ');
age = parseInt(age);
console.log(`You are ${age} years old.`)
for(let i = 10; i <=40; i += 10){
	console.log(`In ${i} years, you will be ${age + i} years old`)
}
```

2. Write a function that computes and returns the factorial of a number by using a `for` loop. The factorial of a positive integer `n`, signified by `n!`, is defined as the product of all integers between `1` and `n`, inclusive:


![![launchSchool_introJS/#^Table3]]

```js 
function factorial(n) { 
  let total = 1
    for (let i = n;  i > 0; i -= 1) {
      total *= i
    }
  return total;
}
```

3. The following code causes an infinite loop (a loop that never stops iterating). Why?
```js
let counter = 0;

while (counter = 1) {
  console.log(counter);
  counter += 1;

  if (counter > 2) {
    break;
  }
}
```
Because in line 3 the counter variable is being reassigned to 1 causing the block of code to run infinitely since the expression will never turn falsy. 

4.  Does the following code produce an error? Why or why not? What output does this code send to the console?
```js
for (let i = 0; i < 5;) {
  console.log(i += 1);
}
```
It will not cause an error since it will execute.

5. The following code uses a `randomNumberBetween` function to generate a number between its first and second arguments. It uses a `while` loop to try to generate a number greater than `2`. Refactor the code so that you don't need to call `randomNumberBetween` from two different locations, lines 6 and 10. Do not change the arguments you pass to `randomNumberBetween`.
```js
function randomNumberBetween(min, max) {
  return Math.floor(Math.random() * (max - min + 1) + min);
}

let tries = 0;
let result = randomNumberBetween(1, 6);
tries += 1;

while (result <= 2) {
  result = randomNumberBetween(1, 6);
  tries += 1;
}

console.log('It took ' + String(tries) + ' tries to get a number greater than 2');
```

refactored: 

```js
function randomNumberBetween(min, max) {
  return Math.floor(Math.random() * (max - min + 1) + min);
}

let tries = 0;
let result;

do {
  result = randomNumberBetween(1, 6);
  tries += 1;
} while (result <= 2);

console.log('It took ' + String(tries) + ' tries to get a number greater 2');
```

6.  Reimplement the `factorial` function from exercise 2 using recursion. Once again, you may assume that the argument is always a positive integer.

```js
function factorial(n) { 
  let total = 1
    for (let i = n;  i > 0; i -= 1) {
      total *= i
    }
  return total;
}
```

recursion version: 
```js
const factorial = n => { 
   if (n === 1) {
     return 1;
   } else { 
     return n * factorial(n - 1);
   }
}
```
