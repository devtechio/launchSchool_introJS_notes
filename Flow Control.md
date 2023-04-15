#### Conditionals 

A conditional is a fork ( or multiple forks ) in the road, Data arrives at a conditional which then tells the data where to go, in the simplest, conditionals are a combination of if statements with comparison and logical operators:

`<`, `>`, `<=`, `>=`, `==`, `===`, `!=`, `!==`, `&&`, `||`

```js
let a = prompt('Enter a number');

if(a ==='3') {
  console.log('a is 3');
} else if (a === '4'){
  console.log('a is 4');
} else {
  console.log('a is neither 3, nor 4');
}
```

```js
if (x === 3) {                          // Example 1
  console.log("x is 3");
}

if (x === 3) {                          // Example 2
  console.log("x is 3");
} else {
  console.log("x is NOT 3");
}

//It's important to understand that the `else` clause is not a separate statement: it's part of the `if` statement.

if (x === 3) console.log("x is 3");     // Example 3

if (x === 3)                            // Example 4
  console.log("x is 3");

if (x === 3)                            // Example 5
  console.log("x is 3");
else
  console.log("x is NOT 3");

if (x === 3) {                          // Example 6
  console.log('x is 3');
} else {
  if (x === 4) {
    console.log('x is 4');
  } else {
    console.log('x is NOT 3 or 4');
  }
}

if (x === 3) {                          // Example 7
  console.log("x is 3");
} else if (x === 4) {
  console.log("x is 4");
} else {
  console.log('x is NOT 3 or 4');
}
```

### Comparisons 

Comparison operators return a boolean value `true` or `false`. 

`===` strict equality operator, also known as the identity operator returns `true` when the operands have the same `type` and `value`, otherwise `false`.

```js
5 === 5 // true
5 === 4 // false
'abc' === 'abc' // true
'abc' === 'abcd' // false
'abc' === 'aBc' // false
'5' === '5' // true
'5' === '6' // false
5 === '5' // false
'' === 0 // false
```


`!==` strict inequality operator returns `false` when the operands have the same type and value, `true` otherwise.  It's the inverse of `===`
```js
5 !== 5 // false
5 !== 4 // true
'abc' !== 'abc' // false
'abc' !== 'abcd' // true
'abc' !== 'aBc' // true
'5' !== '5' // false
'5' !== '6' // true
5 !== '5' // true
'' !== 0 // true
```

`==` non-strict equality operator / loose equality operator is similar to === but when the operands have different `types`, `==` attempts to coerce one of the operands to other's type prior to comparing them; sometimes even coercing both.   The result will be `true` when the final values are the same.

```js
// Compare with the `===` examples.

> 5 == 5
= true

> 5 == 4
= false

> 5 == '5'
= true

> '' == 0
= true
```

`!=` non-strict inequality operator / loose inequality operator similar to !== however when the operands have different types, != attempts to coerce one of the operands to match the other's type, the result s `false` when the final values are the same, `true` otherwise.

```js 
// Compare with the `==` and `!==` examples.

> 5 != 5
= false

> 5 != 4
= true

> 5 != '5'
= false

> '' != 0
= false
```

< `less than operator` returns `true` when the value of the left operand has a vlaue that is less than the value of the right, `false` otherwise
```js
> 4 < 5
= true

> 5 < 4
= false

> 5 < 5
= false

> "4" < "5"
= true

> "42" < "402"
= false

> "42" < "420"
= true

> "42" < 420
= true
```

* when comparing strings the comparison is character-by-character, JavaScript moves from left-to-right looking for the first character that is different from the counterpart in the other string. If a string is being compared to a number, it gets coerced to a number so a numeric comparison takes place.

`> greater than operator` returns `true` when the value of the left operand has a value that is greater than the value of the right operand, `false` otherwise.

```js
// Compare with the `<` examples.

> 4 > 5
= false

> 5 > 4
= true

> 5 > 5
= false

> "4" > "5"
= false

> "42" > "402"
= true

> "42" > "420"
= false

> "42" > 420
= false
```

`<= Less than or equal to operator` returns `true` when the value of the left operand has a value that is less `or equal` to the right operand, `false` otherwise.  

```js
// Compare with the `<` examples.

> 4 <= 5
= true

> 5 <= 4
= false

> 5 <= 5
= true
```

`>= Greater than or equal to` returns `true` when the value of the left operand has a value that is greater than or equal to the value of the right operand, `false` otherwise.
```js
// Compare with the `>` examples.

> 4 >= 5
= false

> 5 >= 4
= true

> 5 >= 5
= true
```


## Logical Operators 

The `!, && and ||` operators provide the ability to combine conditions.

`!` `not operator` returns `true` when its operand is `false` and returns `false` when the operand is `true`, it negates the operand, and it takes a single operand, which appears to the right.

