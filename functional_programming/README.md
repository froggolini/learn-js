## Functional Programming
The Functional Programming Paradigm is a programming paradigm in which the computational process is based on pure mathematical functions. Functional Programming (hereinafter referred to as FP) is written in a declarative style that focuses on "what to solve" rather than "how to solve" which is embraced by the imperative style.

As an illustration for those of you who don't know what declarative and imperative are further, please see the following code example.
```js
const names = ['Harry', 'Ron', 'Jeff', 'Thomas'];

const newNamesWithExcMark = [];

for(let i = 0; i < names.length; i++) {
  newNamesWithExcMark.push(`${names[i]}!`);
}

console.log(newNamesWithExcMark);

/* output:
   [ 'Harry!', 'Ron!', 'Jeff!', 'Thomas!' ]
*/
```

The code example above is one of the imperative code writing styles. Where the process of filling in the new array value (newNames) based on the old array (names) is done manually. This is the meaning of "how to solve", where we need to think about how to do the loop (`for`); when the loop must stop (`i < names.length`); how to insert new value into array (`newNamesWithExcMark.push`).

Let's look at the code with the same function but in a declarative style.
```js
const names = ['Harry', 'Ron', 'Jeff', 'Thomas'];

const newNamesWithExcMark = names.map((name) => `${name}!`);

console.log(newNamesWithExcMark);

/* output:
* [ 'Harry!', 'Ron!', 'Jeff!', 'Thomas!' ]
*/
```

We do not need to bother to think about manual ways to achieve a goal. No manual looping process; No need to know when to stop the loop; We just focus on "what to solve" aka what we want to complete or achieve.

