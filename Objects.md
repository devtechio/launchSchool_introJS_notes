In this program, objects will be discussed as complex data structures, similar to arrays. 

Objects store collections of data in key-value pairs: each item in the collection has a name that we call the key and an associated value.   In contrast with arrays, which associate values with ordered indexes. 

An object's keys are strings or symbols, but the values can be any type, including other objects.  

```js
let person = {
  name:    'Jane',
  age:     37,
  hobbies: ['photography', 'genealogy'],
};
```

```node
> let person = { name: 'Jane', age: 37, hobbies: ['photography', 'genealogy']};
```

This object is named `person` and has 2 key-value pairs
* the name of the person, a string, defined by the `name` key
* the age of the person, a number, defined by the `age` key
* a list of the person's hobbies, an array of strings, defined by the `hobbies` key

Keys are strings, but the quotes are typically omitted when the key consists of alphanumeric characters and underscores. 

Values in objects can be accessed in two ways: 
* dot notation 
* bracket notation

```node
> person.name 
= 'Jane'

> person['age']
= 37
```

Adding more key-value pairs to `person` object: 

```node
> person.height = '5 ft'
 = '5 ft'

> person['gender'] = 'female'
= 'female'

> person
= { name: 'Jane', age: 37, hobbies: ['photography', 'genealogy'], height: '5 ft', gender: 'female'}
```

Use `delete` to remove something from an existing object.
```node
> delete person.age
= true

> delete person['gender']
= true

> delete person['hobbies']
= true

> person
= { name: 'Jane', height: '5ft'}
```

`delete` removes the key-value pair from the object and returns `true` unless it cannot delete the property.

In JavaScript key-value pairs are also called **properties**.  'Property' can also be used to refer to the key name.  For example the `name` property for the person object without mentioning the value. 

If a variable declared with `const` is initialized with an object, you cant change what object the variables refers to but you can modify the object's properties and property values.

```node

> const MyObj = { foo: 'bar', qux: 'xyz' }
> MyObj.qux = 'hey there'
> MyObj.pi = 3.1415
> MyObj
= { foo: 'bar', qux: 'hey there', pi: 3.1415 }

> MyObj = {} // Uncaught TypeError: Assignment to constand variable.


//Important to remember : variables are pointers concept
```

<mark class="hltr-orange">Const declaration prohibits changing what const  points to, but not changing the content of that thing</mark>

Like arrays, you can use Object.freeze to freeze the property values of an object:

```js
> const MyObj = Object.freeze({ foo: 'bar', qux: 'xyz' })
> MyObj.qux = 'hey there'
> MyObj
= { foo: 'bar', qux: 'xyz' }
```

#### Objects vs Primitives

Refresher:
Primitives
* strings, numbers, booleans, null, undefined, bigints and symbols.

Objects
* simple objects, arrays, dates, functions.

Objects are complex values composed of primitives values or other objects.  For example array object has a length property that contains a number: a primitive value.  Objects are usually mutable: you can add, remove and change their various values.

<mark class="hltr-red">Primitive values are always immutable. </mark> They don't have part that one can change, so their values are atomic: indivisible.  If a variable contains a primitive value, all that can be done is use it in an expression assignment or reassigning it by giving it a new value. 

```js
let number = 20
let newNumber = number + 1
newNumber
21

number
20

let object = { a: 1, b: 2, c: 3 }
object.c = object.c + 1
4
```


## Functions are Objects

This means that functions can be assigned to variables, passed to other functions as arguments and returned by other functions. 
```js
function hello() { 
  console.log('Hello there!');
}

hello(); // Prints 'Hello there!'

let greet = hello; // `greet` now points to `hello`
greet(); // Prints 'Hellow there!'
```

Both `hello` and `greet` reference the same function object.  `hello` is created automatically when declaring the function. 

```js
let hello = function() {
  console.log("Hello there!");
}

hello(); // Prints "Hello there!"


//here we are using the feature to create a function expression rathter than a delcaration. 
```

The same feature allows us to define methods.

```js
Array.prototype.push = function(newValue) {
  this[this.length] = newValue;
}

let array = [1, 2, 3];
array.push(4);
```

