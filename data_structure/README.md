# Data Structure
## Object
Object is able to store values of various data types and form more complex data. To assign an object to a variable we use curly braces `{}`.
```js
const user = {};
```

Objects contain key and value pairs which are also known as properties. Key acts much like the name of a variable that holds a value. Meanwhile, value contains values with any data type including other objects. The keys and values in the object are written as follows:
```js
let object = {key1: "value1", key2: "value2", key3: "value3"}
```

The key must be a string and be written before a colon (:), followed by the value. Even though the key is a string, we don't need to write quotation marks unless there are special characters such as spaces.

To access the value of an object's property, we can call the object's name and then a period followed by the property name. Example:
```js
const user = {
    firstName: "Luke",
    lastName: "Skywalker",
    age: 19,
    isJedi: true,
};

console.log(`Halo, my name is ${user.firstName} ${user.lastName}`);
console.log(`I am ${user.age} years old`);

/* output
Halo, my name is Luke Skywalker
I am 19 years old
*/
```

In addition to the dot operator, we can also access the properties of an object using brackets or square brackets.
```js
user["home world"];
```

To access keys that have spaces or other special characters, we need to use brackets as above.
```js
const user = {
    firstName: "Luke",
    lastName: "Skywalker",
    age: 19,
    isJedi: true,
    "home world": "Tattooine"
};
console.log(`Halo, my name is ${user.firstName} ${user.lastName}`);
console.log(`I am ${user.age} years old`);
console.log(`I am from ${user["home world"]}`);
/* output
Halo, my name is Luke Skywalker
Umur saya 19 tahun
I am from dari Tattooine
*/
```

To change the value of a property in an object, we use the assignment operator (=).
```js
const spaceship = {
    name: "Millenium Falcon",
    manufacturer: "Corellian Engineering Corporation",
    maxSpeed: 1200,
    color: "Light gray"
};

spaceship.color = "Glossy red";
spaceship["maxSpeed"] = 1300;
console.log(spaceship);

/* output
{
  name: 'Millenium Falcon',
  manufacturer: 'Corellian Engineering Corporation',
  maxSpeed: 1300,
  color: 'Glossy red'
}
*/
```

Wait a minute. The `spaceship` object is declared as `const`, but why can we change its value?

Noteworthy is changing the different values by reinitializing the values. When we create an object, we are not bound by the properties in it so we can still modify its values. It's different if we reinitialize the variable from object.

```js
const spaceship = {
    name: "Millenium Falcon",
    manufacturer: "Corellian Engineering Corporation",
    maxSpeed: 1200,
    color: "Light gray"
};
 
spaceship = { name: "New Millenium Falcon" }; // Error
```

We can also delete properties on objects using the delete keyword as follows:
```js
const spaceship = {
    name: "Millenium Falcon",
    manufacturer: "Corellian Engineering Corporation",
    maxSpeed: 1200,
    color: "Light gray"
};

spaceship.color = "Glossy red";
spaceship["maxSpeed"] = 1300;

delete spaceship.manufacturer;

console.log(spaceship);

/* output
{ name: 'Millenium Falcon', maxSpeed: 1300, color: 'Glossy red' }
*/
```

## Array
Array is a data type that can group more than one value and place them in one variable. Example:
```js
let myArray = ["Cokelat", 42.5, 22, true, "Programming"];
console.log(myArray);

/* output:
[ 'Cokelat', 42.5, 22, true, 'Programming' ]
*/
```

The difference between an array and an object is that the data in the array is arranged sequentially and accessed using an index. To access the values in the array, we use square brackets `[]` which contain a number that represents the position of the value we want to access.

```js
console.log(myArray[1]);
```

If we access the array value more than its index, then the result will be `undefined`. The last index of an array is always the sum of the array values - 1.
```js
let myArray = ["Coklat", 42.5, 22, true, "Programming"];
console.log(myArray[0]);
console.log(myArray[1]);
console.log(myArray[2]);
console.log(myArray[3]);
console.log(myArray[4]);
console.log(myArray[5]);
console.log("Length of myArray is " + myArray.length + ".");

/* output:
Coklat
42.5
22
true
Programming
undefined
Length of myArray is 5.
*/
```

To add data to the array, we can use the `push()` method. This push function will add data at the end of the array.
```js
const myArray = ["Coklat", 42.5, 22, true, "Programming"];

myArray.push('JavaScript');
console.log(myArray);

/* output
[ 'Coklat', 42.5, 22, true, 'Programming', 'JavaScript' ]
*/
```

Meanwhile, to remove the last data or element from the array, we can use the `pop()` method.
```js
const myArray = ["Orange", 42.5, 22, true, "Programming"];

myArray.pop();
console.log(myArray);

/* output
[ Orange, 42.5, 22, true ]
*/
```