```js
> !true
= false

> !false
= true

> !(4 === 4)
= false

> !(4 !== 4)
= true
```

JavaScript first evaluates the expression on the right, then applies ! to the result, negating it.

`&& and operator` returns `true` when both operands are `true` and `false` when either operand is `false`. 

```js
> true && true
= true

> true && false
= false

> false && true
= false

> false && false
= false

> (4 === 4) && (5 === 5)
= true

> (4 === 4) && (5 === 6)
= false

> (4 === 5) && (5 === 5)
= false

> (4 === 5) && (5 === 6)
= false
```

`|| or operator` returns `true` when either operand is `true` and `false` when both operands are false

```js
> true || true
= true

> true || false
= true

> false || true
= true

> false || false
= false

> (4 === 4) || (5 === 5)
= true

> (4 === 4) || (5 === 6)
= true

> (4 === 5) || (5 === 5)
= true

> (4 === 5) || (5 === 6)
= false
```


* <mark class="hltr-red"> `&& and ||` don't always return `true` or `false`, but they do when they operate on boolean values. </mark>

## Short Circuits

The && and | | operators both use `short circuit evaluation` to evaluate operands.

```js
isRed(item) && isPortable(item)
isGreen(item) || hasWheels(item)
```

The first returns true when both item is both red and portable. If item is not red, JavaScript short-circuits the entire expression and doesn't have to call isPortable().  Same goes for second example, if either is true, it doesn't have to call the second.


## Nullish Coalescing Operator 

The `nullish coalescing operator` returns the value of the right-operand if the left-hand operand is `null` or `undefined`.  Otherwise it returns the value of the left-hand operand.

```js
> null ?? 3
= 3

> undefined ?? 42
= 42

> false ?? 3.1415
= false

> 2.718 ?? 1.414
= 2.718
```

`??` is most useful when dealing with code that could result in `undefined` or `null`, and you want to handle the situation gracefully.

```js
function foo(str) {
  let found = ["Pete", "Alli", "Chris"].find(name => name === str);
  return found ?? "Not found";
}

console.log(foo("Alli"));     // => Alli
console.log(foo("Allison"));  // => Not found
```

## Truthiness

Every `if` statement has an expression that evaluates to `true` or `false`.  However, the expression doesn't have to be one of the boolean values, JavaScript can coerce any value to a boolean and that's what it does in conditionals like `if` statements. 

```js
let a = 5
if (a) {
  console.log('how can this be true?');
} else {
  console.log('it is not true');
}
```

```js
let b = 0
if (b) {
  console.log('how can this be true?');
} else{
  console.log('it is not true');
}
```

The first example logs `'how can this be true?'` while the second logs `'it is not true'` because 5 coerces to `true` and 0 to `false` .  

```js

let x;

if (x = 5) {
  console.log('how can this be true?');
} else {
  console.log('it is not true');
}
```

This is assigning `5` to `x` not checking if it's equal, so it's coerced to `true` and `'how can this be true?'` will run.

JavaScript treats the following as false:

* false 
* 0, -0, On
* ''
* undefined
* null
* NaN

Everything else evaluates to `true`

&& and | | also work with truthy and faIsy values, and can also return truthy values instead of boolean. When using && and | | the return value is always the value of the operand evaluated last.
```js 
> 3 && 'foo'  // last evaluated operand is 'foo'
= 'foo'

> 'foo' && 3  // last evaluated operand is 3
= 3

> 0 && 'foo'  // last evaluated operand is 0
= 0

> 'foo' && 0  // last evaluated operand is 0
= 0
```

`!!` isn't a separate operator in JavaScript, it's two consecutive ! operators which is equivalent to writing `!(!a)`. The inner ! coverts the value of a to `false`, if it's truthy, and `true`, if it's falsy.   The outer! then flips true to false and false to true, in the end we end up with the boolean value instead of the truthiness value.

```js
!!3 // 3 is truthy, !3, is false, !fase is true;
= true

!!'' // '' is falsy, !'' is true, !true is false;
= false
```

#### Operator Precedence

* Comparison:  <=, <, >, >= 
* Equality: === , !== , == , != 
* Logical and : &&
* Logical or: | | 

## Ternary Operator 

A quick and easy way to write short, concise and simple if/else conditional using a combination of ? and : symbols and takes three operands.

```js
> 1 == 1 ? 'this is true' : 'this is not true'
= 'this is true'

> 1 == 0 ? 'this is true' : 'this is not true'
= 'this is not true'
```

The advantage of a ternary operator over if/else statement is that the entire structure is an expression.  We can treat the ternary expression as a value, which means we can assign it to a variable, pass it as an argument to a function, etc.   Since if / else is a statement, we can't capture it in a variable. 

```js

> let message = true ? 'this is true' : 'this is not true'
= undefined

> message
= 'this is true'

> console.log(false ? 'this is true' : 'thisis not true')
'this is not true'
= undefined
```