This feature also let you pass functions around as arguments and return values.  Array.prototype.forEach method which takes a callback function as an argument and then it calls that function once for each element in the array. 
```js
Array.prototype.forEach = function(callback) {
  for(let index = 0; index < this.length; index += 1) {
    callback(this[index]);
  }
}

let array = [1, 2, 3];
array.forEach(function callback(value) {
  console.log(value);
})
```
We can define functions that return other functions: 
```js
function greeter(greeting) {
  return function(name) {
    return console.log(`${greeting} ${name}`);
  }
}

let hello = greeter('Hello');
let hi = greeter('Hi');

console.log(hello('Trevor')); // prints 'Hello Tevor'
console.log(hi('Spencer')); // prints 'Hi Spencer'
```

Key takeaway:

<mark class="hltr-red"> functions are objects, not just code. If you want to assign or pass a function to something, you can.</mark>


##### What Things Aren't Objects or Primitives?

* variables or other identifiers like function names
* statements: `if, return, try, while,` and `break`
* keywords such as `new, fucntion, let, const`, and `class`
* anything that is neither data nor a function 
* comments


### Prototypes

JavaScript objects can **inherit** from other objects.  When object `a` inherits from object `b` , `b` is the prototype of `a` .  `a` now has access to properties defined on `b`, even though it doesn't define those properties itself. 

The static method `Object.create` provides a simple way to create a new object that inherits from an existing object:
```js
let bob = { name: 'Bob', age: 22 };
let studentBob = Object.create(bob);
studentBob.year = 'Senior';

console..og(studentBob.name); // 'Bob'
```

`Object.create` creates a new object and sets the prototype for that object to the object passed in as an argument.  The code above creates an inheritance relationship from `studentBob`, the **child** object to `bob` the **parent** object. 


### Iteration 

##### The for/in loop
Behaves similarly to ordinary `for` loop, but syntax is easier to understand since you don't need an initializer, ending condition or increment clause.  Instead, you loop over all the keys of the object, each time it assigns the key to a variable which you use to access the object's values.

```js
let person = {
  name: 'Bob',
  age: 30,
  height: '6 ft',
};

for (let prop in person) {
  console.log(person[prop]);
}

// Bob
// 30
// 6 ft
```

In the first iteration, `prop` is set to name, second: name, etc. 

One of the downside is that `for/in` iterates over the properties of an object's prototypes as well.
```js
let obj1 = { a: 1, b: 2 }
let obj2 = Object.create(obj1)
obj2.c = 3
obj2.d = 4

for (let prop in obj2){
  console.log(obj2[prop])
}
// 3
// 4
// 1
// 2

// The first two outputs are 'own properties' of obj2, followed by the properties of object1, this behavior isnt always desirable when you want to limit iteration to an object's own properties, the ones defined for itself, not inherited properties.  We can use `hasOwnProperty` method to get around that problem. 
```

```js
let obj1 = { a: 1, b:2 }
let obj2 = Object.create(obj1)
obj2.c = 3
obj2.d = 4

for (let prop in obj2){
  if(obj2.hasOwnProperty(prop)) {
    console.log(obj2[prop])  
  }
}
// 3
// 4
```


### Object.keys

The `Object.keys` static method returns an object's keys as an array.

```js
let person = { 
  name: 'Bob',
  age: 30,
  height: '6 ft'
};

let personKeys = Object.keys(person);
console.log(personKeys) // ['name', 'age', 'height']
personKeys.forEach(key => {
  console.log(person[key])
});
// Bob
// 30
// 6
```

#### Order of Object Properties

Modern versions of the ECMAScript standard (ES6+) guarantee the iteration order for an object's property keys.  It's usually in the order in which the keys got added to the object, but if you have symbol keys, or keys that look like non-negative integers ('0', '1', '2', etc) JavaScript will group the non-negative integers first, followed by other string-valued keys, and finally symbolic keys. 

#### Common Operations 

JavaScript objects don't have an abundance of methods that you can apply in your day to day usage. Most operations ob objects involve iterating over the properties or their values. Usually you use methods that extract the keys or values of an object and then iterating over the resulting array, for example when using Object.keys to extract an object's keys as an array an then using .forEach to iterate over the resulting array.

`Object.values`

This method extracts the values from every own property in an object into an array:
```js
let person = { name: 'Bob', age: 30, height: '6ft' };
let personValues = Object.values(person);
console.log(personValues); // => ['Bob', 30, '6ft']
// Remember that you can't predict the order of the values in the returned array.
```

`Object.entries` returns an array of nested arrays, each nested array has two elements: 
* one of the object's keys
* one of the object's corresponding values

