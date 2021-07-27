# Error Handling
## Try and Catch
To handle JavaScript errors, use try and catch. Writing the try-catch code to handle the error is like this:
```js
try {
    // kode
} catch (error) {
    // error handling
}
```

Put the code that has the potential to cause an error in the `try` block. If an error occurs in the try code block, it will be caught and handled by the `catch` code block. Meanwhile, if there is no error in the code, the catch block will be ignored.
```js
try {
    console.log("Beginning of the try block");
    console.log("End of the try block");
} catch (error) {
    console.log("No error occurs, then this code is ignored");
}
 
/* output
Beginning of the try block
End of the try block
*/
```

The code in the try block above will not return an error, so the code in the catch block will be ignored and not executed. The following is an example of code that generates an error:
```js
try {
    console.log("Beginning of the try block");   // (1)
    errorCode;                      // (2)
    console.log("End of the try block");  // (3)
} catch (error) {
    console.log("An error occurred!");  // (4)
}
 
/* output
Beginning of the try block
An error occurred!
*/
```

The line of code (2) will generate an error. The execution of the code inside the try block will be stopped, so line of code (3) will not be executed. Then the code will continue to line (4) or catch block.

Now consider the catch block. There catch has one parameter named error (variable name can be changed). The error variable is an object that stores detailed information about the error that occurred.

The error object has several main properties in it, namely:
- **name** : The name of the error that occurred.
- **message** : Message about error details.
- **stack** : Information on the sequence of events that caused the error. Generally used for debugging because there is information on which line caused the error.

Now let's try to modify the code and display the error property above.
```js
try {
    console.log("Beginning of the try block");   // (1)
    errorCode;                      // (2)
    console.log("End of the try block");  // (3)
} catch (error) {
    console.log(error.name);
    console.log(error.message);
    console.log(error.stack);
}
 
/* output
Beginning of the try block
ReferenceError
errorCode is not defined
ReferenceError: errorCode is not defined
    at file:///home/dicoding/Playground/javascript/CoffeeMachine/error.js:3:5
    at ModuleJob.run (internal/modules/esm/module_job.js:152:23)
    at async Loader.import (internal/modules/esm/loader.js:166:24)
    at async Object.loadESM (internal/process/esm_loader.js:68:5)
*/
```

From the information above, we can tell that the error that appears is a `ReferenceError` because `errorCode` is considered as an undefined variable or value.

### try-catch-finally
The `finally` block will still execute regardless of the outcome of the try-catch block.
```js
try {
    console.log("Beginning of the try block");
    console.log("End of the try block");
} catch (error) {
    console.log("This line is ignored");
} finally {
    console.log("Will still be executed");
}
 
/* output
Awal blok try
Akhir blok try
Akan tetap dieksekusi
*/
```

## Throwing Errors
Now let's look at the implementation of try-catch in a more general case. Note the following code:
```js
let json = '{ "name": "Yoda", "age": 20 }';
 
try {
    let user = JSON.parse(json);
 
    console.log(user.name);
    console.log(user.age);
} catch (error) {
    console.log(error.name);
    console.log(error.message);
}
```

In the code above, the JSON.parse function will parse or convert the json variable (String) into an object. We will encounter many scenarios like the one above when we make requests to the API.

Then, what if the json string doesn't match the JavaScript object format?
```js
let json = '{ bad json }';
 
try {
    let user = JSON.parse(json);
 
    console.log(user.name);
    console.log(user.age);
} catch (error) {
    console.log(error.name);
    console.log(error.message);
}
 
 
/* output
SyntaxError
Unexpected token b in JSON at position 2
*/
```

Syntactically, the code above does not throw an error, so the catch block will be ignored. However, the absence of the name property in json is actually the same as an error because it will have an impact on the running of our program.

To work around this, we can use `throw`. This operator will "throw" the error in the program, so that the code execution will enter the catch block. Here's an example of implementing throw to throw our own error:
```js
let json = '{ "age": 20 }';
 
try {
    let user = JSON.parse(json);
 
    if (!user.name) {
        throw new SyntaxError("'name' is required.");
    }
 
    console.log(user.name); // undefined
    console.log(user.age);  // 20
} catch (error) {
    console.log(`JSON Error: ${error.message}`);
}
 
/* output
JSON Error: 'name' is required.
*/
```

When the `user.name` property has no value, the program will generate a `SyntaxError`. In it we can define a message that can help explain what the error is.

Now suppose that json is correct, but it turns out that another error occurred, for example due to an undefined variable.
```js
let json = '{ "name": "Yoda", "age": 20 }';
 
try {
    let user = JSON.parse(json);
 
    if (!user.name) {
        throw new SyntaxError("'name' is required.");
    }
 
    errorCode;
 
    console.log(user.name); // Yoda
    console.log(user.age);  // 20
} catch (error) {
    console.log(`JSON Error: ${error.message}`);
}
 
/* output
JSON Error: errorCode is not defined
*/
```

The error was handled successfully, but the console still displays the message “JSON Error”, so how can we display the error message according to the error that appears?

The answer is with an if statement.
```js
try {
    // ...
} catch (error) {
    if (error instanceof SyntaxError) {
        console.log(`JSON Error: ${error.message}`);
    } else if (error instanceof ReferenceError) {
        console.log(error.message);
    } else {
        console.log(error.stack);
    }
}
```

With the `instanceOf` operator, we can get the type of the error that occurred. From there we can branch out how to handle the error.

## Custom Error
When developing an application, there will be many possible errors. Often, we need our own error class to indicate a specific error which is not available in JavaScript's built-in Error class.

Let's take another look at our previous code.
```js
let json = '{ "age": 30 }';
 
try {
    let user = JSON.parse(json);
 
    if (!user.name) {
        throw new SyntaxError("'name' is required.");
    }
 
    console.log(user.name);
    console.log(user.age);
} catch (error) {
    if (error instanceof SyntaxError) {
        console.log(`JSON Error: ${error.message}`);
    } else if (error instanceof ReferenceError) {
        console.log(error.message);
    } else {
        console.log(error.stack);
    }
}
```

Initially, `JSON.parse` will convert String data to object. If the String format does not match, then the function will throw a `SyntaxError`. Even if the format or syntax of the json string is appropriate, there is still a possibility that the data in it is incomplete. Currently we are still using SyntaxError to flag errors due to incomplete data, even though syntactically there is no problem with the json variable. Surely it would be better if we had a more specific Error, right?

For that we can create our own Error class with a more appropriate name and message. This class is an instance of the existing Error class. For example, to check data validation from json, we can create an Error class like this:
```js
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = "ValidationError";
    }
}
```

The ValidationError class has a constructor parameter in the form of a `message` that contains a detailed message regarding the error. Let's see how it applies to the previous code.
```js
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = "ValidationError";
    }
}
 
let json = '{ "age": 30 }';
 
try {
    let user = JSON.parse(json);
 
    if (!user.name) {
        throw new ValidationError("'name' is required.");
    }
    if (!user.age) {
        throw new ValidationError("'age' is required.");
    }
 
    console.log(user.name);
    console.log(user.age);
} catch (error) {
    if (error instanceof SyntaxError) {
        console.log(`JSON Syntax Error: ${error.message}`);
    } else if (error instanceof ValidationError) {
        console.log(`Invalid data: ${error.message}`);
    } else if (error instanceof ReferenceError) {
        console.log(error.message);
    } else {
        console.log(error.stack);
    }
}
 
/* output
Invalid data: 'name' is required.
*/
```

Now the code for handling errors is better, right? Using `instanceOf` will give more detailed error results and correspond to the error that occurred.