A <mark class="hltr-cyan">runtime environment</mark>is an execution environment that lets an application program access system resources and provides the tools the app needs to operate.

The runtime environment turns an app from a set of instructions into something that performs actual work.

Programs called compilers and interpreters convert programs into a form the computer can understand. 

Compilers and interpreters differ primarily in what they do with the 1s and 0s. 
* compilers produce an output file that the computer can run directly
* interpreters doesn't produce 1's and 0's that the comp runs directly, instead it runs the interpreted code directly or passes it on to a companion program.

JavaScript is an interpreted language.
* for performance reasons, most modern JS engines employ specialized compiler called the Just In Time (JIT).  JIT takes the interpreted code one step further and lets the computer run the rest.

When an app accesses an operating system's resources, something must ensure that the os provides them in a regulated and safe manner, this is where API (Application Programming Interface) comes in: it describes the scheme and format that the programmer can use to securely access the resources, with the OS acting a the intermediary. 
* a runtime environment adds another layer of abstraction on top of the operating system's API to make these resources available with a higher-level (more accessible) API.
* the compiler/interpreted and the operating system's API together make up a runtime environment.

Besides access to a comp's resources, an app programmer needs tools for debugging and profiling code to fix bugs in the program.  Developer tools = developer environment. 

In JS there are two major runtime environments: the browser and node.js.

Apart from browsers and node.js you can find js in adobe acrobat, ActionScript, GNOME shell, and others.

With a contemporary browser you already have everything you need to run javascript code, but with node.js it may be a little bit more convenient as you dont have to embed your js file 


-   Use semicolons to terminate each logical line of code unless the line ends with `{`, `}`, or `:`. See the next section for details.
- Use spaces between operators and operands to make your code less cluttered and easier to read
- When writing a code block or function body with curly braces, write the opening brace on the same line as the function name or conditional expression. Use a single space just before the opening brace
- Use **camelCase** formatting for most variable and function names. Such names begin with a lowercase letter. If the name contains multiple words, each subsequent word should begin with an uppercase letter:
```js
let answerToUltimateQuestion = 42;     // initializing a variable
function fourScoreAndSevenYearsAgo() { // defining a function
  // do something
}
```
* Some function names -- constructor functions -- should normally use PascalCase (also known as CamelCase -- with a capital C) names. 
```js
function DomesticCat(name) { // defining a function // do something }
```
* Use uppercase names with underscores (SCREAMING_SNAKE_CASE) to represent constants that serve as _unchanging configuration values_ in your program.
```js
const INTEREST_RATE = 0.0525; 
const COURSE_NUMBER = 'JS101'; 
const HOST = 'launchschool.com';
const FIRST_LETTER = 'a'; // magic number 
const LAST_LETTER = 'z'; //
```
* We also use SCREAMING_SNAKE_CASE for constants that represent so-called _magic numbers_ (which may not actually be numbers) -- constants that are important to your program in some way but not as configuration values. 
```js
const SECONDS_PER_MINUTE = 60; 
const OUNCES_PER_POUND = 16;
const METERS_PER_KILOMETER = 1000;
const PI = 3.141592;
const INPUT_PROMPT = '==>';
const TODAY = new Date();
```

## REPL

Read, evaluate, print, loop is an interactive environment where you can type commands and expressions in that language and get immediate results. Node.js comes with one such REPL, that we can access with the `node` command.

```node
> console.log('Hello, world!') 
Hello, world! 
= undefined
```

* code prints the phrase 'Hello, world!' to the screen and returns a value of `undefined`. 


### Running JavaScript

You can run JS files from the command line.

```node
node example.js
```

## Documentation 

* As you begin to develop one of the most important habits you should develop is reading documentation. 


In JavaScript, methods are functions that need a value that you can use to call the function.

```js
'example'.toUpperCase()
```


The best way to search for JavaScript documentation is to precede your search term with the word "mdn".

# Exercises 

1. Create a directory named `my_folder` and navigate to that directory. Create two files named `one.js` and `two.js` in `my_folder`. Add the following JavaScript code to `one.js`:

```bash
mkdir my_folder
cd my_folder
touch one.js two.js

my_folder $ node one.js 
this is file one

my_folder $ node two.js 
this is file two
```

2. When you finish Exercise 1, navigate to the directory above the `my_folder` directory and delete all the content you generated in exercise 1 with one command.

```bash 
my_folder $ cd ../ 
$ rm -R my_folder
```

3. Create a file named `foo.js` in a directory named `preparations_exercises`. Add the following code to the file:
   ```js
   let foo = "bar"; 
   console.log(foo); 
   foo;
   ```
   ```bash
   mkdir preparations_exercises
   touch foo.js
   open foo.js
   ```

4.  
   1.  Use `node` to run the `foo.js` file using `node`. What does it output?
```node
$ node foo.js
bar
```

   2.  Copy and paste the code from `foo.js` into the `node` REPL. What does it output?
```node
> let foo = 'bar'
= undefined

> console.log(foo);
bar
= undefined

> foo
= 'bar'
```

   3.  Copy and paste the code from `foo.js` into the Chrome console REPL. What does it output?
```js
> let foo = 'bar'; 
  console.log(foo); 
  foo 
bar 
= "bar"
```

5. Identify the Constructors for each of the following methods and classify each method as either a "Static" or a "Prototype" method:

-   `substring`
-   `create`
-   `fromCharCode`
-   `slice`
-   `toString`

![![launchSchool_introJS/#^Table]]
6. Which of the following names satisfy the style guidelines for variable names? For the purposes of this question, constants are not variables.

`index`  `CatName`  `snake_case` `lazyDog` `quick_Fox` `1stCharacter` `operand2` `BIG_NUMBER`

index, lazyDog and operand2

7. Which of the following names satisfy the style guidelines for function names?

`index`  `CatName`  `snake_case` `lazyDog` `quick_Fox` `1stCharacter` `operand2` `BIG_NUMBER`

`index`, `lazyDog`, `operand2`, `CatName`  -- constructor functions can use PascalCase

8. Which of the following names satisfy the style guidelines for constants used to represent magic numbers?

`index`  `CatName`  `snake_case` `lazyDog` `quick_Fox` `1stCharacter` `operand2` `BIG_NUMBER`

BIG_NUMBER

9. Which of the following names don't satisfy the style guidelines for naming variables, functions, or constants?

`index`  `CatName`  `snake_case` `lazyDog` `quick_Fox` `1stCharacter` `operand2` `BIG_NUMBER`

snake_case and quick_fox are lowercase so it doesn't work
1stCharacter invalid because it starts with a number




