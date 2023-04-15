# JavaScript Basics

#### Reading Documentation 1

##### Finding Documentation

1. What is an excellent destination when looking for JavaScript documentation?

An excellent destination when looking for JavaScript documentation are the Mozilla Developer Network docs

##### Lowercase

2. Find out whether JavaScript has a method to lowercase a string.

'string'.toLowerCase()

##### Mountain Caps

3. Is there a method to capitalize a string?

No there is nothing to capitalize the first letter of a string, we would have to create a function, if we wanted to make everything uppercase we could use: 'string'.toUpperCase()

##### Array Element Access

4. Locate the documentation for the `Array` built-in object on MDN.  How can we access the element 'and' in the array 
```js
['fish', 'and', 'chips'];

//bracket notation [1] after the array works
['fish', 'and', 'chips'][1];

// or you can save the orignal array to a variable 
let lunch = ['fish','and','chips'];
lunch[1];
```

##### Out of Bounds

5. What happens if we take the array `['fish', 'and', 'chips']` and try to access the element in index position 10? 

Since there is no element at that position,  it's 'out of bounds', JavaScript will return `undefined`. 

##### Property vs Method

6. What are the return values of the statements on line 3 to 5?  Refer to the MDN documentation about the `Array` object for help

```js
let trees = ['birch', 'pine', 'sequoia', 'palm tree'];

trees[trees.length - 1]; // 'palm tree'
trees.pop()              // 'palm tree'
trees.[trees.length - 1] // 'seqouia'
```

##### Type of Primitive

7. Look up the MDN documentation for the `typeof` operator.  What is its return value? Determine what the following statements will return. 

`typeof` returns a string representing the _type_ of its operand.

```js
typeof 23.5;                   // 'number'
typeof 'Call me Ishmael';      // 'string'
typeof false;                  // 'boolean'
typeof 0;                      // 'number'
typeof null;                   // 'object' => this is a very well known and documented bug that was not fixed because it would cause too many problems to many programs. 
typeof undefined;              // 'undefined'
```

##### Return Values

8.  Consider the following code snippet:
```js
let tweet = "I'm learning to program! Woooot :-) #javascript #launchschool";

let words = tweet.split(' ');
let isValid = tweet.length < 140;
```

What will the following statements return? 

```js
typeof tweet // 'string'
typeof words // 'object'
typeof isValid // 'boolean'
```

Arrays are objects, if you need to specifically distinguish something is whether an object is an array you can use `Array.isArray()`, which will return a Boolean:

```js
Array.isArray(words); // true
```


##### Method Chaining 

9. Given the following tweet 

```js
let tweet = 'Starting to get the hang of it... #javascript #launchschool';
```

What will the following statements evaluate to?

```js
tweet.split(' ');// ['Starting', 'to', 'get', 'the', 'hang', 'of', 'it...', '#javascript', '#launchschool']
tweet.split(' ').reverse(); // ['#launchschool', '#javascript', 'it...', 'of', 'hang', 'the', 'get', 'to', 'Starting']
tweet.split(' ').reverse().join(' '); //'['#launchschool #javascript it... of hang the get to Starting'
```

##### Equality

10. In your JavaScript console, execute the following two lines of code to check whether their return values differ and if so, how. Take a look at the MDN documentation on equality comparisons to read about how `==` and `===` differ.
```js
'8' == 8; // true, the string will be corced into a number and then evaluated. 
'8' === 8;// false, the strict equality operator will see if the values and types are equal on both sides. 






