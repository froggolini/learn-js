# Function
## Declaring Function
Functions are declared with the `function` keyword and the function name. The function name is always followed by parentheses without spaces, then there is a pair of curly braces that contains the logic of the function.
```js
multiply(){         // Function name
    return 5 * 5;   // Code that will be executed
}

multiply(a, b){         // Function name with the parameter
    return a * b;   
}
```

Sometimes in brackets we need additional information called parameters. Parameters are data used in functions to be processed in them.

In the function we will meet a lot of terms parameter & argument. The use of this term is often used interchangeably, even among developers.

The basic differences between the two include:
- Parameters are variables defined as input from a function. 

Example:
```js
function multiply(a, b) {
    return a * b;
}
```

An argument is a value or expression that is passed into a function. For example:
```js
multiply(3, 4);
```

After creating a function we can call it by writing the name of the function followed by parentheses and inserting the arguments in it (if any).
```js
function greeting() {
    console.log("Good Morning!")
}

greeting();

/* output
Good Morning!
*/
```

One more thing, functions can produce output or return a value. With the return value, we can create a function that functions to perform mathematical calculations and the results can be entered into a variable. Examples like this:
```js
function multiply(a, b) {
    return a * b;
}

let result = multiply(10, 2)
console.log(result)

/* output
20
*/
```

For a function to return a value, use the `return` keyword followed by the value to be returned. The return value is not only a number, it can also be a string, boolean, object, array, or other type.
```js
function greeting(name, language) {
    if(language === "English") {
        return `Good Morning ${name}!`
    } else if (language === "French") {
        return `Bonjour ${name}!`;
    } else {
        return `Selamat Pagi ${name}!`;
    }
}

let greetingMessage = greeting("Harry", "French");
console.log(greetingMessage);

/* output
Bonjour Harry!
*/
```

Another way to create a function in JavaScript is an expression function. In function expression, we generally don't need to write the function name. An unnamed function is also known as an anonymous function. The following is an example of writing an expression function:
```js
const greeting = function(name, language) {
    if(language === "English") {
        return "Good Morning " + name + "!";
    } else if (language === "French") {
        return "Bonjour " + name + "!";
    } else {
        return "Selamat Pagi " + name + "!";
    }
}

console.log(greeting('Ron', 'English'));

/* output
Good Morning Ron!
 */
```

## Function Parameter
Parameters of functions can be of any data type, ranging from strings, numbers, objects, and even other functions.

If the parameter of the function is an object, we can also use destructuring the object to get its value. Examples are as follows:
```js
const user = {
    id: 24,
    displayName: 'kren',
    fullName: 'Kylo Ren',
};

function introduce({displayName, fullName}) {
    console.log(`${displayName} is ${fullName}`);
}

introduce(user);

/* output
kren is Kylo Ren
*/
```

Functions in JavaScript do not check the number or type of arguments entered in the parameter. This means we can enter arguments even if they don't match the defined parameters.
```js
function exponentsFormula(baseNumber, exponent) {
    let result = baseNumber ** exponent;
    console.log(`${baseNumber}^${exponent} = ${result}`);
}

exponentsFormula(2);

/* output
2^undefined = NaN
*/
```

As we saw in the code sample above, when the argument is less than the parameter, the undefined parameter will be undefined. As a workaround if possible, we can provide a default value for the parameter. This value will be used if we do not enter a parameter.
```js
function exponentsFormula(baseNumber, exponent = 2) {
    let result = baseNumber ** exponent;
    console.log(`${baseNumber}^${exponent} = ${result}`);
}

exponentsFormula(3);

/* output
3^2 = 9
*/
```

Rest parameters are also written using three consecutive dots (...). With the rest parameter, we can combine several elements into one array.
```js
function sum(...numbers) {
    let result = 0;
    for (let number of numbers) {
        result += number;
    }
    return result;
}

console.log(sum(1, 2, 3, 4, 5));

/* output
15
*/
```

## Arrow Function
ES6 introduces a new function called arrow function expression or better known as arrow function. Arrow functions are similar to regular functions in behavior, but differ in how they are written. As the name implies, functions are defined using arrows or fat arrows ( `=>` ).

Apart from syntactic differences, there are behavioral differences between arrow functions and regular functions. Regular functions can be function declarations and function expressions. However, the arrow function is only an expression function. That's why the arrow function has the full name "arrow function expression".
```js
/* Regular function */
// function declaration
function sayHello(greet) {
    console.log(`${greet}!`);
}
 
// function expression
const sayName = function (name) {
    console.log(`Nama saya ${name}`)
}

/* Arrow function */
// function expression
const sayHello = (greet) => {
    console.log(`${greet}!`)
}
 
const sayName = (name) => {
    console.log(`Nama saya ${name}`)
}
```

