# Concurrency
## Synchronous vs Asynchronous
In a synchronous program, the code is executed sequentially from top to bottom. This means that if we write two lines of code, the second line of code cannot be executed before the first line of code is finished.

In an asynchronous program, if we write two lines of code, we can make the second line of code execute without having to wait for the code on the first line to finish executing.

Small tasks will be completed earlier than large tasks, even though large tasks are executed first.

![](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20210330171012e524970a1fb15c37ec815d68528c3dec.png)

An asynchronous program allows one operation to run while waiting for another operation to complete. We generally use asynchronous operations for large and time-consuming operations, such as retrieving data from the internet or an API, saving data to a database, and reading data from a file.

## setTimeout
The setTimeout() function is the easiest way to make our code run asynchronously. This function accepts two parameters. The first parameter is the function to be executed asynchronously. The second is the number value in milliseconds as the waiting value before the function is executed. An example of its use is like this:
```js
console.log("Selamat datang!");
setTimeout(() => {
  console.log("Terima kasih sudah mampir, silakan datang kembali!");
}, 3000);
console.log("Ada yang bisa dibantu?");
```

If we only know the program synchronously, then we can imagine the results have the following order:
- Printing -> Welcome!
- Wait for three seconds.
- Printing -> Thanks for dropping by, please come back!
- Printing -> Can anyone help?

However, in fact `setTimeout()` will not stop JavaScript from executing the next line of code. So the order is like this:
- Printing -> Welcome!
- Printing -> Can anyone help?
- Waiting for three seconds
- Printing -> Thanks for dropping by, please come back!

If the code is run, it will display output like the following:
```bash
$ node index.js 
Selamat datang!
Ada yang bisa dibantu?
Terima kasih sudah mampir, silakan datang kembali!
```

## Callback Function
The thing that is often confusing when working with synchronous and asynchronous programs is how to handle a value that is obtained asynchronously in a synchronously running program. An example is the following code:
```js
const orderCoffee = () => {
    let coffee = null;
    console.log("Sedang membuat kopi, silakan tunggu...");
    setTimeout(() => {
        coffee = "Kopi sudah jadi!";
    }, 3000);
    return coffee;
}
 
const coffee = orderCoffee();
console.log(coffee);
 
/* output
Sedang membuat kopi, silakan tunggu...
null
*/
```

If we do something like the above to print the coffee value, then it will never happen. As we already know, the `setTimeout()` function will not stop JavaScript from executing the next code. So, the `orderCoffee()` function will always return `null`, because the `return coffee` code will be executed first compared to `coffee = "Kopi sudah jadi!";`. Asynchronous code needs to be structured in a different way than synchronous. The most basic way is with a callback function.

What are callback functions? Let's think back to when we ordered coffee. In this case there may be two actions we can take:
- (Synchronous) We keep waiting at the cashier until the coffee comes.
- (Asynchronous) We wait at the table after ordering coffee. Then the coffee will be delivered by the waiter. So, we don't have to wait at the cashier and can do other work.

Well, in JavaScript, this server acts like a callback function. It is ordered to an asynchronous function which will then be called/used when the task is done.

How to implement it in code? First, we add a parameter with the name of the callback to the asynchronous function.
```js
const orderCoffee = callback => {
    let coffee = null;
    console.log("Sedang membuat kopi, silakan tunggu...");
    setTimeout(() => {
        coffee = "Kopi sudah jadi!";
    }, 3000);
    return coffee;
}
```

Then we call or use a callback that is filled with data to be brought (coffee) when the task is completed.
```js
setTimeout(() => {
    coffee = "Kopi sudah jadi!";
    callback(coffee);
}, 3000);
```

After using the callback, the function no longer needs to return a value. So, we can remove the `return coffee;` code. The whole function will look like this:
```js
const orderCoffee = callback => {
    let coffee = null;
    console.log("Sedang membuat kopi, silakan tunggu...");
    setTimeout(() => {
        coffee = "Kopi sudah jadi!";
        callback(coffee);
    }, 3000);
}
```

Then to use the orderCoffee function, change the code from:
```js
const coffee = orderCoffee();
console.log(coffee);
```

To:
```js
orderCoffee(coffee => {
    console.log(coffee);
});
```

So that when executed will be in accordance with our expectations.
```js
const orderCoffee = callback => {
    let coffee = null;
    console.log("Sedang membuat kopi, silakan tunggu...");
    setTimeout(() => {
        coffee = "Kopi sudah jadi!";
        callback(coffee);
    }, 3000);
}
 
 
orderCoffee(coffee => {
    console.log(coffee);
});
 
 
/* output
Sedang membuat kopi, silakan tunggu...
---- setelah 3 detik ----
Kopi sudah jadi!
*/
```