```js
let person = { name: 'Bob', age: 30, height: '6ft' }
console.log(Object.entries(person)); // [['name', 'Bob'], ['age', 30], ['height', '6ft']]
```

`Object.assign

Allows you to merge two or more objects

```js
> let objA = { a: 'foo' }
= undefined

> let objB = { b: 'bar' }
= undefined

> Object.assign(objA, objB) 
= { a: 'foo', b: 'bar' }
```

Object.assign mutates the first object, in this case objA
```js
> objA
= { a: 'foo', b: 'bar' }

> objB 
= { b: 'bar' }
```

Note: that objB does not get mutated.

To create a new object and not mutating use an empty object as the first argument
```js
> objA = { a: 'foo' }
= undefined

> objB = { b: 'bar' }
= undefined

> Object.assign({}, objA, objB)
= { a: 'foo', b: 'bar' }

> objA
= { a: 'foo' }

> objB 
= { b: 'bar' }
```


## Objects vs. Arrays

When you need to choose between an object or an array to store data, ask:

* Do the individual values have names or labels? Yes, choose object, if not, array.
 
* Does order matter? Array.

* Does the structure need to be stack or queue? Arrays are good at 'last-in-first-out' stacks and 'first-in-first-out' queues. 

## Exercises

1. Given the following code, how can you access the name of the person?

```js
let person = {
  name:       'Bob',
  occupation: 'web developer',
  hobbies:    'painting',
};
```

```js
person.name;
person['name'];
```

2. Which of the following values are valid keys for an object?
-   `1`   
-   `'1'`
-   `undefined`
-   `'hello world'`
-   `true`
-   `'true'`

All of these are valid keys.  The ones that are non-string get coerced into strings.

```js
> let myObj = {}
> myObj[true] = 'hello'
> myObj['true'] = 'world'
> myObj[true]
= 'world'
```

3. Use object literal syntax (e.g., `{ key: value, ... }` notation) to create an object that behaves as an array in a `for` statement. The object should contain at least 3 elements. You should place your code between the braces in the `let` statement:

```js
let myArray = {
};

for (let i = 0; i < myArray.length; i += 1) {
  console.log(myArray[i]);
}
```

```node
let myArray = {
  0: 'hello',
  1: 23,
  2: true,
  length: 3
};

for(let i = 0; i < myArray.length; i += 1) {
  console.log(myArray[i]);
}
```

4 Create an array from the keys of the object `obj` below, with all of the keys converted to uppercase. Your implementation must not mutate obj.

```js
let obj = {
  b: 2,
  a: 1,
  c: 3,
};
```

```js
let objKeys = Object.keys(obj)
let upperKeys = objKeys.map((key) => key.toUpperCase())
console.log(upperKeys) // ['B', 'A', 'C']
console.log(obj) // { b: 2, a: 1, c: 3}
```

5. Create a new object named `myObj` that uses `myProtoObj` as its prototype.

```js
let myProtoObj = {
  foo: 1,
  bar: 2,
};
```

```
let myObject = Object.create(myProtoObj)
```

6. Which of the following values are primitive values? Which are objects? Which are neither?

-   `"foo"`  - string, primitive
-   `3.1415` - floating point number, primitive
-   `[ 'a', 'b', 'c' ]` - array, object
-   `false` - boolean, primitive
-   `foo` - neither
-   `function bar() { return "bar"; }`  - function object
-   `undefined`  - primitive 
-   `{ a: 1, b: 2 }` - object

8. Add a `qux` property with value `3` to the `myObj` object we created in the previous exercise. Now, examine the following code snippets:

```js
let objKeys = Object.keys(myObj);
objKeys.forEach(function(key) {
  console.log(key);
});
```

```js
for (let key in myObj) {
  console.log(key);
}
```

solution:
```js
myObj.qux = 3;
```

Both will iterate over the keys of myObj, but the for in iterates all of the keys including those of the prototype object
```bash
qux
foo
bar
```

Snippet one will only iterate over myObj 'own' properties that were directly defined on the object, not prototypes
```bash
qux
```

Adding a conditional to snippet 2 to get the same output as the for/in you would just check if the key is the object's own property with `hasOwnProperty`
```js
for (let key in myObj) {
  if (myObj.hasOwnProperty(key)) {
    console.log(key)
  }
}
```

8. Create a function that creates and returns a copy of an object. The function should take two arguments: the object to copy and an array of the keys that you want to copy. Do not mutate the original object.

* The function should let you omit the array of keys argument when calling the function. If you do omit the argument, the function should copy all of the existing keys from the object.

```js
function copyObj(objToCopy, keyArray) { 
  let destinationObj = {}
  
  if(keyArray) {
    keys.forEach(function(key) {
      destinationObj[key] = objToCopy[key]
    })
    
    return destinationObj
  } else {
    return Object.assign(destinationObj, objToCopy)
  }
}
```

9. What does the following program log to the console? Why?

```js
let foo = {
  a: 'hello',
  b: 'world',
};