Ternary expressions should be used to select between 2 values, not two actions, action would be something like logging a value to the console or setting a variable to a new value.  

The ternary expression's result should almost always be assigned to a variable, passed to a function as an argument, or returned by a function.

```js

let foo = hitchhiker ? 42 : 3.1415;    // Assign result of ?: to a variable
console.log(hitchhiker ? 42 : 3.1415); //Pass result as argument
return hitchhiker ? 42 : 3.1415;       // Return result

```

## Switch Statement

A `switch` statement is similar to an `if` statement but has a different interface, it compares a single value against multiple values for strict equality ( === ), whereas `if` can test multiple expressions with any condition.

```js
let a = 5;

switch (a) {
  case 5:
    console.log('a is 5');
    break;
  case 6:
    console.log('a is 6');
    break;
  default:
    console.log('a is neither 5, nor 6');
    break;
} // => a is 5
```


## Exercises 

1. What values do the following expressions evaluate to? 

```js
false || (true && false); //false || false => false
true || (1 + 2); // true
(1 + 2) || true; // 3
true && (1 + 2); // 3
false && (1 + 2);// false
(1 + 2) && true; // true 
(32 * 4) >= 129; // false
false !== !true; // false
true === 4;      // false 
false === (847 === '847'); // true
false === (847 == '847');  // false
(!true || (!(100 / 5) === 20) || ((328 / 4) === 82)) || false; // true
```

2. Write a function, `evenOrOdd`, that determines whether its argument is an even number. If it is, the function should log `'even'` to the console; otherwise, it should log `'odd'`. For now, assume that the argument is always an integer.

```js
function evenOrOdd(number) {
  if (number % 2 === 0) {
    console.log('even');
  } else {
    console.log('odd');
  }
}
```

3. Let's improve our previous implementation of `evenOrOdd`. Add a validation check to ensure that the argument is an integer. If it isn't, the function should issue an error message and return.
```js
function evenOrOdd(number) {
  if(!Number.isInteger(number)){
    console.log('Sorry, the value you passed is not an integer')
  }
  
  if (number % 2 === 0) {
    console.log('even');
  } else {
    console.log('odd');
  }
}
```

4. What does the following code log to the console, and why?

```js
function barCodeScanner(serial) {
  switch (serial) {
    case '123':
      console.log('Product1');
    case '113':
      console.log('Product2');
    case '142':
      console.log('Product3');
    default:
      console.log('Product not found!');
  }
}

barCodeScanner('113'); // 'Product2' 'Product2' 'Product not found' because the `break` keyword is not being utilized before starting the next case so it creates a 'fall-through' effect all the way to the default.
```

4. Refactor this statement to use an `if` statement instead.
```js

	return foo () ? 'bar' : qux();
```

```js
if (foo()){
  return 'bar';
} else {
  return qux()
}
```

6. What does this code output to the console?
```js 
function isArrayEmpty(arr) {
  if (arr) {
    console.log('Not Empty');
  } else {
    console.log('Empty');
  }
}

isArrayEmpty([]);
```
The output will be 'Not Empty' because `[]` does not evaluate to a falsy value.

7. Write a function that takes a string as an argument and returns an all-caps version of the string when the string is longer than 10 characters. Otherwise, it should return the original string. Example: change `'hello world'` to `'HELLO WORLD'`, but don't change `'goodbye'`.

```js
function allCaps(str){
  return ((str.length > 10) ? str.toUpperCase() : str)
}
```

8. Write a function that logs whether an integer is between 0 and 50 (inclusive), between 51 and 100 (inclusive), greater than 100, or less than 0.

```js
function numberRange(number) {
  if (number < 0) {
    console.log(`${number} is less than 0`);
  } else if (number <= 50) {
    console.log(`${number} is between 0 and 50`);
  } else if (number <= 100) {
    console.log(`${number} is between 51 and 100`);
  } else {
    console.log(`${number} is greater than 100`);
  }
}
```

9.  Without running this code, what will it print?
```js
console.log(false ?? null); // false
console.log(true ?? (1 + 2)); // true
console.log((1 + 2) ?? true); // 3
console.log(null ?? false); // false 
console.log(undefined ?? (1 + 2)); // 3
console.log((1 + 2) ?? null); // 3
console.log(null ?? undefined); // undefined
console.log(undefined ?? null); // null
```

10. Without running this code, what will it print?
```js
function show(foo = undefined, bar = null) {
  console.log(`foo is ${foo ?? 3}, bar is ${bar ?? 42}`);
}

show(5, 7); // 'foo is 5, bar is 7'
show(0, 0); // 'foo is 0, bar is 0'
show(4)     // 'foo is 4, bar is 42'
show();     // 'foo is 3, bar is 42'
```


  