### Callback Hell
What if there are processes that depend on each other? For example, to make a cake the steps we need to do are:
1. Prepare materials
2. Making dough
3. Put the dough into the mold
4. Baking dough

These stages are highly dependent on each other. We cannot print the dough before preparing the ingredients and making the dough. If all these stages were running synchronously, maybe we could do it like this:
```js
function makeACake(...rawIngredients) {
    const ingredients = collectIngredients(rawIngredients);
    dough = makeTheDough(ingredients);
    pouredDough = pourDough(dough);
    cake = bakeACake(pouredDough);
    console.log(cake);
}
```

However, if these functions run asynchronously, then we will create a callback hell. Callback hell occurs because so many callback functions are nested because they need each other.
```js
function makeACake(...rawIngredients) {
    collectIngredients(rawIngredients, function(ingredients) {
        makeTheDough(ingredients, function(dough) {
            pourDough(dough, function(pouredDough) {
                bakeACake(pourDough, function(cake) {
                    console.log(cake);
                })
            })
        })
    });
}
```

So what is the solution so that we can avoid callback hell? One of them is to use Promise.
```js
function makeACake(...rawIngredients) {
    collectIngredients(rawIngredients)
        .then(makeTheDough)
        .then(pourDough)
        .then(bakeACake)
        .then(console.log);
}
```

With Promise, we can minimize callback hell and turn it into very readable code. Even with such code, even non-developers can understand what the code means.

## Promise
Promise is one of the important features of ES6. This promise can override the role of the callback by using the characteristic of its `.then` function.

This feature works as the name suggests, which is to make an appointment. Let's analogize again in the real world. When we order coffee from the waiter, the waiter indirectly promises us to make coffee and serve it to us. But a promise can only be a promise. Even in the real world, promises can also not be fulfilled, whether it's because our coffee order is empty, or the coffee maker is broken.

Well, Promise has the same behavior as the analogy above. Promise has three conditions, namely:
- Pending (Promise in progress)
- Fulfilled (Promise fulfilled)
- Rejected (Promises fail to fulfill)

## Constructing Promise Object
To create a promise object, we use the new keyword followed by the constructor of Promise:
```js
const coffee = new Promise();
```

In the Promise constructor, we need to define a resolver function or it can be called an executor function. The function will be executed automatically when the Promise constructor is called.
```js
const executorFunction = (resolve, reject) => {
    const isCoffeeMakerReady = true;
    if (isCoffeeMakerReady) {
        resolve("Kopi berhasil dibuat");
    } else {
        reject("Mesin kopi tidak bisa digunakan");
    }
}
 
 
const makeCoffee = () => {
    return new Promise(executorFunction);
}
const coffeePromise = makeCoffee();
console.log(coffeePromise);
 
 
/* output
Promise { 'Kopi berhasil dibuat' }
*/
```

Executor function has two parameters, namely resolve and reject which is a function. Here's a detailed explanation:
- **resolve()** is the first parameter of the executor function. This parameter is a function that can accept one parameter. Usually we use it to pass data when the promise is executed successfully. When this function is called, the condition of the Promise will change from **pending** to **fulfilled**.
- **reject()** is the second parameter of the executor function. This parameter is a function that can accept one parameter and is used to provide a reason why the Promise cannot be fulfilled. When this function is called, the Promise condition will change from **pending** to **rejected**.

The Executor function will run asynchronously until the Promise condition changes from **pending** to **fulfilled/rejected**.

In the code example above, the output would be like this:
```js
/* output
Promise { 'Kopi berhasil dibuat' }
*/
```

The executor function executes `resolve()` with the string data "Coffee was created successfully". If we change the value of the `isCoffeeMakerReady` variable to `false`, the executor function will execute `reject()` with a rejection message "The coffee machine cannot be used".
```js
/* output
Promise { <rejected> 'Mesin kopi tidak bisa digunakan' }
*/
```

## Consuming Promises
To handle the result of the Promise, we use the `.then()` method.
```js
const myPromise = new Promise(executorFunction);
myPromise.then(onFullfilled, onRejected);
```

`.then()` itself is a higher-order function that takes two parameters. Both are callback functions which are also known as handlers. The first handler is the function that will be executed when the Promise resolves. While the second handler is a function that will be executed when the Promise is reject status.