Other methods we can use to manipulate data in an array are `shift()` and `unshift()`. The `shift()` method is used to remove the first element from the array, while `unshift()` is used to add an element at the beginning of the array.
```js
const myArray = ["Cokelat", 42.5, 22, true, "Programming"];

myArray.shift();
myArray.unshift("Apple");

console.log(myArray);

/* output
[ 'Apple', 42.5, 22, true, 'Programming' ]
*/
```

We can use `delete` keyword to remove data from the Array.
```js
const myArray = ["Cokelat", 42.5, 22, true, "Programming"];

delete myArray[1];
console.log(myArray);

/* output
[ 'Apple', <1 empty item>, 22, true, 'Programming' ]
*/
```

To remove an element, use the `splice()` method like this:
```js
const myArray = ["Cokelat", 42.5, 22, true, "Programming"];

myArray.splice(2, 1);   // Delete from index 2 for 1 element
console.log(myArray);

/* output
[ 'Cokelat', 42.5, true, 'Programming' ]
*/
```

## Spread Operator
As the name implies "spread", this feature is used to spread the value of an array or rather an iterable object into several elements. Spread operators are written with three dots (`...`). Let's look at the following code example:
```js
// With array
const favorites = ["Seafood", "Salad", "Nugget", "Soup"];
 
console.log(favorites);
 
/* output
[ 'Seafood', 'Salad', 'Nugget', 'Soup' ]
*/

// With spread
const favorites = ["Seafood", "Salad", "Nugget", "Soup"];

console.log(...favorites);

/* output
Seafood Salad Nugget Soup
*/

// The equivalent
console.log(favorites[0], favorites[1], favorites[2], favorites[3]);
```

The spread operator can be used to combine two arrays into a new array. If you don't use this spread operator then the result will be like this:
```js
const favorites = ["Seafood", "Salad", "Nugget", "Soup"];
const others = ["Cake", "Pie", "Donut"];

const allFavorites = [favorites, others];

console.log(allFavorites);

/* output
[
  [ 'Seafood', 'Salad', 'Nugget', 'Soup' ],
  [ 'Cake', 'Pie', 'Donut' ]
]
*/
```

If we use the spread operator:
```js
const favorites = ["Seafood", "Salad", "Nugget", "Soup"];
const others = ["Cake", "Pie", "Donut"];

const allFavorites = [...favorites, ...others];

console.log(allFavorites);

/* output
[ 'Seafood', 'Salad', 'Nugget', 'Soup', 'Cake', 'Pie', 'Donut' ]
*/
```

In addition to arrays, the spread operator can also be used for object literals. This allows us to combine multiple objects with more concise code.
```js
const obj1 = { firstName: 'Obi-Wan', age: 30 };
const obj2 = { lastName: 'Kenobi', gender: 'M' };

const newObj = { ...obj1, ...obj2 };

console.log(newObj);

/* output
{ firstName: 'Obi-Wan', age: 30, lastName: 'Kenobi', gender: 'M' }
*/
```

## Destructuring Object & Array
JSON (JavaScript Object Notation) is the most popular data format used in data transactions today.
```json
[
    {
        "id": 14,
        "title": "Belajar Fundamental Aplikasi Android",
        "author": "Google ATP"
    },
    {
        "id": 51,
        "title": "Belajar Membuat Aplikasi Android untuk Pemula",
        "author": "Google ATP"
    },
    {
        "id": 123,
        "title": "Belajar Dasar Pemrograman Web",
        "author": "Dicoding Indonesia"
    },
    {
        "id": 163,
        "title": "Belajar Fundamental Front-End Web Development",
        "author": "Dicoding Indonesia"
    }
]
```

**What exactly is destructuring objects and arrays?** Destructuring in JavaScript is a syntax that can output values from arrays or properties of an object into smaller units.
```js
// Array
const foods = ['Pie', 'Cake', 'Honey']
 
const myFood = foods[0]
const yourFood = foods[1]
const ourFood = foods[2]
 
console.log(myFood, yourFood, ourFood)
 
/* output:
Pie Cake Honey
*/

// Object
const profile = {
    firstName: "John",
    lastName: "Doe",
    age: 18
}
 
const firstName = profile.firstName
const lastName = profile.lastName
const age = profile.age
 
console.log(firstName, lastName, age)
 
/* output:
John Doe 18
*/
```

The code will extract the value that is in the profile object and store it in a local variable that has the same name as the property in the profile object.

## Destructuring Object
Writing the destructuring object syntax in ES6 uses an object literal (`{ }`) on the left side of the assignment operator.
```js
const profile = {
    firstName: "John",
    lastName: "Doe",
    age: 18
}
 
const {firstName, lastName, age} = profile;
 
console.log(firstName, lastName, age);
 
/* output:
John Doe 18
*/
```

