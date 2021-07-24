# JavaScript Fundamental

## Writing our First Code
```js
// Print
console.log(“Hello, World!”);

// Expression
5; // This line of code is an expression because the interpreter will read this code and return the value 5.
2 + 3; // This line of code is also an expression. The interpreter evaluates the code and will also return a value of 5.

// Statement
var yourName;
let yourAge;
const numberOfDays;  // declaration statement

// Comments
// This is a one line comment, the code below will not run
// console.log("Halo!");

/* This is a comment with more than one line
Any text that is here will be used as a comment.
When using it, don't forget to close it.
*/
```
Expression is a code that returns a value. The statement shows the action taken.

## Variable
In JavaScript, there are at least three ways to declare a variable, namely using the `var`, `let`, and `const` keywords. The ECMAScript 2015 (ES6) version introduced variable declarations with `let` and const to replace `var` which is considered controversial and prone to bugs.

The code:
```js
// First example
let lastName;
lastName = "Skywalker";
console.log(lastName);

// You can also initialize a variable's value immediately after declaring it like this:
let lastName = "Skywalker";
console.log(lastName);

// Trying to initialize the const variable again.
const z = 100;
console.log(z);
z = 200;
console.log(z)

/* TypeError: Assignment to constant variable. */
```

Because expressions must return values, they can appear anywhere in a JavaScript program. Meanwhile, statements refer to actions. So, in certain parts of the code that require a value, we can't fill it with a statement. For example:
```js
let fullName = let lastName; // Error because let lastName is a statement for variable declaration. Statements cannot be in the expression position.
let fullName = (lastName = "Skywalker"); // (lastName = "Skywalker") is an expression, so this code does not error.
let fullName = "Luke" + "Skywalker"; // "Luke" + "Skywalker" is also an expression, so this code does not error.
```

Some rules in variable naming you need to know:
- Must start with a letter or underscore (_).
- Can consist of letters, numbers, and underscore (_) in various combinations.
- Cannot contain whitespace. If the variable name is more than two words, write it in camelCase. Example firstName, lastName, catName, etc.
- Must not contain special characters (! . , / \ + * = etc.)

## Data Type
- **Undefined**. 

    This data type is formed when a variable has no value. That is, when we declare a variable without initializing its value, the variable becomes undefined. Example:

    ```js
    let x;
    console.log(typeof(x));

    /* output: undefined */
    ```
    > The `typeof()` function is used to determine the data type of a variable by returning the data type as text. 
- **Numbers**. 
    ```js
    // Integer
    let x = 10;
    console.log(typeof(x))
    /* output: number */

    // Decimal
    let y = 17.25;
    console.log(typeof(y))
    /* output: number */
    ```
    The following operators can be used in arithmetic calculations on the number data type:
    | Operator | Function | Example |
    | -------- | -------- | ------- |
    | + | Addition | 10 + 10 = 20 |
    | - | Subtraction | 15 - 7 = 8 |
    | / | Division | 21 / 7 = 3 |
    | * | Multiply | 9 * 9 = 81 |
    | % | Modulo | 5 % 2 = 1 |

    The increment (++) and decrement (--) operators are used to add or subtract 1 to the current variable value. This operator can be written before or after the variable, but it does not mean the same. Here are the conditions:
    - If written after the variable (x++), the expression will return the value of the variable before increasing its value.
    - If written before the variable (++x), the expression will return the value of the variable after increasing its value.

    Example:
    ```js
    /* Increment and Decrement */

    let postfix = 5;
    console.log(postfix++);
    /* output: 5 */
    console.log(postfix);
    /* output: 6 */

    let prefix = 5;
    console.log(++prefix);
    /* output: 6 */
    ```
- **BigInt**. 

    In JavaScript, the "Number" data type only includes values from -(2^53 - 1) to (2^53 - 1). For values outside Number, we can use the BigInt type. To distinguish between BigInt and Number types, add the character n at the end of the number. An example is like the code below.
    ```js
    const bigNumber = 1234567890123456789012345678901234567890n;
    const myInt = 1234567890123456789012345678901234567890;

    console.log(bigNumber);
    console.log(myInt);

    /* output
    1234567890123456789012345678901234567890n
    1.2345678901234568e+39
    */

    // Can be used to store small number too
    const bigIntButSmall = 7n;
    ```

    We can also use BigInt for arithmetic operations in general. The difference is in the division operation, the result will be rounded down and without containing a decimal value. Examples are like this:
    ```js
    console.log(5n + 2n);
    console.log(5n - 2n);
    console.log(5n * 2n);
    console.log(5n / 2n);
    console.log(5n % 2n);

    /* output
    7n
    3n
    10n
    2n; Not 2.5n
    1n
    */
    ```
