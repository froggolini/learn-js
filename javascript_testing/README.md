# JavaScript Testing
## Introduction to JavaScript Testing
A software testing process can be done by:
- **Manual**

    The process of testing manually by a person appointed as a test, or some users who do get access to pre-release testing. This process is usually related to usability, accessibility of an application.
- **Automatic**

    The testing process is automatically carried out by the computer by writing a special script, usually carried out by a software engineer directly or by a QA Engineer. This process is usually related to the functionality of an application.

From the testing process above, the types of testing in software development in general can be divided into 4 types of tests, namely:
- Static test

    Ensures no typos (standard naming convention) and ensures no error types.

- Unit tests

    This is done to ensure that every unit of code that we write can work as expected. Unit itself means the smallest component that can be tested in isolation in the software we create, it can be a function or even a class if we use the OOP paradigm. This process can also be automated.

- Integration test

    Ensuring that several sets of functions that are interdependent on each other work properly. This testing process can be done automatically by writing a test script.

- End-to-End test

    The process of testing an application to test the flow from start to finish, like a user when using an application. Ensure that the application is functioning properly. Usually this process can be done automatically or manually by the tester.

When we write a test case (test case), then there are several points that we must define first:
- What do you want to test?

    For example: Performing tests on the function to calculate the average student score, or you can also test the account registration process, and so on.
- What are the expectations?
    - For the case of calculating the average value:
        - Generates the appropriate calculation output based on the given input.
        - The input must be a number.
    - For the case of account registration process:
        - Users can register normally.
        - Users with the same email cannot register.
        - and so forth.

## Jest
Jest is one of the most popular testing frameworks for writing test code in the JavaScript programming language. Jest can be used to write test scripts for backend and frontend applications.

We will try to write a test code using the jest framework.
1. Create a new project with a directory called practicetesting.

    ```bash
    $ mkdir latihantesting
    ```
2. Setelah masuk ke direktori tersebut, kita dapat melakukan init project kita.
    ```bash
    $ npm init
    ```
3. After the project is initialized. Next we can install the jest framework library.
    ```bash
    $ npm install --save-dev jest
    ```
4. After the installation process is complete, open the project in the code editor.
5. In the package.json file, we add a script to test by adding the following line of code:
    ```js
    {
    "scripts": {
        "test": "jest"
    }
    }
    ```
    The addition of the script is used so that we can run the test script which we will later create using the runner.

## Writing Test Code
From the previous project, we will try to start with the introduction of simple formats when we are going to write a test.
```js
test('deskripsi dari testcase kamu', () => {
    expect(perintah).matcher(nilai yang diekspektasikan);
});
 
// Example
test('dua tambah dua adalah empat', () => {
    expect(2+2).toBe(4);
});
```

From the code example above `expect(2 + 2)` is a segment that contains a command that produces a return value, the command can be a function or a direct command.

`toBe(4)`, called a matcher, contains the expected value of a previously executed command. In jest itself there are various matchers that can be used, for example:
| Matchers | Description |
| - | - | 
| toBe(x) | that the expected value is x | 
| toEqual(x) | that the expected value is equal to x | 
| toBeNull() | that the expected value is null | 
| toBeTruthy() | that the expected value is truth | 
| toBeFalsy() | that the expected value is false | 

In addition to the matchers above, you can also see other matchers that can be used here [https://jestjs.io/docs/using-matchers](https://jestjs.io/docs/using-matchers).

In the jest framework, we can also write a test in a grouping based on the same characteristics or groups using the `describe` segment, for example as follows:
```js
describe('pengujian olah aritmatika', () => {
    test('#1 dua tambah dua adalah empat', () => {
         expect(2+2).toBe(4);
    });
  
    test('#2 dua kali tiga adalah enam', () => {
         expect(2*3).toBe(6);
    });
 });
```

## Code Testing
Next, we will create 2 create functions for code testing based on the project that was created in the previous material. Note the sequence of steps below.

Create a file called **gradeCalculations.js** in the **latihantesting** folder.
```js
const averageExams = (valuesExam) => {
    const numberValidation = valuesExam.every(exam => typeof exam === 'number');
    if (!numberValidation) throw Error('please input number');
 
    const sumValues = valuesExam.reduce((accumulator,currentValue) => accumulator + currentValue, 0);
    return sumValues / valuesExam.length;
};
 
const isStudentPassExam = (valuesExam, name) => {
    const minValues = 75;
    const average = averageExams(valuesExam);
    
    if (average > minValues) {
        console.log(`${name} is fail the exams`);
        return true;
    } else {
        console.log(`${name} is pass the exams`);
        return false;
    }
};
 
module.exports = { averageExams, isStudentPassExam };
```

The code above has 2 functions:
- **averageExams** : Calculates the average value of students from an input in the form of a list of numbers in the form of an array.
- **isStudentPassExam** : Calculates whether a student passed the exam or not based on the average score obtained (depending on the averageExams function).

Writing test code can be done by starting the testcase framework that we mentioned above.
- What will be tested?
    - The function calculates the average.
    - Function to check whether a student passed the exam.
- Expected expectations?
    - Returns the appropriate value from the input.
    - The input must be a number.
    - Produce yes/no graduation results for students with certain criteria scores.

After we write the sample **gradeCalculations.js** code, the things that need to be done in writing test code using jest are as follows:
- Save the test script in a folder called __tests__.
- 1 test file for 1 command scope with the format **nameScopeFunctions.test.js**.

From the example above, all testcases of gradeCalculations are written in **gradeCalculations.test.js**.

Writing unit tests for `averageExams` code as follows:
```js
const { averageExams } = require('../gradeCalculations');
 
test('it should return exact average', () => {
    const listValueOfExams = [80, 100, 100, 80];
    expect(averageExams(listValueOfExams)).toEqual(90);
})
```

To run the test code, you can run the runner command that we created earlier.
```bash
$ npm run test
> latihantesting@1.0.0 test
> jest

 PASS  __tests__/gradeCalculations.test.js
  ✓ it should return exact average (4 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        0.228 s
Ran all test suites.
```

From the example above, we can see that the test case is as expected. In addition, we can also create multiple cases by making other tests, for example with the following code:
```js
test('it should handle non-number ', () => {
    const listValueOfExams = [80, 'a', '100', 80];
    expect(() => averageExams(listValueOfExams)).toThrow();
})
```

Integration tests can be run or written in conjunction with unit tests. So we can do the grouping of the code examples above into the following:
```js
const { averageExams, isStudentPassExam } = require('../gradeCalculations');
 
describe('grade calculations', () => {
    test('it should return exact average', () => {
        const listValueOfExams = [80, 100, 100, 80];
        expect(averageExams(listValueOfExams)).toEqual(90);
    });
 
    /**
     * Integration testing
     */
    test('it should return exam passed status', () => {
        const listValueOfExams = [80, 100, 100, 80];
        expect(isStudentPassExam(listValueOfExams, 'Budi')).toEqual(true);
    })
 
 
    test('it should return exam failed status', () => {
        const listValueOfExams = [50, 40, 70, 80];
        expect(isStudentPassExam(listValueOfExams, 'Budi')).toEqual(false);
    })
})
```

After writing down all the existing test cases, with jest we can see the code report that has been tested in the following way:
```bash
$ npm run test -- --coverage
```

After the process is complete, jest will automatically generate a test report in the **coverage** folder. In that folder there are:
- **index.html** contains the entire test report (1 project).
- **functionDiTest.js.html** contains test reports per test code.