In the previous example, we have done destructuring object on variable declaration. However, in certain cases we may need to do this on a variable that has already been declared.
```js
const profile = {
    firstName: "John",
    lastName: "Doe",
    age: 18
}
 
let firstName = "Dimas";
let age = 20;
 
// initialize a new value via object destruction
({firstName, age} = profile);
 
console.log(firstName);
console.log(age);
 
/* output:
John
18
*/
```

When we destroy an object and assign a variable with a name that is not a property of the object, the value of that variable becomes `undefined`. For example:
```js
const profile = {
    firstName: "John",
    lastName: "Doe",
    age: 18
}
 
 
const {firstName, age, isMale} = profile;
 
console.log(firstName)
console.log(age)
console.log(isMale)
 
/* output:
John
18
undefined
*/
```

Alternatively, we can optionally define a default value for a particular property if it is not found. To do this, add an assignment sign (=) after the variable name and set the default value like this:
```js
const profile = {
    firstName: "John",
    lastName: "Doe",
    age: 18
}
 
 
const {firstName, age, isMale = false} = profile;
 
console.log(firstName)
console.log(age)
console.log(isMale)
 
/* output:
John
18
false
*/
```

If the property value is not found, the default value will be applied to the variable.

Actually in the process of destructuring the object we can use different local variable names. ES6 provides additional syntax that allows us to do just that. The writing is similar to when we create properties and their values on objects.
```js
const profile = {
    firstName: "John",
    lastName: "Doe",
    age: 18
}
 
const {firstName: localFirstName, lastName: localLastName, age: localAge} = profile;
 
console.log(localFirstName);
console.log(localLastName);
console.log(localAge);
 
 
/* output:
John
Doe
18
*/
```

## Destructuring Array
Destructuring arrays is similar to destructuring objects. Objects use curly braces `{}` while arrays use square brackets `[]`. Another difference is that destructuring arrays works by position rather than naming their properties. Here's an example of destructuring an array in ES6:
```js
const favorites = ["Seafood", "Salad", "Nugget", "Soup"];
 
const [firstFood, secondFood, thirdFood, fourthFood] = favorites;
 
console.log(firstFood);
console.log(secondFood);
console.log(thirdFood);
console.log(fourthFood);
 
/* output:
Seafood
Salad
Nugget
Soup
*/
```

We can also select values at certain indexes for destructuring the array. For example, if you want to retrieve the third value from an array, you don't need to set up a local variable to hold the value of the first, second, or fourth array. We can do this by leaving the array indexes we don't want empty (without writing local variables). Furthermore, a comma (,) is still needed to indicate the index position like this:
```js
const favorites = ["Seafood", "Salad", "Nugget", "Soup"];
 
const [, , thirdFood ] = favorites;
 
console.log(thirdFood);
 
/* output:
Nugget
*/
```

We can also perform destructuring assignments on arrays. However, unlike objects, we don't need to wrap them in parentheses. Examples are as follows:
```js
const favorites = ["Seafood", "Salad", "Nugget", "Soup"];
 
let myFood = "Ice Cream";
let herFood = "Noodles";
 
[myFood, herFood] = favorites;
 
console.log(myFood);
console.log(herFood);
 
/* output:
Seafood
Salad
*/
```

With array destructuring assignment, we can swap variable values easily without creating additional variables.
```js
let a = 1;
let b = 2;
 
console.log("Before swap");
console.log("Value a: " + a);
console.log("Value b: " + b);
 
[a, b] = [b, a]
 
console.log("After swap");
console.log("Value a: " + a);
console.log("Value b: " + b);
 
/* output
Before swap
Value a: 1
Value b: 2
After swap
Value a: 2
Value b: 1
*/
```

When destructuring an array, but there is a variable whose position cannot be reached by the array, then the variable will be undefined. For example:
```js
const favorites = ["Seafood"];
const [myFood, herFood] = favorites
 
console.log(myFood);
console.log(herFood);
 
/* output:
Seafood
undefined
*/
```

Just like objects, in destructuring arrays we can also assign default values to variables that cannot be reached by arrays, so that the value of the variable will not be undefined.
```js
const favorites = ["Seafood"];
 
const [myFood, herFood = "Salad"] = favorites
 
console.log(myFood);
console.log(herFood);
 
/* output:
Seafood
Salad
*/
```

## Map
Map is a data type that stores a collection of data in a key-value format like Object. The difference is that Map allows keys with any data type, compared to Object which only allows keys of type String or Symbol.

To define Map use constructor as below:
```js
const myMap = new Map();
```

