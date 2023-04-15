Array is an ordered list of elements, each element has a value of any type.

```js
let myArray = [2, 'Pete', 2.99, 'another string']
```
Arrays are **heterogeneous** : elements of various types; they can have anything in them including objects and other arrays. 

If you don't know how many elements an array contains you can access the last element by using:
```js
myArray[myArray.length - 1];
```
We have to account for index 0 so we subtract 1 from the length to get the last element index.

#### Modifying Arrays

The [ ] operator and array methods help us accomplish modifying arrays. 

```js 
> let array = [1, 2, 3]
> arr[1] = 4
= 4

> array
= [1, 4, 3]
```

```js
> array[array.length] = 10
= [1, 4, 3, 10]
```

 Variables declared with `const` are cannot change reference but you can change the contents.  Variables as pointers.  Const prohibits what variable is pointing to but not the content of that thing, in this case an array.
 
 ```js
 > const MyArray = [1, 2, 3]
 > MyArray[1] = 5
 > MyArray
 = [1, 5, 3]
 
 > MyArray = [4, 5, 6] // Uncaught TypeError: Assignment to constant variable 
```

If you want the elements of the array to also stay constant you can use the `Object.freeze` method:
```js
> const MyArray - Object.freeze([1, 2, 3])
> MyArray[1] = 5
> MyArray 
= [1, 2, 3]
```

<mark class="hltr-blue">line two will not have any effect on the array content</mark>. Object.freeze only works one level deep in the array, if the array contains nested arrays or other objects, the values inside them can still be changed unless they are also frozen deliberately. 

```js
> const MyArray = Object.freeze([1, 2, 3, [4, 5, 6]])
> MyArray[3][1] = 0
> MyArray
= [1, 2, 3, [4, 0, 6]]
```

```js
> const MyArray = Object.freeze([1, 2, 3, Object.freeze([4, 5, 6])])
> MyArray[3][1] = 0
> MyArray
= [1, 2, 3, [4, 5, 6]]
```


## Push

Adding an element to the end of an array

```js
> array.push('a')
= 5 // new length of the array

> array
= [1, 4, 3, 10, 'a']

> array.push(null, 'xyz')
= 7

> array
= [1, 4, 3, 10, 'a', null, 'xyz']
```

push appends elements to the end of the caller array, but it returns the array's updated new length it does NOT return the modified array.

## Concat

Similar to push, but it doesn't mutate the caller array. It takes two arrays, concatenates and returns a brand new array containing all the element's from the original array followed by the all the arguments passed to it. 

```js
> array.concat(42, 'abc') 
= [1, 4, 3, 10, 'a', null, 'xyz', 42, 'abc']

> array
= [1, 4, 3, 10, 'a', null, 'xyz']
```

## Pop

pop removes and returns the last element of the array 

```js 
> array.pop()
= 'xyz'

> array
= [1, 4, 3, 10, 'a', null]
```

pop mutates the caller.

## Splice

Splice method removes one or more elements from an array, even those from any position.

```js 
let array = [1, 4, 3, 10, 'a', null]

> array.splice(3,2)
[10, 'a']

> array 
= [1, 4, 3, null]
```

splice method mutates the original array and returns a new array that contians the deleted elements.  

splice can also add and insert elements. 


## Iteration Methods

forEach uses a callback function as an argument, a callback function is a function that you pass to another function as an argument.  The called function invokes the callback function when it runs, the forEach method invokes its callback once for each element in an array, passing it the element's value as an argument. <mark class="hltr-orange"> forEach always returns undefined. 
</mark>

```js
let array = [1, 2, 3]
array.forEach(function(num){
  console.log(num); // on first iteration => 1
                    // on second iteration => 2
                    // on third iteration => 3
}); // returns `undefined`
```

The callback function is invoked on every element in the caller array.

```js
let array = [1, 2, 3];
array.forEach(num => console.log(num));
```

```js
let array = [1, 2, 3];
array.forEach(num => console.log(num + 2)); // on first iteration 3
											// on second iteration 4
											// on third iteration 5
```


## map

