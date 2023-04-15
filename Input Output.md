A computer needs to take input from some source, perform some actions on that input and provide output.

A computer can obtain input from another computer's output.  For example, when you enter your login credentials for a website, your computer encrypts those credentials and sends them to the website's authentication serve, which then inputs the data and attempts to verify your identity. 

#### Command Line Output

```js
let name = 'Jane';
console.log(`Good morning, ${name}!`);
````

#### Command Line Input

Node.js has an API called **readline** that lets JavaScript programs read input from the command line.

For now we can use a simplified version of the readline library called **readline-sync** 


# Exercises 

1. Write a dynamic greeter program named `greeter.js`. The program should ask for your name, then output `Hello, {name}!` where `{name}` is the name you entered:
   
```bash
$ node greeter.js 
What is your name? Sue 
Hello, Sue!
```
Node solution: 
```js
let readlineSync = require('readline-sync');
let name = readlineSync.question('What is your name? ');
console.log(`Hello, ${name}!`);
```
Browser solution: 
```js 
let name = prompt('What is your name? ');
console.log(`Hello, ${name}!`);
```

2. Modify the `greeter.js` program to ask for the user's first and last names separately, then greet the user with their full name.
```bash
$ node greeter.js
What is your first name? Sue
What is your last name? Roberts
Hello, Sue Roberts!
```

```js
let readlineSync = require('readline-sync');
let firstName = readlineSync.question('What is your first name? ');
let lastName = readlineSync.qurstion('What is your last name? ');
console.log(`Hello, ${firstName} ${lastName}!`);
```

3. Modify the `age.js` program you wrote in the exercises for the _Variables_ chapter. The updated code should ask the user to enter their age instead of hard-coding the age in the program. Here's an example run:

```bash
How old are you? 22 
You are 22 years old. 
In 10 years, you will be 32 years old. 
In 20 years, you will be 42 years old. 
In 30 years, you will be 52 years old. 
In 40 years, you will be 62 years old.
```

```js
let readlineSync = require('readline-sync');
let age = readlineSync.question('Hold old are you? ');
age = parseInt(age);
console.log(`You are ${age} years old.`)
console.log(`In 10 years, you will be ${age + 10} years old.`)
console.log(`In 20 years, you will be ${age + 20} years old.`)
console.log(`In 30 years, you will be ${age + 30} years old.`)
console.log(`In 40 years, you will be ${age + 40} years old.`)
```