If you want to assign the value of the Map directly, use a multi-dimensional array like this:
```js
const myMap = new Map([
    ['1', 'a String key'],
    [1, 'a number key'],
    [true, true]
]);

console.log(myMap);

/* output
Map(3) { '1' => 'a String key', 1 => 'a number key', true => true }
*/
```

The first (outer) array stores each element or key-value pair of the Map. Then the array in it has two elements, where the first element is the key and the second array is the value.

Once we've created a Map object, we can get its value based on a specific key with the `get()` method. Then, to add a new key-value pair use the `set()` method. If we want to check if there is a certain key on it, we can use the `has()` method and we can use the `delete()` method do delete the key-value pair.
```js
const capital = new Map([
    ["Jakarta", "Indonesia"],
    ["London", "England"],
    ["Tokyo", "Japan"]
]);

console.log(capital.size);
console.log(capital.get("London"));
capital.set("New Delhi", "India");
console.log(capital.size);
console.log(capital.get("New Delhi"));
console.log(capital.has("New Delhi"));
console.log(capital.delete("New Delhi"));
console.log(capital.size);

/* output
3
England
4
India
true
true
3
*/
```

## Set
Set is a "set of values". What distinguishes Sets from other data structures is that the data in Sets is neither sequential nor indexed. In addition, the data in the Set is also unique and there is no duplication. Take a look at the Set declaration example below:
```js
const numberSet = new Set([1, 4, 6, 4, 1]);

console.log(numberSet);

/* output
Set(3) { 1, 4, 6 }
*/
```

To add data to a Set we can use the `add()` function.
```js
const numberSet = new Set([1, 4, 6, 4, 1]);
numberSet.add(5);
numberSet.add(10);
numberSet.add(6);

console.log(numberSet);

/* output
Set(5) { 1, 4, 6, 5, 10 }
*/
```

The `add()` function accepts only one argument. If you enter an array, it will be treated as a single element on its own. Duplicate values will be ignored.
```js
const numberSet = new Set([1, 4, 6, 4, 1]);
numberSet.add(5);
numberSet.add([10,2]);
numberSet.add(6);

numberSet.delete(4);

console.log(numberSet);

/* output
Set(4) { 1, 6, 5, [ 10, 2 ] }
*/
```
> Note that Set has no order or index, so the argument to the `delete` function is the value you want to delete, not the index.

## WeakMap & WeakSet
WeakMap is a variant of Map that supports garbage collection. Garbage collection is the process by which the JavaScript interpreter reclaims memory that is no longer “reachable” and unusable by the program. 

What we mean by weak in WeakMap is a reference to the stored value. If a value stored in WeakMap is no longer accessible or can no longer be accessed, the reference to its memory will be deleted.

The following are some of the things that distinguish between Map and WeakMap:
- The key of WeakMap must be an object or an array. Primitive values cannot be used as keys because they do not support garbage collection.
- WeakMap has `get()`, `set()`, `has()`, and `delete()` method. However, WeakMap doesn't belong to the iterable category so it doesn't have `keys()`, `values()`, or `forEach()` methods.
- WeakMap also does not have a `size` property. This is because the size of the WeakMap may change due to the garbage collection process.

Let's have a look at the sample code and the difference between Map and WeakMap.
```js
let visitsCountMap = new Map(); // Save list of user
 
function countUser(user) {
    let count = visitsCountMap.get(user) || 0;
    visitsCountMap.set(user, count + 1);
}
 
let jonas = { name: "Jonas" };
countUser(jonas);                // Add user "Jonas"
 
jonas = null;                    // Data object "Jonas" deleted
 
console.log(visitsCountMap);
 
/* output
Map(1) { { name: 'Jonas' } => 1 }
*/
```

When the `jonas` object reference is deleted by changing it to `null`, the map should no longer store user data (garbage collected). However, the fact is that Jonas data is still available in the Map. That is, the Jonas data is still stored in memory until we completely delete it.

It's different if we use WeakMap, when the `jonas` value is unreachable, the `jonas` object will be deleted from memory including the information stored in the WeakMap.
```js
let visitsCountMap = new WeakMap(); // Save list of user

function countUser(user) {
    let count = visitsCountMap.get(user) || 0;
    visitsCountMap.set(user, count + 1);
}

let jonas = { name: "Jonas" };
countUser(jonas);                // Add user "Jonas"

jonas = null;                    // Data object "Jonas" deleted

console.log(visitsCountMap);

/* output
WeakMap { <items unknown> }
*/
```

Like WeakMap, WeakSet is a weak reference version of Set. The differences between WeakSet and Set include:
- WeakSet cannot store primitive values.
- WeakSet is not an iterable and only has `add()`, `has()`, and `delete()` methods.
- WeakSet does not have a `size` property.