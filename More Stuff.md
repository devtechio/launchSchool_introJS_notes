##### Variables as Pointer

You can say a variable points to or references an object In memory, and you can also say that the pointers stored in variables are references.  Some languages make distinction between references and pointers, but JavaScript doesn't. 

```js
let count = 1;
count = 2;
```

Every time a program creates a new variable, JavaScript allocates a spot somwhere in its memory to hold its value.  With (most) primitive values, the variable's actual value gets stored in its allocated memory.   So, the `count` variable may end up at address 0x1234 in the computer's memory.  The first line sets the memory at the address to `1`.  The second line then replaces the value with at the address with `2`: 

![![launchSchool_introJS/#^Table4]]
```js 

> let a = 5
> let b = a
> a = 8


> a
= 8

> b
= 5
```

![![launchSchool_introJS/#^Table5]]The variables are stored in separate memory addresses, but both have same value, 5.

Next, we reassign variable `a` to a value of `8` on line 3, and on lines 4 and 5, we see that `a` does indeed now have the value `8` .  On lines `7` and `8` , we see that `b`'s value did not change: it is still 5.

![![launchSchool_introJS/#^Table6]]
Strings are primitives, but they aren't stored directly in variables in the same way as most primitive values, however they behave as they are stored that way.

##### Working with Objects and Non-Mutating Operations 




```js 
let obj = { a: 1 }
obj = { b : 2 }
```

We declare a variable named `obj` on line 1 and initialized it to { a : 1 }, which is an object value.  Line 2 reassigns `obj` to a new object { b : 2 }

With objects, JavaScript doesn't store the object's value in the same place.  Instead, it allocates additional memory for the object and places a pointer to the object int he variable.  We need to follow two pointers to get the value of our object from its variable name 

![![launchSchool_introJS/#^Table7]]
`Obj` is always at address 0x1234, the value at 0x1234 is a pointer to the actual object. 

While the pointer to the object can change, { b : 2 }, the `obj` itself itself always has the same address. 

The value stored at 0x1234 is a pointer to an object somewhere else in memory. 

Initially the pointer references the object { a : 1 } but after it's reassigned the new point value references the object { b : 2 }

```js
> let c = [1, 2]
> let d = c
> c = [3, 4]
> c
= [3, 4]
> d
= [1, 2]
```

#### Gotcha 

Reassignment can mutate 
```js
> let g = ['a', 'b', 'c']
> let h = g
> g[1] = 'x'
> g
= ['a', 'x', 'c']

> h
= ['a', 'x', 'c']
```

We're reassigning a specific element in the array, not the entire array. 

Takeaway:

JavaScript stores primitives values in variables.  It uses pointers for non-primitive values like arrays and other objects.

Pointers can lead to surprising and unexpected behavior when two or more variables reference the same object.  Primitive values don't have this problem. 

#### for/in and for/of

The for/in statement iterates over all enumerable properties of an object including any properties inherited from another object.

```js
let obj = { 
  foo: 1, 
  bar: 2, 
  qux: 'c'
};

for (let key in obj) {
  console.log(key);
}
// Output: foo
//         bar
//         qux
```

```js
let arr = [10, 20, 30];
for (let value in arr) {
  console.log(value);
}
// Output:  0
//          1
//          2
```
iterates over index values, indices are keys.

```js
let arr = [10, 20, 30];
for (let index in arr){
  console.log(index + 5);
}
// Output : 05 => '0' + 5
//          15 => '1' + 5
//          25 => '2' + 5
```
This is why you never use for/in to iterate over an array.

For arrays use for/of
```js
let arr = [10, 20, 30];
for (let value of arr){
  console.log(value);
}
// 10
// 20
// 30
```

for/of is similar to for/in but it iterates over the values of any 'iterable' collection, not the keys or indices.

```js
let str = 'abc';
for (let char of str) {
  console.log(char);
}
// a
// b
// c
```

### Method Chaining 
```js
let str = 'Pete Hanson';
let names - str.toUpperCase().split(' ').reverse().join(', ');
console.log(names); // => HANSON, PETE
```

1. first `.toUpperCase()` runs and returns 'PETE HANSON'
2. Then `split(' ')` runs and returns 
   ```js
   ['PETE', 'HANSON']
   ```
1. then `reverse()` runs and returns
```js
['HANSON', 'PETE']
```
3. then `join(', ')` runs and returns 'HANSON, PETE'

```js
let str = 'Pete Hanson'
let names = str.toUppercase()
               .split(' ')
               .reverse()
               join(', ');
console.log(names);
```

```js 
let str = 'Pete Hanson';
let names = str.toUppercase()
  .split(' ')
  .reverse()
  .join(', ');
console.log(names)
```

```js
let str = 'Peter Hanson'
let names = str.toUpperCase().
               split(' ').
               reverse().
               join(', ');
console.log(names);
```

#### Regex

A  **regular expression** or --regex-- is a sequence of characters that you can use to test whether a string matches a given pattern. 

JavaScript uses RegExp objects to store regex, which can invoke methods.  The method `test` returns a boolean value based on whether a string argument matches the regex.

```js
> /o/.test('bobcat')
= true

> /l/.test('bobcat')
= false
```

```js
if (/b/.test('bobcat')) {
  // this branch executes since 'b' is in 'bocat'
  console.log('Yes, it contains the letter "b"');
} else {
  // this branch does not execute since 'bobcat' contains 'b'
  console.log("No, it doesn't contain the letter 'b'")
}
```

`match` method comes in handy because boolean values sometimes don't provide enough info about a match

```js
> 'bobcat'.match(/x/) // no match
= null

> 'bobcat'.match(/[bct]/g) // global match
= ['b', 'b', 'c', 't']

> 'bobcat'.match(/b((o)b)/) // singular match with groups
= ['bob', 'ob', 'o', index: 0, input, 'bobcat', groups: undefined]
```

When `match` returns `null` if there is no match occurring, you can use that in conditionals: 
```js
function has_a_or_e(string) {
  let results = string.match(/[ae]/g);
  if (results) {
    // a non-null return value from match is truthy
    console.log(`We have a match! ${results}`);
  } else {
    console.log('No match here.');
  }
}

has_a_or_e('basketball') // We have a match! a,e,a
has_a_or_e('football') // We have a match! a
has_a_or_e('hockey') //  We have a match! e
has_a_or_e('golf') //  No match 
```

## The Math Object

Square root
```js
> Math.sqrt(36)
= 6

> Math.sqrt(2)
= 1.4142135623730951
```

PI
```js
> Math.PI
= 3.141592653589793
```

### Dates

```js
> let date = new Date('December 25, 2012')
> date.getDay()
= 2
```
getDay() returns a number for the day of the week with Sunday starting at 0, therefore 2 would be Tuesday.

```js
funtion getDayOfWeek(date) {
  let daysOfWeek = [
   'Sunday',
   'Monday',
   'Tuesday',
   'Wednesday',
   'Thursday',
   'Friday',
   'Saturday',
  ];

  return daysOfWeek[date.getDay()]
}

let date = new Date('December 25, 2012');
console.log(getDayOfWeek(date)); // => Tuesday
```

## Exception Handling 

Exception handling is the process that handles errors in a manageable and predictable manner.

```js
try {
 // perform an operation that may produce an error
} catch (exception) {
  // an error occured, do something about it
  // log the error for example
} finally {
  // Optional 'finally' block, not used often
  // Executes regardless of whether and exception occurs
}
```

```js
let names = ['bob', 'joe', 'steve', undefined, 'frank'];
names.forEach(name => {
  console.log(`${name}'s name has ${name.length} letters in it.`);
}) // => bob's name ...
   // => joes' name ...
   // => steve's name ...
   // TypeError: Cannot read property 'length'..
```

with error handling: 
```js
let names = ['bob', 'joe', 'steve', undefined, 'frank'];

names.forEach(name => {
  try {
    console.log(`${name}'s name has ${name.length} letters in it.`);
  } catch (exception) {
    console.log('Something went wrong');
  }
}); // => bob's name has 3 letters in it.
    //    joe's name has 3 letters in it.
    //    steve's name has 5 letters in it.
    //    Something went wrong
    //    frank's name has 5 letters in it.
    ```

```js 
function foo(number) {
  if (typeof number !== 'number') {
    throw new TypeError('expected a number');
  }

  // we're guaranteed to have a number here
}
```

The `throw` keyword raises an exception of the type specified as an argument, which is usually given as a `new` followed by one of the Error types.   

Best practice is to not raise exceptions for preventable conditions, they should be reserved for situations that your program can't control very easily. 


### SyntaxError

This occurs when the code can't be handled as valid JavaScript code, it occurs immediately after loading a JavaScript program, but before it begins to run.  

Unlike TypeError exception that is dependent upon runtime conditions, JS detects syntax errors based solely on the text of the program. 

```js
console.log('hello')

function foorbar()
  // some code here
}

foobar();
```

```js
}
^
SyntaxError: Unexpected token '}'
```

Three takeaways
1.  `SyntaxError` usually has nothing to do with the values of any of the variables, you can almost always spot the error visually.
2. `SyntaxError` can occur long after the point where the error was.  In the code above, the error is on line 3 (missing { ), but the problem is reported on line 5.
3. The code before and after the error does not run,  since the code is detected before programs begin to run.
4


### Stack Traces
```
TypeError: Cannot read property 'length' of undefined
    at names.forEach (repl:2:42)
    at Array.forEach (<anonymous>)
```

This error message is a stack trace: it reports the type of error that occurred, where it occurred and how it got there. 

```js
function foo() {
  console.log(bar);
}

foo();
```

```node
$ node error.js
/Users/wolfy/tmp/x.js:2
  console.log(bar);

ReferenceError: ar is not defined
  at foo (error.js:2:15)
  at Object.<anonymous> (error.js:5:1)
  ...
  ```

## Exercises 
1. What does this code log to the console? Why?
```js
let array1 = [1, 2, 3];
let array2 = array1;
array1[1] = 4;
console.log(array2);
```

Since only the 1st index of array1 is being reassigned and not the entire array, the reference remains the same for array2, so [1, 4, 3] will be logged.

2.  What do the following error message and stack trace tell you?
```plaintext
$ node exercise2.js
/Users/wolfy/tmp/exercise2.js:4
  console.log(greeting);
              ^

ReferenceError: greeting is not defined
    at hello (/Users/wolfy/tmp/exercise2.js:4:15)
    at Object.<anonymous> (/Users/wolfy/tmp/exercise2.js:13:1)
    at Module._compile (internal/modules/cjs/loader.js:721:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:732:10)
    at Module.load (internal/modules/cjs/loader.js:620:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:560:12)
    at Function.Module._load (internal/modules/cjs/loader.js:552:3)
    at Function.Module.runMain (internal/modules/cjs/loader.js:774:12)
    at executeUserCode (internal/bootstrap/node.js:342:17)
    at startExecution (internal/bootstrap/node.js:276:5)
```

It tells us that an error occurred on the exercise2.js file on line 4, it gives the point where JavaScript approximates that the error took place. 

3. Write some code to output the square root of 37.
```js
> console.log(Math.sqrt(37))
6.082762530298219
= undefined 
```

4. Given a list of numbers, write some code to find and display the largest numeric value in the list.
![![launchSchool_introJS/#^Table8]]
```js
let maxValue = Math.max(arr)
console.log(maxValue)
```

5. What does the following function do?
```js
function doSomething(string) {
  return string.split(' ').reverse().map((value) => value.length);
}
```

This function expects a string to be passed in as an argument into the parameter, then it will first split the string anywhere there is a space and create an array with those values.  It will then reverse the order of those elements in the array. Finally the map method will take those values and return a new array with the lengths of each element.

6. Write a function that searches an array of strings for every element that matches the regular expression given by its argument. The function should return all matching elements in an array.
```js
function allMatches(words, pattern) { 
  let matches = [];
  for(let i = 0; i < words.length; i += 1) {
    if (pattern.test(words[i])) {
      matches.push(words[i])
    }
  }
}

// OR

function allMatches(words, pattern) {
  return words.filter((word) => pattern.test(word))
}
```

7.  What is exception handling and what problem does it solve?

Exception handling will attempt to run code that you think may be problematic, by using try/catch statement to catch exceptions that the code in the `try` block raises, allowing the programmer to deal with the problem in a way that makes sense and prevents failures or bugs.

8. **Challenging Exercise** This exercise has nothing to do with this chapter. Instead, it uses concepts you learned earlier in the book. If you can't figure out the answer, don't worry: this question can stump developers with more experience than you have.

Earlier, we learned that `Number.isNaN(value)` returns `true` if `value` is the `NaN` value, `false` otherwise. You can also use `Object.is(value, NaN)` to make the same determination.

Without using either of those methods, write a function named `isNotANumber` that returns `true` if the value passed to it as an argument is `NaN`, `false` if it is not

```js
function isNotANumber(value) {
  return value !== value;
}
```

9.  You can use `Object.is` to determine whether a value is `-0`:
```js
> let value = -0;
> Object.is(value, 0)
= false

> Object.is(value, -0)
= true
```

```js
function isNegativeZero(value) {
  return 1 / value === -Infinity
}
```

10. What gets returned by `y++` in the snippet below?
```js
> let y = "5"
> y++
= 5
```
  
The return value will be the numeric value of 5, when you apply ++ to a string JavaScript coerces it into a number. After coercion it increments the value to 6.  Yet, the return value of `5` since the post-increment operator (y++) returns the original value of y, not the incremented value. 