Let's create an object to hold the stock and a function that returns a Promise object.
```js
const stock = {
    coffeeBeans: 250,
    water: 1000,
}
 
const checkStock = () => {
    return new Promise((resolve, reject) => {
        if (stock.coffeeBeans >= 16 && stock.water >= 250) {
            resolve("Stok cukup. Bisa membuat kopi");
        } else {
            reject("Stok tidak cukup");
        }
    });
};
```

Then below that we add two functions to handle resolve and reject states, respectively.
```js
const handleSuccess = resolvedValue => {
    console.log(resolvedValue);
}
 
const handleFailure = rejectionReason => {
    console.log(rejectionReason);
}
```

Finally call the `.then()` method on `checkStock()` to handle the result returned from the promise.
```js
checkStock().then(handleSuccess, handleFailure);
```

So, the whole code will be like this:
```js
const stock = {
    coffeeBeans: 250,
    water: 1000,
}
 
const checkStock = () => {
    return new Promise((resolve, reject) => {
        if (stock.coffeeBeans >= 16 && stock.water >= 250) {
            resolve("Stok cukup. Bisa membuat kopi");
        } else {
            reject("Stok tidak cukup");
        }
    });
});
 
const handleSuccess = resolvedValue => {
    console.log(resolvedValue);
}
 
const handleFailure = rejectionReason => {
    console.log(rejectionReason);
}
 
checkStock().then(handleSuccess, handleFailure);
```

Let's dissect the code above:
- `checkStock()` is a function that returns a promise and will return `resolve()` with a value of "Stok cukup. Bisa membuat kopi."
- Then we declare the `handleSuccess()` and `handleFailure()` functions that print the values of the parameters.
- Then we call the `.then()` method of `checkStock`. Fill the `then()` parameter with the two handler functions we created earlier.
- The first parameter contains the handleSuccess function to handle the condition when the promise resolves. The second parameter contains the handleFailure function which handles when the promise has a reject state.

## onRejected with Catch Method
One way to write good code is to follow a principle called separation of concerns. Segregating the problem means organizing the code into different parts based on a specific task. This will make it easier for us to find the wrong code later if the application does not work properly.

Note that the `.then()` method returns the same promise value as when the promise object was called. By virtue of this nature, instead of assigning resolve and reject logic to one `then()` method, we can separate the two logics using each `then()` method like this:
```js
checkStock()
  .then(handleSuccess)
  .then(null, handleFailure);
```

However, to set the onRejected handler, we need to pass `null` in the first parameter of the `.then()` method. This is a little inconvenient isn't it? The solution we can use another method, namely `.catch()`.

The `.catch()` method is similar to the `.then()` method. However, this method only accepts one function parameter that is used for the rejected handler. This catch() method will be called when the promise object has an onRejected condition. The following is an example of using the `.catch()` method:
```js
checkStock()
  .then(handleSuccess)
  .catch(handleFailure);
```

By using the `catch()` method, we can apply the principle of separation of concerns while making the code neater.

## Chaining Promises
With promises we can perform asynchronous processes in a chain. To make sure that the promise set runs properly, we need to return the next promise. Examples are like this:
```js
function makeEspresso() {
    checkAvailability()
        .then((value) => {
            console.log(value);
            return checkStock();
        })
        .then((value) => {
            console.log(value)
            return brewCoffee();
        })
        .then((value) => {
            console.log(value);
        })
        .catch((rejectedReason) => {
            console.log(rejectedReason);
        });
}
 
makeEspresso();
```

First, the machine will check the availability status. If the coffee machine is not busy, the promise returns a `resolve("Mesin kopi siap digunakan")`. However, if the machine's status is still busy, the status is `reject("Maaf, mesin sedang sibuk")`.

Here is the code for the `checkAvailability()` function:
```js
const checkAvailability = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (!state.isCoffeeMachineBusy) {
                resolve("Mesin kopi siap digunakan.");
            } else {
                reject("Maaf, mesin sedang sibuk.");
            }
        }, 1000);
    });
};
```

In the code above, we use the `setTimeout()` function to simulate an asynchronous process and delay the process for 1 second (1000 milliseconds). The object to store the state of the coffee machine is like this:
```js
const state = {
    stock: {
        coffeeBeans: 250,
        water: 1000,
    },
    isCoffeeMachineBusy: false,
}
```

Then, the coffee machine needs to make sure that the stock of coffee beans and water is sufficient to make coffee. Here also we change the status of the coffee machine to busy.
```js
const checkStock = () => {
    return new Promise((resolve, reject) => {
        state.isCoffeeMachineBusy = true;
        setTimeout(() => {
            if (state.stock.coffeeBeans >= 16 && state.stock.water >= 250) {
                resolve("Stok cukup. Bisa membuat kopi.");
            } else {
                reject("Stok tidak cukup!");
            }
        }, 1500);
    });
};
```

