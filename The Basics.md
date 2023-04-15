`Primitive Data types` in JavaScript: 

`string number boolean null undefined`

Everything else is considered `object type`

Data value types can be represented by `literals`.  Literals are any notation that lets you represent a fixed value in source code:

```js
'Hello, world!'     // string literal
3.141592            // numeric literal
true                // boolean literal
{ a: 1, b: 2 }      // object literal
[ 1, 2, 3 ]         // array literal
undefined           // undefined literal
```


##### Strings 

A `string` is a list of characters in a specific sequence.

In programming we often have to work with text data such as names, messages and descriptions, JavaScript uses `strings` to represent this type of data.

You can use 'single quotes' or "double quotes"; the quotes themselves are syntactic components, not part of the value.

Template literals uses backticks and enable `string interpolation` 

```js
> `5 plus 5 equals ${5 + 5}`
= '5 plus 5 equals 10'
```

String interpolation is handy way to merge JavaScript expressions with strings:
```js
`This is an example ${expression} test.`
```
JavaScript replaces the ${expression} substring with the value of the expression inside the braces: it `interpolates` the expression's value. 

##### Numbers

JavaScript has a single data type, Number, that represents all types of numbers. 

```js
1, 2, -3, 4.5, -6.77, 234891234 // example
```

##### Booleans

`Boolean` values represent an 'on' or 'off' state, for example, if you want to represent the state of a light switch on an app, you can use boolean values. 

Boolean literal values: `true` or `false`

```node 
> let toggleOn = true
= undefined 

> let sessionActive = false
= undefined
```

##### Undefined

In programming we need a way to express the absence of a value, and in JavaScript we accomplish this with `undefined`

When a variable is not defined, its value is given by `undefined`

We can describe `undefined` as representing the absence of a value.

```js
setAgeFor('Pete', undefined)
```

```node
> console.log('Hello, World!')
Hello, World!
= undefined
```

`console.log` writes a value to the console but it doesn't have a reason to return anything specific so it returns `undefined` 

`undefined` also arises when declaring variables without an explicit value. 

```js
> let foo
= undefined

> foo
= undefined 

> let bar = 3
= undefined 

> bar
= 3
```

##### Null

`null` is similar to `undefined` : it represents the intentional absence of value, often represents emptiness or nothing. 

The chief difference between `undefined` and `null` is that you use `null` explicitly if you want to use it, `undefined` can be arise implicitly. 

You can think of `null` as a value that represents emptiness or nothing.
```js
> let foo = null
```

#### The `typeof` Operator 

Every value you use in JavaScript has a data type.

```js 
> typeof 1 
= 'number' 

>typeof 'foo' 
= 'string' 

> typeof true 
= 'boolean' 

> typeof undefined 
= 'undefined' 

> typeof null 
= 'object' 

> typeof [1, 2, 3] 
= 'object'
```

`null` being an object is a mistake from the first iteration of JavaScript, but ECMAScript standards documents describes `null` as a primitive. 

#### Operations 

>+ addition
>- subtraction
>* multiplication
>/ division
>% remainder 

### NaN

Some operations such as 0 / 0 or 3 + undefined return the value of NaN, which stands for "Not a Number"

```js
> typeof NaN
= 'number'
```

So why is typeof NaN 'number'? It's good to think of NaN as a numeric result that indicates an error occurred. NaN values arise in two main situations.

```js
let value = NaN;
Number.isNaN(value)
= true;

Object.is(value,NaN)
= true
```

Infinity and -Infinity 

Infinity is a number so large, it can't be written down, NaN on the other hand is the result of an attempted mathematical operation that is neither a valid number nor an infinite number.

1 / 0 = `Infinity`

```js
> Infinity * Infinity 
= Infinity 

> Infinity + Infinity 
= Infinity 

> Infinity - Infinity 
= NaN 

> Infinity / Infinity 
= NaN 

> 1234567890 / Infinity 
= 0
```

```js
> -1 / 0 
= -Infinity
```

```js
typeof Infinity 
= 'number'
```


String Concatenation 
```js
> 'foo' > 'bar'
= 'foobar'
```

If either operand is a string, and you're trying to '+' Javascript uses implicit type coercion to make the non-string operand into a string.

```js
> '1' + 2  
= '12'
```

Explicit Coercion

'1' and '2' and you want to add mathematically to get 3

you cant use + because of concatenation, explicit type coercion lets you decide what you want to do, whereas implicit lets the engine choose.

Strings to Numbers

The `Number` function coerces a string to a number:
```js
> Number('1')
= 1
```