JavaScript itself is a programming language that supports the FP paradigm. There are many Higher-Order Functions (we'll discuss this in detail later) that we can use as utilities, one of which is the array map() function above.

But FP is not just using the built-in High-Order Function. To understand the FP paradigm in depth, we first need to know what concepts are in it.

## Functional Programming Concepts
### Pure Function
Pure Function is the concept of creating a function that requires the function **not to depend on values that are outside the function or its parameters**. So no matter what the situation is, the function that is created always produces the same thing, except when the function is given a different parameter value.
```js
let PI = 3.14;

const hitungLuasLingkaran = (jariJari) => {
  return PI * (jariJari * jariJari); 
}

console.log(hitungLuasLingkaran(4)); // 50.24

PI = 5; // tidak sengaja nilai PI berubah

console.log(hitungLuasLingkaran(4)); // 80
```

The function cannot be said to be a pure function because it requires a value that is outside the function, namely the PI value. If the PI value changes, then the use of the function produces a different value even though the same parameter value is given.

So, how to make the function pure?
```js
const hitungLuasLingkaran = (jariJari) => {
  return 3.14 * (jariJari * jariJari); 
}

console.log(hitungLuasLingkaran(4)); // 50.24
console.log(hitungLuasLingkaran(4)); // 50.24
console.log(hitungLuasLingkaran(8)); // 200.96
console.log(hitungLuasLingkaran(8)); // 200.96
```

Besides being forbidden to depend on external values, pure functions are also **strictly forbidden to change external values either intentionally or unintentionally**. Pure function should not cause side effects (no side effect) when used.
```js
const createPersonWithAge = (age, person) => {
  person.age = age;
  return person;
};

const person = {
  name: 'Bobo'
};

const newPerson = createPersonWithAge(18, person);

console.log({
  person,
  newPerson
});

/**
 * Output:
 *  {
      person: { name: 'Bobo', age: 18 },
      newPerson: { name: 'Bobo', age: 18 }
    }
*/
```

The `createPersonWithAge` function creates a new person object with the addition of the `age` property of the existing `person` object. But instead of just creating a new object, it also changes the value of the old object. Well, this is why the `createPersonWithAge` function is not a pure function.

Then how to make the function pure?
```js
const createPersonWithAge = (age, person) => {
  return { ...person, age };
};

const person = {
  name: 'Bobo'
};

const newPerson = createPersonWithAge(18, person);

console.log({
  person,
  newPerson
});

/**
 * Output:
 *  { 
 *    person: { name: 'Bobo' },
 *    newPerson: { name: 'Bobo', age: 18 } 
 *  }
*/
```

To make it easier to know whether the function you created is pure or not, make sure these 3 concepts exist in the function you create.
- Returns the same value when the inputs (parameter values) are the same.
- Depends only on the arguments given.
- Does not cause side effects.

If the 3 concepts above are met, then you can be sure you create a pure function.

### Immutability
Immutable means that an object cannot be changed after it has been created. Contrast with mutable which means that objects can be changed after they are created.

The concept of immutability is very thick in the FP paradigm. You can see earlier in the example of using an array map. When using `array.map()`, instead of changing the values of the array itself, it creates or generates a new array.
```js
const names = ['Harry', 'Ron', 'Jeff', 'Thomas'];

const newNamesWithExcMark = names.map((name) => `${name}!`);

console.log({
    names,
    newNamesWithExcMark,
});

/**
 * {
     names: [ 'Harry', 'Ron', 'Jeff', 'Thomas' ],
     newNamesWithExcMark: [ 'Harry!', 'Ron!', 'Jeff!', 'Thomas!' ]
   }
 */
```

So, what if we really need to change the value of an object? Examples like this:
```js
const user = {
    firstname: 'Harry',
    lastName: 'Protter', // ups, typo!
}

const renameLastNameUser = (newLastName, user) => {
    user.lastName = newLastName;
}

renameLastNameUser('Potter', user);

console.log(user);

/**
* output:
* { firstname: 'Harry', lastName: 'Potter' }
* 
*/
```

Yup! Your goal is achieved but that is not the concept of the FP paradigm. If you want to fully implement FP, avoid the method above. So what's the solution? Just like the `map()` array function, instead of changing the object values directly, apply those changes to the return values in the new object.
```js
const user = {
    firstname: 'Harry',
    lastName: 'Protter', // ups, typo!
}

const createUserWithNewLastName = (newLastName, user) => {
    return { ...user, lastName: newLastName }
}

const newUser = createUserWithNewLastName('Potter', user);

console.log(newUser);

/**
* output:
* { firstname: 'Harry', lastName: 'Potter' }
* 
*/
```

The result is the same right? Apart from that, you can also customize the function name from `renameLastNameUser` to `createUserWithNewLastName`. It is necessary to indicate that the function returns or generates a new user object.

### Recursive
Recursion is a technique in which a function calls itself.

We will try to change the countDown function which we usually create using iteration syntax such as for, foreach, while as in the code below into recursive form.
```js
const countDown = start => {
  do {
    console.log(start);
    start -=1;
  }
  while(start > 0);
};
 
countDown(10);
```

So the recursive way is:
```js
const countDown = start => {
  console.log(start);
  if(start > 0) countDown(start-1);
};

countDown(10);
```

### Higher-Order Function
JavaScript has the ability to [First Class Functions](https://developer.mozilla.org/en-US/docs/Glossary/First-class_Function), so functions in JavaScript can be treated like data. We can store functions in variables, pass functions as parameters to other functions, and return functions in functions.
```js
const hello = () => {
  console.log('Hello!')
};

const say = (someFunction) => {
  someFunction();
}

const sayHello = () => {
    return () => {
        console.log('Hello!');
    }
}

hello();
say(hello);
sayHello()();

/**
* Hello!
* Hello!
* Hello!
*/
```

Because with its First Class Functions ability, we can create Higher-Order Functions easily. Higher-Order Functions are part of the concept of the FP paradigm. Higher-Order Functions are functions that can accept other functions as arguments; return a function; or even both.

The Higher-Order Function technique is commonly used to:
- Abstracting or isolating an action, event, or handling asynchronous flow using callbacks, promises, and more.
- Create utilities that can be used in various data types.
- Make a currying technique or function composition.

Array map() is an example of a Higher-Order Function in JavaScript. Because in its use, **it accepts one argument which is a function**.

Knowing that Higher-Order Functions exist, you can create your own version of the map() function!
```js
const names = ['Harry', 'Ron', 'Jeff', 'Thomas'];

const arrayMap = (arr, action) => {
  const loopTrough = (arr, action, newArray = [], index = 0) => {
    const item = arr[index];
    if(!item) return newArray;
    return loopTrough(arr, action, [...newArray, action(arr[index])], index + 1);
  }

  return loopTrough(arr, action);
}


const newNames = arrayMap(names, (name) => `${name}!` );

console.log({
    names,
    newNames,
});

/**
* output:
* {
*   names: [ 'Harry', 'Ron', 'Jeff', 'Thomas' ],
*   newNames: [ 'Harry!', 'Ron!', 'Jeff!', 'Thomas!' ]
* }
*/
```

## Reusable Function
By applying the concepts contained in the FP paradigm, the functions you create will be reusable. Since the function you create is a pure function, it will not be affected or affect the state on/from the outside. This of course allows the function to be used over and over again without worrying about getting results beyond your expectations.

### Array Map
The `array.map()` function is a very useful and widely used built-in function of arrays.
```js
['Harry', 'Ron', 'Jeff', 'Thomas'].map(() => { });
```

The callback function will be called as many times as the length of the array and will have access to the array index according to its iteration.
```js
['Harry', 'Ron', 'Jeff', 'Thomas'].map((name) => { });
```

The map function will return a new array. The value of each item in the returned array, is the return of its callback function. Because callback functions can access array items, developers usually use them to generate new values.
```js
const newArray = ['Harry', 'Ron', 'Jeff', 'Thomas'].map((name) => { return `${name}!`});

console.log(newArray);

/**
* [ 'Harry!', 'Ron!', 'Jeff!', 'Thomas!' ]
* 
*/
```

### Array Filter
Just like `array.map()`, the `array.filter()` function is a built-in function for data of type array in JavaScript. As the name implies, this function is very useful for filtering the existing array values. If you have a case where you want to omit some items in an array based on certain specifications, this function is perfect for you to use.

The way this function works is similar to `array.map()`. However, the callback function of this function must return a boolean. Where this boolean value is used to determine whether the array items pass the filter or not.

Just like the `map()` function, the `filter()` function will also return the filtered array in the form of a new array.
```js
const truthyArray = [1, '', 'Hallo', 0, null, 'Harry', 14].filter((item) => Boolean(item));

console.log(truthyArray);

/**
* output:
* [ 1, 'Hallo', 'Harry', 14 ]
* 
*/
```

Another example, use a filter to filter an array of student objects that are eligible for scholarships based on the scores obtained.
```js
const students = [
  {
    name: 'Harry',
    score: 60,
  },
  {
    name: 'James',
    score: 88,
  },
  {
    name: 'Ron',
    score: 90,
  },
  {
    name: 'Bethy',
    score: 75,
  }
];

const eligibleForScholarshipStudents = students.filter((student) => student.score > 85);

console.log(eligibleForScholarshipStudents);

/**
* output:
* [ { name: 'James', score: 88 }, { name: 'Ron', score: 90 } ]
* 
*/
```

### Array Reduce
Just like `array.map()`, `array.reduce()` is a built-in function of data type array that is used to execute the value for each element and display as a single value.
```js
arr.reduce(callback( accumulator, currentValue, [, index[, array]] )[, initialValue])
```

The callback function of this function can be processed to manipulate the currentValue data and store it in the accumulator. In addition, the reduce function also has an initial value that can be defined in the initialValue section.

An example of its use, for example, is when we want to add up the total student scores:
```js
const students = [
  {
    name: 'Harry',
    score: 60,
  },
  {
    name: 'James',
    score: 88,
  },
  {
    name: 'Ron',
    score: 90,
  },
  {
    name: 'Bethy',
    score: 75,
  }
];

const totalScore = students.reduce((acc, student) => acc + student.score, 0);

console.log(totalScore);

/**
* output:
* 313
* 
*/
```

### Array some
`array.some()` is a built-in function of arrays which is quite often used. This function will return a boolean value.
```js
arr.some(callback(element[, index[, array]])[, thisArg])
```

The resulting value is based on the statement whether there is at least one of the rows of values in the array passed based on the criteria that we write in the callback function.

An example of its use, suppose we want to find out whether in a series of numbers there are even numbers.
```js
const array = [1, 2, 3, 4, 5];
const even = array.some(element => element % 2 === 0);

console.log(even);

/** 
output true
**/
```

### Array find
Similar to `array.some()`, `array.find()` as the name implies is used to find out whether in a row of values there are values that match the criteria defined in the callback function.

What distinguishes `array.find()` with `array.some()`, find will return one value from the first element found based on certain criteria and will return an undefine value if no criteria are met in the array item.
```js
arr.find(callback(element[, index[, array]])[, thisArg])
```

For example, suppose we are going to search for a student with the name `James`.
```js
const students = [
  {
    name: 'Harry',
    score: 60,
  },
  {
    name: 'James',
    score: 88,
  },
  {
    name: 'Ron',
    score: 90,
  },
  {
    name: 'Bethy',
    score: 75,
  }
];

const findJames = students.find(student => student.name === 'James');
console.log(findJames);

/**
output
{ name: 'James', score: 88 }
**/
```

### Array sort
`array.sort()` is a built-in function for arrays that is useful for sorting values from a series of values. By default, the sort function converts all the values in a series to strings and sorts them in ascending order.
```js
arr.sort([compareFunction])
```

A simple example is as follows:
```js
const months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// output: [ 'Dec', 'Feb', 'Jan', 'March' ]

const array1 = [1, 30, 4, 1000, 101, 121];
array1.sort();
console.log(array1);
// output: [ 1, 1000, 101, 121, 30, 4 ]
```

The sorting example above is based on sorting the form of a string data type. Therefore, when we want to sort according to the criteria we want (by date or based on student grades) then we need to create a separate compare function.
```js
const array1 = [1, 30, 4, 1000];

const compareNumber = (a, b) => {
  return a - b;
};
const sorting = array1.sort(compareNumber);
console.log(sorting);

/**
output
[ 1, 4, 30, 1000 ]
**/
```

In the compare function, the function will compare 2 values which will produce 3 results, namely negative (-), 0, and positive (+).
- If, is negative then `a` will be placed before `b`
- If, is positive then `b` will be placed before `a`
- If, 0 then there is no change in position.

### Array every
`array.every()` is the default function of array which is used to check whether all values of an array match the defined criteria. The return of `array.every()` is a Boolean value.
```js
arr.every(callback(element[, index[, array]])[, thisArg])
```

For example, we will check whether a student has passed all the material tests:
```js
const scores = [70,85,90];
const minimumScore = 65;

const examPassed = scores.every(score => score >= minimumScore);
console.log(examPassed);

/**
output
true
**/
```

### Array forEach
The forEach array is a built-in function of the array that serves to call the callback function on each iteration of the array index. Unlike the other array functions we've discussed, this function doesn't return any values. So this function literally only serves to call the callback function, nothing more.

Through this function, you can change the syntax of the loop based on the number of arrays from imperative to declarative.
- The imperative way.

    ```js
    const names = ['Harry', 'Ron', 'Jeff', 'Thomas'];
    
    for(let i = 0; i < names.length; i++) {
    console.log(`Hello, ${names[i]}!`);
    }
    
    /**
    * output:
    * Hello, Harry!
    * Hello, Ron!
    * Hello, Jeff!
    * Hello, Thomas!
    * 
    */
    ```
- The declarative way.
    ```js
    const names = ['Harry', 'Ron', 'Jeff', 'Thomas'];
    
    names.forEach((name) => {
    console.log(`Hello, ${name}`);
    });
    
    /**
    * output:
    * Hello, Harry!
    * Hello, Ron!
    * Hello, Jeff!
    * Hello, Thomas!
    * 
    */
    ``` 

However, note that when using forEach, you cannot use the break or continue operators in the loop process (you can do this in a for loop). This also applies to map and filter functions.
```js
const names = ['Harry', 'Ron', 'Jeff', 'Thomas'];
 
for(let i = 0; i < names.length; i++) {
  if(names[i] === 'Jeff') continue; // Works!
  
  console.log(`Hello, ${names[i]}!`);
}
 
names.forEach((name) => {
  if(names[i] === 'Jeff') continue; // Didn't work!
  console.log(`Hello, ${name}`);
});
```