Then the last promise function is a function to mix coffee and water and serve it in a glass. This function returns a promise with a resolve state that carries the value "Kopi sudah siap!".
```js
const brewCoffee = () => {
    console.log("Membuatkan kopi Anda...")
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("Kopi sudah siap!")
        }, 2000);
    });
};
```

The series of processes above run sequentially because we use the `.then()` method. If we read the code it will be something like this: "To make espresso, check the availability of the machine, **then** check the stock in the machine, **then** make coffee."

If the promise rejects, it will be handled by the `catch()` method we wrote at the end. Whether it's because the coffee machine is busy or the ingredients are out of stock.

Full code:
```js
const state = {
    stock: {
        coffeeBeans: 250,
        water: 1000,
    },
    isCoffeeMachineBusy: false,
}
 
const checkAvailability = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (!state.isCoffeeMachineBusy) {
                resolve("Mesin kopi siap digunakan.");
            } else {
                reject("Maaf, mesin sedang sibuk.");
            }
        }, 1000);
    });
};
 
const checkStock = () => {
    return new Promise((resolve, reject) => {
        state.isCoffeeMachineBusy = true;
        setTimeout(() => {
            if (state.stock.coffeeBeans >= 16 && state.stock.water >= 250) {
                resolve("Stok cukup. Bisa membuat kopi.");
            } else {
                reject("Stok tidak cukup!");
            }
        }, 1500);
    });
};
 
const brewCoffee = () => {
    console.log("Membuatkan kopi Anda...")
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("Kopi sudah siap!")
        }, 2000);
    });
};
 
function makeEspresso() {
    checkAvailability()
        .then((value) => {
            console.log(value);
            return checkStock();
        })
        .then((value) => {
            console.log(value)
            return brewCoffee();
        })
        .then(value => {
            console.log(value);
            state.isCoffeeMachineBusy = false;
        })
        .catch(rejectedReason => {
            console.log(rejectedReason);
            state.isCoffeeMachineBusy = false;
        });
}
 
makeEspresso();
 
/* output
Mesin kopi siap digunakan.
Stok cukup. Bisa membuat kopi.
Membuatkan kopi Anda...
Kopi sudah siap!
*/
```

## Promise All
When we go to a coffee shop with coworkers, we usually order coffee together. Even though the coffee we ordered was different, it was not uncommon for the service to deliver the order together. Well, in this case the server uses the `Promise.all()` technique.

The `Promise.all()` method can accept multiple promises in an array of parameters. Then the method will return the entire value of the promise in the form of an array.
```js
const promises = [firstPromise(), secondPromise(), thirdPromise()];
 
Promise.all(promises)
    .then(resolvedValue => {
        console.log(resolvedValue);
    });
 
/* output
[ 'first promise', 'second promise', 'third promise' ]
*/
```

In the case of coffee machines, we can add processes to heat water and grind coffee beans.
```js
const boilWater = () => {
    return new Promise((resolve, reject) => {
        console.log("Memanaskan air...");
        setTimeout(() => {
            resolve("Air panas sudah siap!");
        }, 2000);
    })
}
 
const grindCoffeeBeans = () => {
    return new Promise((resolve, reject) => {
        console.log("Menggiling biji kopi...");
        setTimeout(() => {
            resolve("Kopi sudah siap!");
        }, 1000);
    })
}
```

Both can run simultaneously. We will use `Promise.all()` to run both of the above functions before the `brewCoffee()` function. Change the `makeEspresso()` function code to something like this:
```js
function makeEspresso() {
    checkAvailability()
        .then((value) => {
            console.log(value);
            return checkStock();
        })
        .then(value => {
            console.log(value);
            const promises = [boilWater(), grindCoffeeBeans()];
            return Promise.all(promises);
        })
        .then((value) => {
            console.log(value)
            return brewCoffee();
        })
        .then(value => {
            console.log(value);
            state.isCoffeeMachineBusy = false;
        })
        .catch(rejectedReason => {
            console.log(rejectedReason);
            state.isCoffeeMachineBusy = false;
        });
}
 
makeEspresso();
 
/* output
Mesin kopi siap digunakan.
Stok cukup. Bisa membuat kopi.
Memanaskan air...
Menggiling biji kopi...
[ 'Air panas sudah siap!', 'Kopi sudah siap!' ]
Membuatkan kopi Anda...
Kopi sudah siap!
*/
```

When the above code is executed, we need to wait two (2) seconds for boilWater and grindCoffeeBeans to run (longest duration of the promise executed from Promise.all()). This indicates that all the promises in Promise.all() run concurrently and wait until all the processes in it finish executing.