`Number` takes a string value as an argument and returns a number if the string contains a valid numeric value.

```js
> Number('foo')
= NaN
```


You can use the `parseInt` function to coerce strings to numbers
```js
> parseInt('12')
= 12

> parseInt('12xyx') 
= 12

> parseInt('3.1415')
= 3

> paseFloat('12.5foo')
= 12.5
```

Number to Strings
```js
> String(20)
= '20'
```


#### Data Structures

Two most common data structures, or complex data types, that JavaScript developers use are `arrays` and `objects`

Arrays

JavaScript organize information into ordered lists using arrays. In js array literals use square brackets [ ] . 

You can access an array element by placing its index inside brackets[].  Element indexes are non-negative integers starting at 0.
```js
> [1,2,3,4,5][0]
= 1
```

Arrays can also be written in multi-line format which is useful for larger arrays or arrays with long values:
```js
[
	'Eric Idle',
	'John Cleese',
	'Terry Gilliam',
	'Graham Chapman',
	'Michael Palin',
	'Terry Jones',
]
```

* The order of the elements is significant
* Use index numbers to retrieve array elements
* Index numbers are non-negative integers starting from 0.

Objects

JavaScript `objects` have many use cases, but the one that interests us most now is the dictionary-like data structure that matches keys with specific values. 

You use keys to set or retrieve values.

### Expressions and Values

An expression is anything that JavaScript can evaluate to a value, even if that value is `undefined` or `null`. 

#### Printing (logging) vs returning values

The term **log** is a synonym for printing or displaying something to the console.

Expressions do something but they also return or evaluate to a value, the returned value may not always be what you expect.

```js 
>let a = console.log('Howdy')
>a // undefined
// the value returned by console.log() is undefined so that's the value that gets assigned to a.
```

#### Statement

 Most developers use the term "statement" in the broader sense: any syntactic unit of code that expresses an action for the computer to perform.


### Exercises 

1. Concatenate two or more strings, one with your first name and one with your last, to create a string with your full name as its value. For example, if your name is John Doe, think about how you can put `'John'` and `'Doe'` together to get `'John Doe'`.

```js 
let firstName = 'Farshad';
let lastName = 'Soheili'
let fullName = firstName + ' ' + lastName
console.log(fullName)// 'Farshad Soheili
```

2. Using arithmetic operators, get the individual digits of a 4-digit number like `4936`:

	1.  thousands place is `4`
	2.  hundreds place is `9`
	3.  tens place is `3`
	4.  ones place is `6`

3. Identify the data type for each of the following values: 
   
  ```js
  'true'        // String
  false         // Boolean
  1.5.          // Number
  2             // Number
  undefined.    // Undefined
  { foo: 'bar'} // Object 
```

4. Explain why this code logs '510' instead of 15.
```js
console.log('5' + 10)
```

This code logs '510' because in JavaScript, the + operand is being used for concatenation of strings and not arithmetic 'adding'.  Therefore it coerces the number 10 into the String '10' and concatenation occurs resulting in '510'

5. Refractor the code from the previous exercise to use explicit coercion so it logs 15 instead.
   
   ```js 
   console.log(Number('5') + 10)
   ```

6. Use the template literal syntax along with the expression `Number('5') + 10` to log the following sentence to the console:

```plaintext
The value of 5 + 10 is 15.
```

```js
console.log(`The value of 5 + 10 is ${Number('5') + 10}.`)
```

7. Will an error occur if you try to access an array element with an index that is greater than or equal to the length of the array? For example:

```js
let foo = ['a', 'b', 'c']; console.log(foo.length); // => 3 console.log(foo[3]); // will this result in an error?
```

It will result in `undefined`, because at the moment only index 0-2 have been defined.

8. Create an array named `names` that contains a list of pet names
   
   ```js
   let names = [asta,butterscotch, pudding, neptune,darwin]
   ```

9. Create an object named `pets` that contains a list of pet names and the type of animal. For instance:

```js
let pets = {
	asta: 'dog',
	butterscotch: 'cat',
	pudding: 'cat',
	neptune: 'fish',
	darwin: 'lizard'
}
```

10. What value does the following expression evaluate to?
```js
'foo' === 'Foo'
```
This will evaluate to false, case matters when comparing strings.

11. What value does the following expression evaluate to?
```js
parseInt('3.1415')
```

This will evaluate to 3, since parseInt will return the first integer it finds.

12. What value does the following expression evaluate to?
```js
'12' < '9'
```

This will evaluate to true since it will compare the first character in each 'string', it will determine that 1 is less than 9; and therefore return that 12 must be less than 9.