forEach works well when you want to use the values of an array's elements.  
```js
> let numbers = [1, 2, 3, 4]
> let squares = []
> numbers.forEach(num => squares.push(num * num))
> squares
= [1, 4, 9, 16]

> numbers
= [1, 2, 3, 4]
```

side effect: squares variable gets modified which isn't part of the callback function.

```js
let numbers = [1, 2, 3, 4]
let squares = numbers.map(num => num * num)
squares
[1, 4, 9, 16]

squares = numbers.map(num => num * num)
[1, 4, 9, 16]
```

map returns a new array that contains one element for each element in `numbers`, with each element set to the return value of the callback: the squares of the numbers in this case.  This code has no side effects; the callback doesn't update `squares`, and we don't have to reset the variable if we rerun the same code.

Main thing to remember: 

<mark class="hltr-red">forEach performs simple iteration and returns undefined, while map transforms an arrays elements and returns a new array with the transformed values.</mark>

## Filter

The `filter` method is another iteration method that returns a new array that includes all the elements from the calling array which the callback returns a truthy value.  

```js
> let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 1, 2]
> numbers.filter(num => num >4) 
= [5, 6, 7, 8, 9, 10]

> numbers
= [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 1, 2]
```

`filter` iterates over the elements of the array, during each of the iterations it invokes the callback function, using the value of the current element as an argument. If the callback returns a truthy value, filter appends the element's value to a new array. When filter finishes iterating, it returns the array of _selected_ elements.  `filter` does not mutate the caller.

## reduce 

The `reduce` method effectively reduces the contents of an array to a single value. It takes to arguments: a callback function and a value that initializes something called the **accumulator**.  

In its simplest form, the callback function takes two arguments, the current value of the accumulator and an element from the array.  It then returns a value that will be used as the accumulator in the next invocation of the callback.

```js
> let arr = [2, 3, 5, 7]
> arr.reduce((accumulator, element) => accumulator + element, 0)
= 17

> arr.reduce((accumulator, element) => accumulator * element, 1)
= 210
```

```js
> let strings = ['a', 'b', 'c', 'd']
> strings.reduce((accumulator, element) => {
... return accumulator + element.toUpperCase()
...}, '');
= 'ABCD'
```

`reduce` does not mutate the caller.


#### Arrays can be odd

* indexes start at 0
* length property returns a number that is one greater than the greatest index used.  Largest index: 9 Length: 10 
* arrays are objects, typeof returns 'object'
```js
> let arr = [1, 2, 3]
> typeof arr
= 'object'
```

if you need to see if something is an array you use  `Array.isArray()` 
```js
> let arr = [1, 2, 3]
> Array.isArray(arr)
= true
```

If you change an existing array's length to something smaller, that array gets truncated, JavaScript removes all elements beyond new length.  The opposite is true as well.

```js
> let arr = []
> arr.length = 3
> arr
= [ //empty x 3]

> arr[0]
= undefined

> arr.filter(element => element === undefined)
= []

> arr.forEach(element => console.log(element)) // no output
= undefined

> arr[1] = 3
> arr
< empty, 1, empty>

> arr.length
= 3

> arr.forEach(element => console.log(element))
= 3
= undefined

> Object.keys(arr)
=['1']
```

JavaScript treats unset array elements as missing, but the length property will include those unset elements.

You can create array 'elements' with indexes that use negative or non-integer values, or even non-numeric values:
```js
> arr = [1, 2, 3]
= [1, 2, 3]

> arr[-3] = 4
= 4

> arr
= [1, 2, 3, '-3': 4]

> arr[3.1415 = 'pi']
= 'pi'

> arr['cat'] = 'Fluffy'
= 'Fluffy'

> arr
= [1, 2, 3, '3': 4, '3.1415': 'pi', cat: 'Fluffy']
```

These are properties on the array object, not true elements.  Only index value (0,1,2,3,4...) count towards the length of the array
```js
> arr.length
= 3
```

Since arrays are objects you can use the Object.keys method to return array keys, its index values, as an array of strings, even the negative, non-integer, non-numeric ones.

