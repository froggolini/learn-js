# Module
## Export & Import
In the Node.js environment, use the `module.exports` command to export the module. Every JavaScript file that runs on Node, has a local module object that has an exports property. These properties are used to define what values to export from the file.

Create a new file called **state.js** in your project. The code below is an example of how to export values using `module.exports`.
```js
const coffeeStock = {
  arabica: 100,
  robusta: 150,
  liberica: 200
}
 
module.exports = coffeeStock;
```

The code `module.exports = coffeeStock` creates a `coffeeStock` object set as the value of `module.exports`. The values of this exports property can later be imported and used in other JavaScript files.

If you try to view the existing module values in the **state.js** file by adding the `console.log(module)` code at the end of the file, then we will see the coffeeStock object being the value of the exports property.
```js
Module {
  id: '.',
  path: '/home/froggo/Learn/learn-js/module',
  exports: { arabica: 100, robusta: 150, liberica: 200 },
  parent: null,
  filename: '/home/froggo/Learn/learn-js/module/state.js',
  loaded: false,
  children: [],
  paths: [
    '/home/froggo/Learn/learn-js/module/node_modules',
    '/home/froggo/Learn/learn-js/node_modules',
    '/home/froggo/Learn/node_modules',
    '/home/froggo/node_modules',
    '/home/node_modules',
    '/node_modules'
  ]
}
```

Then how to import or use objects that have been exported? The trick is to use the `require()` method.
- `index.js`:

    ```js
    const coffeeStock = require('./state');
    
    console.log(coffeeStock);
    
    /* output
    { arabica: 100, robusta: 150, liberica: 200 }
    */
    ```
- `state.js`:
    ```js
    const coffeeStock = {
        arabica: 100,
        robusta: 150,
        liberica: 200
    };
    
    module.exports = coffeeStock;
    ```

In initializing the `coffeeStock` variable (the name of the independent variable we specify), we use the `require()` method by passing the **state.js** file location parameter. That way the coffeeStock variable will have the same `module.exports` value in the **state.js** file. After getting the value, we are free to use it like a local variable in general.
```js
const coffeeStock = require('./state');
 
const makeCoffee = (type, miligrams) => {
    if (coffeeStock[type] >= miligrams) {
        console.log("Kopi berhasil dibuat!");
    } else {
        console.log("Biji kopi habis!");
    }
}
 
makeCoffee("robusta", 80);
 
/* output
Kopi berhasil dibuat!
*/
```
> **Tip:** If you're using a relative location (changeable/moveable), make sure to start with ./. For example, the index.js and state.js files are in the same folder, so we can simply write them with ./state.js.

## Export Multiple Values in Node.js
Let's give an example by adding the `isCoffeeMachineReady` variable to the state.js file as follows:
```js
const coffeeStock = {
    arabica: 100,
    robusta: 150,
    liberica: 200
};
 
const isCoffeeMachineReady = true;
```

We can not export the two values above in the following way:
```js
module.exports = coffeeStock;
module.exports = isCoffeeMachineReady;
```

The second line of code means that we reinitialize the value of the `module.exports` property so that the only export value is the `isCoffeeMakerReady` variable.

The solution is that we export one value anyway, but we'll take advantage of **object literals** ({ }).
```js
module.exports = {coffeeStock, isCoffeeMachineReady}; 
```