What we need to note is that the order of values returned by this method corresponds to the promise we set in its parameters.
```js
/* output
[ 'Air panas sudah siap!', 'Kopi sudah siap!' ]
*/
```

## Async-await
As we know, writing asynchronous code is slightly different from synchronous processing. For example, to get the coffee value from an asynchronous process, we can't do it with a technique like this:
```js
function makeCoffee() {
    const coffee = getCoffee(); // async process using promise
    console.log(coffee);
}
 
makeCoffee();
```

Rather it should be like this:
- Promise:

    ```js
    function makeCoffee() {
        getCoffee().then(coffee => {
            console.log(coffee);
        });
    }
    
    makeCoffee();
    ```
- Callback:
    ```js
    function makeCoffee() {
        getCoffee(function(coffee) {
            console.log(coffee);
        });
    }
    
    makeCoffee();
    ```

However, since ES8 (ECMAScript 2017) we can write asynchronous processes like synchronous processes with the help of the `async` and `await` keywords.

The async/await feature is really just syntactic sugar. That means functionality is not a new feature in JavaScript. However, only a new writing style was developed from the combination of using Promise and [generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator). So, this async/await cannot be used if there is no Promise.

In the previous code sample, let's also look at the `getCoffee()` function and how it returns a promise.
```js
const getCoffee = () => {
    return new Promise((resolve, reject) => {
        const seeds = 100;
        setTimeout(() => {
            if (seeds >= 10) {
                resolve("Kopi didapatkan!");
            } else {
                reject("Biji kopi habis!");
            }
        }, 1000);
    })
}
```

To get the value from the `getCoffee()` function using `.then()`, our code would look like this:
```js
function makeCoffee() {
    getCoffee().then(coffee => {
        console.log(coffee);
    });
}
 
makeCoffee();
 
/* output
Kopi didapatkan!
*/
```

Async-await allows us to write asynchronous processes like synchronous processes. Approximately our program code will be like this:
```js
function makeCoffee() {
    const coffee = getCoffee();
    console.log(coffee);
}
 
makeCoffee();
 
/* output
Promise { <pending> }
*/
```

However, when the above code is executed the result will not be what we expected because the `getCoffee()` function is a Promise object. To wait for the `getCoffee()` function to run asynchronously, add the `await` keyword before calling the `getCoffee()` function.
```js
const coffee = await getCoffee();
```

Then, because the `makeCoffee()` function now handles asynchronous processes, it also becomes an asynchronous function. Add `async` before the function declaration to make it asynchronous.
```js
async function makeCoffee() { … }
```

With the above changes, we have successfully written an asynchronous process in synchronous style.
```js
async function makeCoffee() {
    const coffee = await getCoffee();
    console.log(coffee);
}
 
makeCoffee();
 
/* output
Kopi didapatkan!
*/
```

The `async` keyword is used to tell JavaScript to run the `makeCoffee()` function asynchronously. Then, the `await` keyword is used to stop further code reading until the `getCoffee()` function returns the value of the promise resolves.

### Handle onRejected using async-await
Note that `await` will only return a value if the promise is successful (onFulfilled). We can handle an error or rejection by using `try...catch`.

When using async/await, make it a habit when you get the resolved value of a promise, to place it in a try block like this:
```js
async function makeCoffee() {
    try {
        const coffee = await getCoffee();
        console.log(coffee);
    }
}
```

That way we can use a catch block to handle if the promise fails (onRejected).
```js
async function makeCoffee() {
    try {
        const coffee = await getCoffee();
        console.log(coffee);
    } catch (rejectedReason) {
        console.log(rejectedReason);
    }
}
 
makeCoffee();
 
/* output
Biji kopi habis!
*/
```

### Chaining Promise using async-await
With the async-await approach, our coffee machine code would look like this:
```js
async function makeEspresso() {
    try {
        await checkAvailability();
        await checkStock();
        const coffee = await brewCoffee();
        console.log(coffee);
    } catch (rejectedReason) {
        console.log(rejectedReason);
    }
}
 
makeEspresso();
 
/* output
Membuatkan kopi Anda...
Kopi sudah siap!
*/
```

Finally, to run multiple promises simultaneously with Promise.all, we can write them like this:
```js
async function makeEspresso() {
    try {
        await checkAvailability();
        await checkStock();
        await Promise.all([boilWater(), grindCoffeeBeans()]);
        const coffee = await brewCoffee();
        console.log(coffee);
    } catch (rejectedReason) {
        console.log(rejectedReason);
    }
}
```