If the function has only one parameter, then we can remove the brackets as follows:
```js
const sayName = name => {
    console.log(`Nama saya ${name}`)
}

sayName("Leia");

/* output
Nama saya Leia
*/
```

However, if we don't need any parameters at all, then we can still write brackets but empty like this:
```js
const sayHello = () => {
    console.log("Selamat pagi semuanya!")
};

sayHello();

/* output
Selamat pagi semuanya!
*/
```

When the body of the function is only one line, we can remove the curly braces. 
```js
const sayName = name => console.log(`Nama saya ${name}`);
sayName("Leia");

const sayHello = () => console.log("Selamat pagi semuanya!");
sayHello();

/* output
Nama saya Leia
Selamat pagi semuanya!
*/
```

When a function needs to return a value, we no longer need to write return (only works for single-line functions).
```js
const multiply = (a, b) => a * b;
console.log(multiply(3, 4));

/* output
12
*/
```

## Variable Scope
There are many situations where we need variables to be accessed throughout our scripts. But there are also situations where we want the variable to be accessible only in the scope of the function and its derived functions.

Variables that can be accessed from all scripts are called “globally scoped”, while variables that are only accessible to certain functions are called “locally scoped”.

JavaScript variables use functions to manage their scope. If a variable is defined outside a function, it is global. If a variable is defined inside a function, then the variable is local and its scope is only to the function and its derivatives. 

Here is an example of scoping in code:
```js
// global variable, accessible on parent() and child()
const a = 'a'; 
 
function parent() {
    // local variables, can be accessed in parent() and child(), but cannot be accessed outside of the function.
    const b = 'b'; 
    
    function child() {
        // local variable, accessible only in the child() function.
        const c = 'c';
    }
}
```

We have to be careful about defining variables inside functions. Because, we can get unexpected results, for example as follows:
```js
function multiply(num) {
    total = num * num;
    return total;
}

let total = 9;
let number  = multiply(20);

console.log(total)

/* output
400
*/
```

Perhaps we expect the total value to remain 9, considering that the `total` variable in the multiply function should have no effect for code outside of the function. This can happen because in the `multiply()` function we don't set the total variable as local scope. We do not use the `const` or `let` keywords when declaring the total variable in the `multiply()` function so that the total variable becomes global.

> If we forget to `write` `let`, `const`, or `var` keywords in the script when creating a variable, the variable will become global.

## Closure
A function that can access variables within its lexical scope is called a closure. Lexical scope means that in a nested function, the function inside has access to the variables in its parent scope.
```js
function init() {
    var name = 'Obi Wan';   // Local variables inside the scope of the init function
    
    function greet() {      // Inner function, is an example of a closure
        console.log(`Halo, ${name}`);   // Calling the variable declared in the parent function
    }

    greet();
}

init();

/* output
Halo, Obi Wan
*/
```

The `init()` function has a local variable `name` and a `greet()` function. The `greet()` function is an inner function defined in `init()` and can only be accessed from within the init() function. Note that the `greet()` function has no local variables. However, because the inner function has access to variables in its parent function, `greet()` can access the variable `name`. That is what is meant by lexical scope.

Now consider the following code example:
```js
function init() {
    var name = 'Obi Wan';

    function greet() {
        console.log(`Halo, ${name}`);
    }

    return greet;
}

let myFunction = init();
myFunction();

/* output
Halo, Obi Wan
*/
```

The above code will produce the same output. The difference is that the `greet()` function is returned from its outer function before it is executed. Because the name variable is in the `init()` scope, it is generally lost or deleted when the function is finished. However, in the above case the `greet()` function accessed via the `MyFunction()` function still has a reference or access to the name variable. The variables in the above mechanism have been closed (closed covered), which means they are inside the closure.

JavaScript does not have a way to declare a function or variable to be private like the Java language. So that a function or variable can be accessed from anywhere.
```js
let counter = 0;

let add = () => {
    return ++counter;
}

console.log(add());
console.log(add());
counter = 23;
console.log(add());

/* output
1
2
24
*/
```

The `counter` value will increase when we call the `add()` function. However, we can also change the counter value directly with the assignment operator.

Closures allow us to make functions and variables appear private. This is an example of a counter program created with a closure:
```js
let add = () => {
    let counter = 0;
    return () => {
        return ++counter;
    };
}

let addCounter = add();

console.log(addCounter());
console.log(addCounter());
console.log(addCounter());

/* output
1
2
3
*/
```