- **Strings**.

    String which is a text. To assign a value as a string to a variable, use single quotation marks (') or double quotation marks (") between the text. For example:
    ```js
    let greet = "Hello";
    console.log(typeof(greet))
    /* output: string */

    // Wrapping it up
    const question = '"What do you think of JavaScript?" I asked';
    console.log(question)
    /* output: "What do you think of JavaScript?" he asked */

    // Using backslash (/) 
    const answer = '"I think it\'s awesome!" he answered confidently';
    ```

    String concatenation using plus (+) sign.
    ```js
    let greet = "Hello";
    let moreGreet = greet + greet;
    console.log(moreGreet);

    /* output: HelloHello */
    ```

    In addition to concatenation, strings in JavaScript also support string interpolation. Simply, we can pass variables into a template string. Examples are as follows:
    ```js
    const myName = "Luke";
    console.log(`Hello, my name is ${myName}.`);

    /* output: Hello, my name is Luke. */
    ```
    > Note that to define template strings, you need to use backticks (`), usually located on the keyboard to the left of the 1 key.

- **Boolean**.

    ```js
    let x = true;
    let y = false;

    console.log(typeof(x))
    console.log(typeof(y))

    /* output: 
    boolean
    ```

    We can also use comparison like more than (>) or less than (<):
    ```js
    let isGreater = a > b;
    let isLess = a < b;

    console.log(isGreater);
    console.log(isLess);

    /* output:
    false
    ```

- **Null**.

    Similar to undefined, but null needs to be initialized to the variable. Null is usually used as a temporary value in a variable, but it actually "does not exist". Instead we don't set any value (variable will be undefined) we better give null value to that variable and change it later when we need it. Example:
    ```js
    let someLaterData = null;
    console.log(someLaterData);

    /* output:
    null
    */
    ```

- **Symbol**.

    The Symbol data type is used to represent a unique identifier. When creating a Symbol, we can provide a description or name of the symbol like this:
    ```js
    const id = Symbol("id");

    console.log(id);

    /* output
    Symbol(id)
    */
    ```

    Symbols are called unique identifiers because even if we create two symbol variables with the same name or description, the two values are still considered different. For example see the following code:
    ```js
    const id1 = Symbol("id");
    const id2 = Symbol("id");

    console.log(id1 == id2);

    /* output
    false
    */
    ```
    This symbol is generally used as the property name of the Object.

## Operator
Operators in programming languages themselves are symbols that tell the interpreter to perform an operation such as math, relational, or logic to give a certain result.

- Assignment Operator.
    ```js
    x = y;
    ```
    The above expression means that we initialize the value of `y` on the variable `x`, so that the value of x now has the same value as y. 

    There are several other additional assignment operators in initializing values in variables. We can call it a shortcut in determining the value. For example:
    ```js
    let x = 10;
    let y = 5;
    
    x += y; // -> x = x + y;
    x -= y; // -> x = x - y;
    x *= y; // -> x = x * y;
    x /= y; // -> x = x / y;
    x %= y; // -> x = x % y;
    ```
- Comparison Operator.

    There is a set of special characters called comparison/comparison operators that can evaluate and compare two values. The following is a list of operators and their functions:
    | Operator | Function |
    | -------- | ------ |
    | == | Comparing the two values are the same. (not identical). |
    | != | Comparing the two values are not equal. (not identical). |
    | === | Compares the two values are identical. |
    | !== | Comparing the two values are not identical. |
    | > | Compares two values whether the first value is more than the second value. |
    | >= | Compares two values whether the first value is more or equal to the second value. |
    | < | Compares two values whether the first value is less than the second value. |
    | <= | Compares two values whether the first value is less or equal to the second value. |

    When we do a comparison between two values, JavaScript will evaluate both values and return a boolean with the result of the comparison, either false or true. Here's an example:
    ```js
    let a = 10;
    let b = 12;

    console.log(a < b);
    console.log(a > b);

    /* output
    true
    false
    */
    ```

    We already know that every value must have a data type be it number, string or boolean. For example, the strings "10" and the number 10 are similar, but they are not exactly the same.
    
    This is what distinguishes between equal and identical in JavaScript. If we want to compare only from the similarity of values we can use `==` but if we want to compare with respect to the data type we use `===`. 
    
    For example:

    ```js
    const aString = '10';
    const aNumber = 10

    console.log(aString == aNumber) // true, because the values are both 10
    console.log(aString === aNumber) // false, because even though the values are the same, the data types are different

    /* output
    true
    false
    */
    ```
- Logical Operator.

    With logical operators, we can use a combination of two or more boolean values in specifying logic.

    In JavaScript there are three special characters that function as logical operators. The following are the various logical operators and their functions:
    | Operator | Description |
    | -------- | --------- |
    | && | Operators AND. Logic will return true if all conditions are met (true). |
    | \|\| | operator OR. Logic will return true if one of the conditions is met (true). |
    | ! | The operator NOT. Used to reverse a condition. |

    Here is the example:
    ```js
    let a = 10;
    let b = 12;

    /* AND operator */
    console.log(a < 15 && b > 10); // (true && true) -> true
    console.log(a > 15 && b > 10); // (false && true) -> false

    /* OR operator */
    console.log(a < 15 || b > 10); // (true || true) -> true
    console.log(a > 15 || b > 10); // (false || true) -> true

    /* NOT operator */
    console.log(!(a < 15)); // !(true) -> false
    console.log(!(a < 15 && b > 10)); // !(true && true) -> !(true) -> false

    /* output
    true
    false
    true
    true
    false
    false
    */
    ```

## If/Else Statement
In the following code example we will perform a condition check using the comparison operator.
```js
let x = 50;

if(x > 70) {
    console.log(x);
} else {
    console.log("Nilai kurang dari 70");
}
```

We can also check multiple conditions at once by combining else and if. Examples are such as the following program:
```js
let language = "French";
let greeting = "Selamat Pagi"

if(language === "English") {
    greeting = "Good Morning!";
} else if(language === "French") {
    greeting = "Bonjour!"
} else if(language === "Japanese") {
    greeting = "Ohayou Gozaimasu!"
}

console.log(greeting);

/* output
Bonjour!
*/
```

In addition to the if statement above, JavaScript also supports ternary operators or conditional expressions. With this, we can write if-else statements in just one line.
```js
// condition ? true expression : false expression

const isMember = false;
const discount = isMember ? 0.1 : 0;
console.log(`Anda mendapatkan diskon sebesar ${discount * 100}%`)

/* output
Anda mendapatkan diskon sebesar 0%
*/
```

The ternary operator requires three operands. Before the question mark (?) contains the condition we want to evaluate. Then followed by an expression if the condition value is true before the colon. Lastly is the expression which is executed when the condition is false. Since it is a conditional expression, the second and third operands must return a value.

Every value in JavaScript also inherits a boolean property. This value is known as truthy or falsy. The truthy value means the value which when evaluated will return true, as well as falsy is false. So which are truthy and falsy? In addition to the boolean value false, data types or values that are considered falsy include:
- Number 0
- BigInt 0n
- Empty string like "" or ''
- null
- undefined
- NaN, or Not a Number

Here's an example in code:
```js
let name = "";

if (name) {
    console.log(`Halo, ${name}`);
} else {
    console.log("Name still empty");
}

/* output:
Name still empty
 */
```

## Switch Case Statement
In addition to `if`, JavaScript also supports a `switch` statement to check multiple conditions more easily and concisely.
```js
switch (expression) {
  case value1:
    // do something
    break;
  case value2:
    // do something
    break;
  ...
  ...
  default:
    // do something else
}
```

The parentheses after the `switch` keyword contain the variable or expression to be evaluated. Then for each condition that may occur, we enter the keyword `case` followed by a valid value. If the condition in the `case` is the same as the variable in the `switch`, the code block after the colon (:) will be executed. The `break` keyword is used to exit the switch process. There is one case named `default` which has the same function as the else keyword in the if-else control flow. If there is no value equal to the variable on the switch, then this code block will be executed.

## Loop

- For Loop.

    The basic structure of a `for` looks like this:
    ```js
    for(variable initialization; condition test; variable value change) {
        // do something
    }
    ```

    The following is an example of its actual implementation:
    ```js
    for(let i = 0; i < 5; i++) {
        console.log(i);
    }

    /* output
    0
    1
    2
    3
    4
    */
    ```

    There are three main parts to the for syntax above:
    - First, the variable `i` as iteration index. In this variable we initialize the initial value of the loop.
    - Second, the comparison operation. In this section, JavaScript will check whether the loop still needs to be done. If it is true, then the code inside the for block will be executed. 
    - Third, increment/decrement. Here we are adding or subtracting iteration variables. So, in the example above, the variable `i` will be incremented by 1 at the end of each loop. This value change is important because if we change the value, the loop process can run forever because the condition will continue to be met.

- For of Loop.

    Another way to loop is to use `for..of`. This method is much simpler and more modern than the usual for loop. The basic syntax of a for of loop is like this:
    ```js
    for(arrayItem of myArray) {
        // do something
    }
    ```

    With `for..of` the value of each array will be initialized to a new variable that we specify in each looping process. The number of loops will also adjust to the size of the array.

    Here is the example:
    ```js
    let myArray = ["Luke", "Han", "Chewbacca", "Leia"];

    for(const arrayItem of myArray) {
        console.log(arrayItem)
    }

    /* output
    Luke
    Han
    Chewbacca
    Leia
    */
    ```

- While and do-while.

    The example:
    ```js
    let i = 1;

    while (i <= 100) {
        console.log(i);
        i++;
    }
    ```

    Although while can perform the same loop as for, while is more suitable for cases where we are not sure how many iterations are required.

    Another form of while is the `do-while` loop.

    ```js
    let i = 1;

    do {
        console.log(i);
        i++;
    } while (i <= 100);
    ```

    The while condition will be evaluated before the code block in it is executed, while the do-while will evaluate the boolean expression after the code block has run. This means that the code in the do-while will be executed at least once.