let qux = 'hello';

function bar(argument1, argument2) {
  argument1.a = 'hi';
  argument2 = 'hi';
}

bar(foo, qux);

console.log(foo.a);
console.log(qux);
```

'hi' and 'hello' because objects are mutable, while strings and primitives are not.  

10. How many primitive values are there in the following expression? Identify them. How many objects are there in the expression? Identify those objects.
```js
[1, 2, ["a", ["b", false]], null, {}]
```

Primitive: 

```js
1, 2, 'a', 'b', false, null
```

Objects: 

```js
[1, 2, ["a", ["b", false]], null, {}]
["a", ["b", false]]
['b', 'false']
{}
```

11. Write some code to replace the value `6` in the following object with `606`:

```js
let obj = {
  foo: { a: "hello", b: "world" },
  bar: ["example", "mem", null, { xyz: 6 }, 88],
  qux: [4, 8, 12]
};
```

```js
obj['bar'[3]['xyz'] = 6

// 

obj.bar[3].xyz = 6
```

12. Consider the following code:

```js
function foo(bar) {
  console.log(bar, bar, bar);
}

foo("hello"); // should print "hello hello hello"
bar("hi");    // should print "hi hi hi"
```

As written, this code will raise an error on line 6. Without creating a new function or changing lines 5 or 6, update this code to work as intended.

```js
let bar = foo
```

13.  Consider the following code:

```js
function foo(bar) {
  console.log(bar());
}

foo();    // Should print 'Welcome'
foo();    // Should print 3.1415
foo();    // Should print [1, 2, 3]
```

As written, this code will raise an error on line 5. Without modifying `foo`, update this code to print the desired text.

```js

function foo(bar) {
  console.log(bar());
}

foo(function() { return 'Welcome'})
foo(function() { return 3.1415})
foo(function() { return [1, 2, 3]})
```

14. Identify **all** of the variables, object property names, primitive values, and objects shown in the following code (assume the code has not been executed). Don't panic if you miss a few items - this exercise is more challenging than it looks.

```js
function hello(greeting, name) {
  return greeting + ' ' + name;
}

function xyzzy() {
  return { a: 1, b: 2, c: [3, 4, 5], d: {} };
}

const howdy = hello('Hi', 'Grace');
let foo = xyzzy();
```

```js 
//variables: 
hello, greeting, name, xyzzy,  howdy, foo

//object property names: 
a, b, c, d //as well as array indexes 
0, 1, 2 //(tricky)

//primitive values: 
' ', 1, 2, 3, 4, 5, 'Hi', 'Grace'

//objects: 
hello, xyzzy // both objects (functions and arrays are objects)
{ a: 1, b: 2, c: [3,4, 5], d: {}}
[3, 4, 5]
{}
```
15. Identify all the variables, object property names, primitive values, and objects

```js
function bar(arg1, arg2) {
  let foo = 'Hello';
  const qux = {
    abc: [1, 2, 3, [4, 5, 6]],
    def: null,
    ghi: NaN,
    jkl: foo,
    mno: arg1,
    pqr: arg2,
  };

  return qux;
}

let result = bar('Victor', 'Antonina');
```

```js
//variables: 
bar, qux, result, arg1, arg2, foo

// object property names:
abc, def, ghi, jkl, mno, pqr, 0, 1, 2, 3)

// primitive values:
'Hello', 1, 2, 3, 4, 5, 6, null, NaN, 'Victor', 'Antonina', 'abc', 'def', 'ghi', 'jkl', 'mno', 'pqr', '0', '1', '2', '3'


// Objects:
  //function: 
  bar
  //object: 
  qux
  //array: 
           [1, 2, 3, [4, 5, 6]]
           [4, 5, 6]
   {
    abc: [1, 2, 3, [4, 5, 6]],
    def: null,
    ghi: NaN,
    jkl: foo,
    mno: arg1,
    pqr: arg2,
  }