```js

> arr = [1, 2, 3]
> arr[-3] = 4
> arr[3.1415] = 'pi'
> arr['cat'] = 'Fluffy'
> arr 
= [1, 2, 3, '-3': 4, '3.1415': 'pi', cat: 'Fluffy']

> Object.keys(arr)
= ['0', '1', '2', '-3', '3.1415', 'cat']
```

```node

> let a = new Array(3);
> a
= [ <3 empty items> ]

> a[0] === undefined;
= true

> let b = [];
> b.length = 3;
> b
= [ <3 empty items> ]

> b[0] === undefined;
= true

> let c = [undefined, undefined, undefined]
> c
= [ undefined, undefined, undefined ]

> c[0] === undefined;
= true
```
While the length property of Array includes unset values in the count, Object.keys only counts those values that have been set to some value.

```js

> let aKeys = Object.keys(a)
> a.length
= 3
> aKeys.length
= 0

> let bKeys = Objects.keys(b)
> b.length
> 3
> bKeys.length
= 0

> let cKeys = Object.keys(c)
> c.length
= 3
> cKeys.length
= 3
```

## Nested Arrays

Array elements can include other arrays

```js
> let teams [['Joe', 'Jennifer'], ['Frank', 'Molly'], ['Dan', 'Sarah']]
```

```js
> teams[2]
= ['Dan', 'Sarah']
```

to get the second element of teams[2] you append [1] 
```js
> teams[2][1]
= 'Sarah'
```

## Array Equality

```js
> [1, 2, 3] === [1, 2, 3] // false they are not the same array occupied in memory. These arrays occupy distinct positions in memory, so they aren't the same array/ not equal.

> let a = [1, 2, 3]
> let b = a
> a === b // true 
```

#### How to check whether two arrays have the same elements

```js 
function arraysEqual(arr1, arr2) { 
  if (arr1.length !== arr2.length) 
    return false;
    
  for (let i = 0; i < arr1.lengthl i += 1) { 
    if (arr1[i] !== arr2[i]) {
      return false
    }
  }
  
  return true;
}

console.log(arraysEqual([1, 2, 3], [1, 2, 3])) // => true
console.log(arraysEqual([1, 2, 3], [4, 5, 6])) // => false
console.log(arraysEqual([1, 2, 3], [1, 2, 3, 4])) // => false
```

This works if every element is primitive, if either contain array or objects it doesn't behave as you would expect.
```js
> arrayEquals([1, 2, [3, 4], 5], [1, 2, [3, 4], 5]) 
= false
```

### Other Array Methods

##### `includes` determines whether an array includes an given element. 
```js
> let a = [1, 2, 3, 4, 5]
> a.includes(2)
= true

> a.includes(10)
= false
```

Internally `includes` uses `===` to compare elements of the array with the argument, which means we can't use `includes` to check for the existence of a nested array or an object unless we have the same object or array we're looking for: 

```js
> let inner = [3, 4];
> let a = [1, 2, inner, 5]

> a.inlcudes([3,4])
= false

> a.includes(inner)
= true
```

##### sort

The `sort` method is hand way to rearrange the elements of an array in sequence. It mutates the calling array.

```js 
> let a = ['e', 'c', 'h', 'b', 'd', 'a']
> a.sort()
= ['a', 'b', 'c', 'd', 'e', 'h']
```

##### slice

The `slice` method extracts and returns a portion of the array, it takes two optional arguments.   The first is an index which extraction begins, the second is where extraction ends. Slice does **doesn't** mutate the original array.

```js
> let fruits = ['mango', 'orange', 'banana', 'pear', 'apple']
> fruits.slice(1, 3)
= ['mango', 'orange', 'banana']

> fruits.slice(2) // second argument defaults to rest of the array
= ['banana', 'pear', 'apple']

> fruits.slice() // no arguments duplicates array
= ['mango', 'orange', 'banana', 'pear', 'apple']
```
With a second argument, `slice` returns the elements up to but excluding that index.

##### reverse

The `reverse` method reverse the order of an array.  It mutates the callign array.
```js
> let numbers = [1, 2, 3, 4]
> numbers.reverse()
= [4, 3, 2, 1]

> numbers
= [4, 3, 2, 1]
```