If we look at the module values in the console, the value of the exports property is an object that holds the value of the `coffeeStock` object and the `isCoffeeMachineReady` variable.
```js
Module {
  id: '/home/froggo/Learn/learn-js/module/state.js',
  path: '/home/froggo/Learn/learn-js/module',
  exports: {
    coffeeStock: { arabica: 100, robusta: 150, liberica: 200 },
    isCoffeeMachineReady: true
  },
  parent: Module {
    id: '.',
    path: '/home/froggo/Learn/learn-js/module',
    exports: {},
    parent: null,
    filename: '/home/froggo/Learn/learn-js/module/index.js',
    loaded: false,
    children: [ [Circular *1] ],
    paths: [
      '/home/froggo/Learn/learn-js/module/node_modules',
      '/home/froggo/Learn/learn-js/node_modules',
      '/home/froggo/Learn/node_modules',
      '/home/froggo/node_modules',
      '/home/node_modules',
      '/node_modules'
    ]
  },
  filename: '/home/froggo/Learn/learn-js/module/state.js',
  loaded: false,
  children: [],
  paths: [
    '/home/froggo/Learn/learn-js/module/node_modules',
    '/home/froggo/Learn/learn-js/node_modules',
    '/home/froggo/Learn/node_modules',
    '/home/froggo/node_modules',
    '/home/node_modules',
    '/node_modules'
  ]
}
```

Then how to import these two values? Still remember the material destructuring object? In the index.js file we use the object destructuring technique to get the imported values like this:
```js
const {coffeeStock, isCoffeeMachineReady} = require('./state');
 
console.log(coffeeStock);
console.log(isCoffeeMachineReady);
 
/* output
{ arabica: 100, robusta: 150, liberica: 200 }
true
*/
```

## ES6 Module
In previous Node.js there was no difference between exporting one or more values. All values to be exported are converted to values from the module.exports property. In the ES6 module, if we export only one value in a JavaScript file be it a primitive value, function, array, object, or class, we use the `export default` keyword. Examples like this:
```js
const coffeeStock = {
    arabica: 100,
    robusta: 150,
    liberica: 200
};
 
export default coffeeStock;
```

Then to import the values we can use the `import … from` keyword as follows:
```js
import coffeeStock from "./state.js";
```

When using export default, we can use any name when declaring variables to store imported values.
```js
import stock from "./state.js";
```

Once we have successfully obtained the exported value, we can use the value like a local variable.
- `index.js`:

    ```js
    import coffeeStock from './state.js';
    
    const displayStock = stock => {
        for (const type in stock) {
            console.log(type);
        }
    }
    
    displayStock(coffeeStock);
    ```
- `state.js`:
    ```js
    const coffeeStock = {
        arabica: 100,
        robusta: 150,
        liberica: 200
    };
    
    export default coffeeStock;
    ```

An error will occur, it is because the JavaScript file that we created is not considered a module. Currently, the ES6 module feature is not enabled by default. The error message above mentions two ways how to activate the ES6 module. The two ways are to add properties to **package.json** or by changing the **.js** extension to **.mjs**. Let's use the first method which is simpler.
```js
{
  "name": "coffeemachine",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "type": "module",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js"
  },
  "author": "",
  "license": "ISC"
}
```

Add the **type** property with the **module** value in the **package.json** file. Then run your program again. Node.js should be running properly and displaying output like the following:
```js
arabica
robusta
liberica
```

Named export is used to export multiple values in a JavaScript file. It works similarly to Node.js. The values to be exported are written inside object literals, like this:
```js
const coffeeStock = {
    arabica: 100,
    robusta: 150,
    liberica: 200
};
 
const isCoffeeMachineReady = true;
 
export {coffeeStock, isCoffeeMachineReady};
```

Then to get the value exported via named export, we use destructuring object.
```js
import { coffeeStock, isCoffeeMachineReady } from './state.js';
 
console.log(coffeeStock);
console.log(isCoffeeMachineReady);
 
/* output
{ arabica: 100, robusta: 150, liberica: 200 }
true
*/
```

Because named imports use object destructuring techniques to get values, make sure the variable names match the exported variable names. If the names don't match, something like this will happen:
```js
import { stock, isCoffeeMachineReady } from './state.js';
 
/* output
SyntaxError: The requested module './state.js' does not provide an export named 'stock'
*/
```

However, if we still want to change the variable name from the named import, we can do so by adding the `as` keyword after the variable name.
```js
import { coffeeStock as stock, isCoffeeMachineReady } from './state.js';
 
console.log(stock);
console.log(isCoffeeMachineReady);
 
/* output
{ arabica: 100, robusta: 150, liberica: 200 }
true
*/
```