```node
> let numbers = [1, 2, 3, 4]
> let reversedNumbers = numbers.slice().reverse()
> reversedNumbers
= [4, 3, 2, 1]

> numbers
= [1, 2, 3, 4]
// using slice with no arguments creates a copy and doesn't mutate the orignal array.
```

## Exercises

1. In the following code, what are the final `length` values for `array1`, `array2`, `array3`, `array4`, and `array5`?
```js
let array1 = [1, 2, undefined, 4];

let array2 = [1];
array2.length = 5;

let array3 = [];
array3[-1] = [1];

let array4 = [1, 2, 3, 4, 5];
array4.length = 3;

let array5 = [];
array5[100] = 3
```
* array1 length =  4
* array2 length = 5
* array3 length = 0
* array4 length = 3
* array5 length = 101

2. Log all of the even values from `myArray` to the console.
```js 
let myArray = [1, 3, 6, 11, 4, 2, 4, 9, 17, 16, 0]
```

```js
myArray.forEach(num => (num % 2 === 0) ? console.log(num) : '')
```

3. Let's make the problem a little harder. In this problem, we're again interested in even numbers, but this time the numbers are in nested arrays in a single outer array.
```js
let myArray = [
  [1, 3, 6, 11],
  [4, 2, 4],
  [9, 17, 16, 0],
];
```
```js
for(let i = 0; i < myArray.length ; i += 1) { 
  for(let j = 0; j < myArray[i].length ; j += 1) {
	  let value = myArray[i][j];
      if(value % 2 === 0) { 
          console.log(value);
    }
  }
}
```

4. Let's try another variation on the even-numbers theme.

	We'll return to the simpler one-dimensional array. In this problem, we want to use the `map` function to create a new array that contains one element for each element in the original array. If the element is an even value, then the corresponding element in the new array should contain the string `'even'`; otherwise, the element in the new array should contain `'odd'`.

```js
let myArray = [1, 3, 6, 11, 4, 2, 4, 9, 17, 16, 0];

myArray.map(num => num % 2 === 0 ? 'even' : 'odd');
```

5. Write a `findIntegers` function that takes an array argument and returns an array that contains only the integers from the input array. Use the `filter`  method in your function.

```js
let things = [1, 'a', '1', 3, NaN, 3.1415, -4, null, false];
let integers = findIntegers(things);
console.log(integers); // => [1, 3, -4]
```

```js
function findIntegers(array) { 
  return array.filter(function(element) { 
    return Number.isInteger(element);
  });
}
```

 6. Use `map` and `filter` to first determine the lengths of all the elements in an array of string values, then discard the even values (keep the odd values).

```js
let arr = ['a', 'abcd', 'abcde', 'abc', 'ab'];
console.log(oddLengths(arr)); // => [1, 5, 3]
```

```js
const oddLengths = arr => { 
  let valLength = arr.map(val => val.length);
  return valLength.filter(num => num % 2 !== 0);
}
```

7. Use `reduce` to compute the sum of the squares of all of the numbers in an array:
```js
let array = [3, 5, 7];
console.log(sumOfSquares(array)); // => 83
```

```js
const sumOfSquares = array => {
  return array.reduce((acc, curr) => acc+ curr * curr, 0);
}
```

8.  Write a function similar to the `oddLengths` function from Exercise 6, but don't use `map` or `filter`. Instead, try to use the `reduce` method.
```js
function oddLengths(arr){
  arr.reduce((newArr, value){
    if(arr.length % 2 ===1){
      newArr.push(arr.length);
    }
    return newArr;
  }),[]);
}
```

9.  Without using a `for`, `while`, or `do/while` loop, write some code that checks whether the number `3` appears inside these arrays:

```js
const doesThreeExist = arr => arr.includes(3);
```

10. Write some code to replace the value `6` in the following array with `606`:
```js
let arr = [
  ["hello", "world"],
  ["example", "mem", null, 6, 88],
  [4, 8, 12]
];

arr[1][3] = 606;
```


