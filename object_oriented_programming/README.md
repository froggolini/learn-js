# Object-Oriented Programming (OOP)
## Introduction to OOP
Object Oriented Programming (OOP) is one of the paradigms in the world of computer programming. It is an object-based approach, where an object consists of a collection of attributes and methods in it. In JavaScript, attributes are variables used to store values. While a method is a function that is used to run a process.

Previously we have known and studied objects that can represent a data layer. If a string is analogous to a word (a set of characters), a number as a number, and a boolean as a true or false statement; then the object is analogous to a more complex object. OOP is the same, but more complex because in the OOP paradigm there are 4 main pillars, namely encapsulation, abstraction, inheritance, and polymorphism.

For example, we have a data object named mail as in the example below.
```js
const mail = {
    from: "pengirim@dicoding.com",
    sendMessage: function (msg, to) {
        console.log(`you send: ${msg} to ${to} from ${this.from}`);
    }
};
 
console.log(mail.from);
mail.sendMessage('apakabar', 'penerima@dicoding.com');
 
/**
output:
you send: apakabar to penerima@dicoding.com from pengirim@dicoding.com
**/
```

The above object has an attribute with a string data type (`from`) and a function or method to send a message (`sendMessage`). In addition we can also change the content of one of the attributes of the object. For example:
```js
mail.from = "sender2@dicoding.com";
```

Or, add a new function called saveContact.
```js
mail.saveContact = function(addr) {
  console.log(`email saved ${addr}`);
}
```
The example above is written in the style of an object literal format, namely writing an object by directly writing its key and value in the created Object. These things do not fully encapsulate the concept of objects in OOP.

Instead, in OOP we will create a base template from an object, then from that base we can instantiate it in various forms of objects. Below is an illustration where Mail is the base template and sms, email, mailgroup are instances of Mail.

## Class
Classes are very important in object-oriented programming. That's because the class provides information about an object. So it can be said that an object is an instance of a class. Class itself in the OOP paradigm is technically a blueprint in defining the characteristics of an object. For example, suppose there is a blueprint for defining a `Mail` object. Where `sms` and `postman` are objects of the `Mail` class.

| Class Name | Mail |
| - | - |
| Characteristics | sender, recipient, message body |
| Capabilities/actions | send message, receive message |

Inside a class, it can consist of properties and methods. Properties are characteristics of the class, while methods are the capabilities or capabilities possessed by the class.

Let's first see how to create a class using the function syntax.
- Using the Prototype approach.

    ```js
    function Mail() {
        this.from = 'pengirim@dicoding.com';
    };
    
    Mail.prototype.sendMessage = function n(msg, to) {
    console.log(`you send: ${msg} to ${to} from ${this.from}`);
    };
    ```
- Without Prototype approach.
    ```js
    function Mail(){
        this.from = "pengirim@dicoding.com",
    this.sendMessage = function(msg, to) {
        console.log(`you send: ${msg} to ${to} from ${this.from}`);
    } 
    };
    ```

And here is how to call it:
```js
const mail1 = new Mail();
mail1.sendMessage('hallo', 'penerima@dicoding.com');
 
/**
output:
you send: hallo to penerima@dicoding.com from pengirim@dicoding.com
**/
```

Here is the differences:
- Using Prototype:

    ![Prototype](https://d17ivq9b7rppb3.cloudfront.net/original/academy/202104291708028182f37d1e301452f6f7a1bc1e1d1162.jpeg)
- Without Prototype:

    ![Without Prototype](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20210429170824c6515f8e38ba4b0cd9bfa8b00ab00abc.jpeg)

Prototype is an internal property that will always exist when an object is created. Of the two approaches, the call to the property can be done in the same way. However, the implementation of the prototype is preferred. the syntax below.
```js
// using prototype
const mail = new Mail();
mail.hasOwnProperty('sendMessage');
// result = false
 
--------
 
// without prototype
const mail = new Mail();
mail.hasOwnProperty('sendMessage');
// result = true
```

When we instantiate other objects, the object using the prototype does not copy the sendMessage attribute to each object. It's different when we don't use prototype, all attributes are copied to each object. Thus, the use of prototypes can save memory allocation used.

Continue to the second method, which is using class syntax.
```js
// Method 2
class Mail {
    constructor() {
        this.from = 'pengirim@dicoding.com';
    }
 
    sendMessage(msg, to) {
        console.log(`you send: ${msg} to ${to} from ${this.from}`);
    };
}
 
const mail1 = new Mail();
mail1.sendMessage('hallo', 'penerima@dicoding.com');
 
/**
output:
you send: hallo to penerima@dicoding.com from pengirim@dicoding.com
**/
```

The second way is basically using prototype, the use of class syntax in javascript is just syntatic sugar from the prototype itself.

## Property & Method Property
### Property
Property is an attribute of an object, the property itself can be a primitive data type--as previously discussed--it can even be in the form of objects and functions. For example, message content, recipient list, sender data, send orders, etc. As an example:
```js
// cara 1
class Mail {
    constructor() {
        this.from = 'pengirim@dicoding.com';
        this.contacts = [];
        this.yourOtherProperty = 'the values';
    }
    sendMessage(msg, to) {
        console.log(`you send: ${msg} to ${to} from ${this.from}`);
        this.contacts.push(to); // save new contact
    };
}
 
// cara 2
function Mail() {
    this.from = 'pengirim@dicoding.com';
    this.contacts = [];
    this.yourOtherPrototype = 'the values';
};
 
Mail.prototype.sendMessage = function (msg, to) {
    console.log(`you send: ${msg} to  ${to} from ${this.from}`);
    this.contacts.push(to); // save new contact
};
```

The example class above has 3 (three) properties and methods. What you need to remember, `this` is a representation that the designated variable is an attribute that is global and attached to the object. So, variables can be accessed from methods or properties in the class by adding this in front of it.
```js
class Mail {
    constructor() {
        this.from = 'pengirim@dicoding.com';
        this.contacts = [];
    }
    sendMessage(msg, to, from) {
        console.log(`you send: ${msg} to ${to} from ${from}`);
        // from here refers to the `from` parameter, not to the `from` of the global value i.e. sender@dicoding.com
        this.contacts.push(to);
    };
}

const mail1 = new Mail();
mail1.sendMessage('hallo', 'penerima@dicoding.com', 'aku@gmail.com');

/**
you send: hallo to penerima@dicoding.com from aku@gmail.com
**/
```

The example above shows that when we want to initialize or access a global attribute of a class, we must use `this.attributeName`.

In OOP itself, properties are divided into 2:
- Internal interface: methods and properties that can be accessed by other methods but cannot be fetched/executed outside the class.
- External interface: methods and properties that can be accessed outside the class itself.

While in JavaScript itself there are 2 types of access identifiers for a field:
- Public: can be accessed from anywhere.
- Private: can only be accessed from within the class itself.

By default, all defined attributes are public. So that all these attributes can be accessed by objects that have instantiated the class. As an example:
```js
const mail1 = new Mail();
mail1.from; // 'pengirim@dicoding.com'
mail1.contacts; // ['penerima@dicoding.com']
mail1.sendMessage('hallo', 'penerima@dicoding.com'); // message sending method
```

From this example, what if we want to change the `contacts` attribute which cannot be accessed directly by the instantiated object. We need to change a bit to our `Mail` class code:
```js
/** 
1st way, using var (can only be used in writing classes using the `function` statement)
**/
var contacts = [];
// example
function Mail() {
    this.from = 'pengirim@dicoding.com';
    var contacts = [];
}
 
/**
2nd way, this method can be used for writing classes using `function` and `class` . statements
**/
this._contacts = []
// example
class Mail {
    constructor() {
        this._contacts = [];
        this.from = 'pengirim@dicoding.com';
    }
}
 
/** 
3rd way, add prefix # , this method can be used for writing classes using only `class` statements 
**/
#contacts = [];
// example
class Mail {
    #contacts = [];
    constructor() {
        this.from = 'pengirim@dicoding.com';
    }
}
```

From the above example, when we want to access the contacts attribute directly through the initiating object, the return is undefined. These three methods can also be used in a method or function.
```js
const mail = new Mail();
mail.contacts; // undefined
```
> Be aware that the 2nd way is not the pure JavaScript way of setting private attributes. However, this method is a writing standard that is usually used by software developers (with JS) to distinguish variables that are private variables.

### Class Method
Class Method is a function or method in an object. To use it, a class must be instantiated into a new object that can be executed. In the mail class example above, we will use the `sendMessage` method, so we must instantiate `Mail` first.
```js
const mail1 = new Mail();
mail1.sendMessage('hallo', 'penerima@dicoding.com');
/**
output:
you send: hallo to penerima@dicoding.com from pengirim@dicoding.com
**/
```

We can't directly access `sendMessage` without instantiating it, for example:
```js
Mail.sendMessage('hallo', 'penerima@dicoding.com');
/**
output:
TypeError: Mail.sendMessage is not a function
**/
```

### Static Method
Static methods are functions or methods that are the same as class methods, but to access them there is no need to instantiate the class. We just need to write the class name and method name directly (`ClassName.MehodName()`).

For example, we added a method to check if an input is a mobile number:
```js
class Mail{
  static isValidPhone(phone) {
    return typeof phone === 'number';
  }
}
```

From the example above, we can call the function without instantiating the `Mail` class first.
```js
Mail.isValidPhone(089000000000) //true
```

### Constructor
A constructor is a method/function that is executed the first time an object is created. From the example class we created earlier, we will create from as a value that must be written when an object is initiated. So in JavaScript there are two ways, namely:
```js
// 1st way, if we use the class statement statement
class YourClassName{
  constructor(params1, params2, ....) {
    // do something here
  };
}
 
// 2nd way, if we use the function statement
function Mail(params1, params2, ....) {
    this.yourPropertyName = params1;
  // do something here
}
```

An example of its application is as follows:
```js
// 1st way
class Mail {
    constructor(author) {
        this.from = 'pengirim@dicoding.com';
        console.log('is instantiated', author);
    };
}
 
// 2nd way
function Mail(author) {
    this.from = author;
    console.log('is instantiated', author);
}
```

Since JavaScript is not a language with support for static types, we can actually instantiate parameters as we like:
```js
const mail1 = new Mail(085000111222); 
const mail2 = new Mail("emailku@dicoding.com"); 
```

## 4 Pillars of OOP
### Encapsulation
Encapsulation is a condition in which an attribute or method in a class is wrapped and is private. This means that other objects cannot access or change the value of the property directly. In the `Mail` case example, we can't directly change the contact list, but we can add it via a function when sending a message or retrieve the data via the `showAllContacts` method.
```js
class Mail{
    constructor(author) {
        this._contacts = [];
        this.from = author;
    }
    sendMessage = function(msg, to) {
        console.log('you send:', msg, 'to', to, 'from', this.from);
        this._contacts.push(to);
    }
    showAllContacts() {
        return this._contacts;
    }
}
```

### Abstraction
Abstraction is a natural application of encapsulation. Abstraction means that an object only performs high-level operations. For example, we know enough how messages are sent or received, but we don't need to know what the encryption and decryption process is like, or how a contact list can grow.

### Inheritance
Beberapa objek bisa memiliki beberapa karakteristik atau perilaku yang sama, tetapi mereka bukanlah objek yang sama. Di sinilah inheritance atau pewarisan berperan. SMS dan jenis pesan lainnya memiliki karakteristik umum yang dimiliki juga oleh jenis pesan lainnya, seperti memiliki konten pesan, alamat/nomor pengirim, alamat/nomor penerima, dsb. Maka dari itu, Email sebagai objek turunan (subclass) mewarisi semua sifat dan perilaku dari objek induknya (superclass) Mail. Begitu juga dengan objek Whatsapp juga mewarisi sifat dan perilaku yang sama. Namun, whatsapp bisa membuat grup, mengirim broadcast message sedangkan Email tidak.

![Example](https://d17ivq9b7rppb3.cloudfront.net/original/academy/20210331101812f297bf560a9a74da5feaa334a070eeab.png)

From the example above, suppose we want to create 2 (two) child classes, namely WhatsApp and Email. So in JavaScript, there are 2 ways to write inheritance, namely as follows:
```js
// 1st way: using the keyword `extends` if using the `class` . statement
class ChildClassName extends ParentClassName{}
 
 
// 2nd way: use `prototype` if using `function` / `class` . statements
ChildClassName.prototype = new ParentClassName()
```

Suppose we are going to create a child class named WhatsApp which inherits the Mail class.
```js
class Mail {
    constructor(author) {
        this.from = author;
        this._contacts = [];
    }
    sendMessage(msg, to) {
        console.log(`you send: ${msg} to ${to} from ${this.from}`);
        this._contacts.push(to);
    }
    showAllContacts() {
        return this._contacts;
    }
}

class WhatsApp extends Mail {
    constructor() {
        super();
        this.username = 'dicoding';
        this.isBussinessAccount = true;
    }
    myProfile() {
        return `my name ${this.username}, is ${this.isBussinessAccount ? 'Business' : 'Personal'}`;
    }
}

const wa1 = new WhatsApp(080111000222);
console.log(wa1.myProfile());
// my name dicoding, is Business
```

We can also access the attributes and methods of the parent class that is Accessible. For example:
```js
wa1.sendMessage('halo', 089000999888);
```

### Polymorphism
Polymorphism in Greek means "many forms". Simply put, objects can have different forms or implementations in the same method. All types of Mail can send messages, but whatsapp, email, sms of course have different ways of sending messages, for example: whatsapp can send voice messages while others can't, email can filter spam content when sending messages while others do not. The difference in the form or way of sending the message is an example of polymorphism.

## Overriding Method
Overriding is a technique for us to overhaul (whether in whole or not) on a method or constructor owned by the parent class. So, it can be adapted to the behavior in the child class.

### Overriding Constructor
```js
class WhatsApp extends Mail{
  constructor() {
    super();
    this.username = 'dicoding';
    this.isBussinessAccount = true;
  }
}
 
//pemanggilan
const wa1 = new WhatsApp(080111000222);
```

Now what if we add username and isBussinessAccount into the constructor? If we create a new constructor the code will be like this:
```js
class WhatsApp extends Mail {
    constructor(username, isBussinessAccount, phone) {
        super();
        this.username = username;
        this.isBussinessAccount = isBussinessAccount;
    }
}
 
const wa1 = new WhatsApp('dicoding', true, 089989090898);
/**
Error:
Must call super constructor in derived class before accessing 'this' or returning from derived constructor
**/
```

The error above occurs because the constructor in the parent class failed to execute, even though we have used the `this.nameOfProperty` operator. The solution is we can use the super() operator to execute the parent method. So, the constructor of the WhatsApp class looks like this.
```js
constructor(username, isBussinessAccount, phone) {
  super(phone);
  this.username = username;
  this.isBussinessAccount = true;
}
```

### Overriding Method
Sometimes we don't use a method completely the same as the parent class. However, we can add certain commands or reduce them. The following is an example of overriding the `sendMessage` method.
```js
class WhatsApp extends Mail {
    constructor(username, isBussinessAccount, phone) {
        super(phone);
        this.username = username;
        this.isBussinessAccount = isBussinessAccount;
    }
 
    // Overriding method => Total Override
    sendMessage(msg, to) {
        console.log('Send by WA');
    }
}
```

When we call the `sendMessage` method in the above example, it will only execute the code in the child class.
```js
const wa1 = new WhatsApp('di', true, 089000999888);
wa1.sendMessage('halo', 089000999888);
 
/**
Output:
Send by WA
**/
```

To continue executing code on the parent class, it is necessary to use the `super.methodName()` operator.
```js
sendMessage(msg, to) {
    super.sendMessage(msg, to);
    console.log('Send by WA');
}
```

Notes:
> `super(...)` digunakan untuk memanggil constructor parent dan hanya dapat digunakan di constructor.
> `super.methodName(...)` digunakan untuk memanggil parent method.

## Object Composition
Object composition is the principle of composition of a business flow without the need to inherit from the parent class. This principle is based on the set of behaviors (methods/functions) we have defined. So, when we want to create another business flow with some of the same behavior (method), we can use existing functions without doing inheritance.

Basically the concept to do is:
1. Separate commonly used functions.

    ```js
    const yourGenericAction = params => ({
    actionA: () => { /** do action A **/},
    actionB: () => { /** do action B **/},  
    });
    ```
2. Create a class as usual.
    ```js
    const YourClassName = (paramA, paramB) => {
    }
    ```
3. We can save the attributes that we have into an object, usually an engineer uses a constant with the name self or state to hold the attribute.
    ```js
    const YourClassName = (paramA, paramB) => {
    const self = {
        paramsA,
        paramsB
    };
    }
    ```
4. Add a behavior (method/function) that only exists in that class.
    ```js
    const YourClassName = (paramA, paramB) => {
    const self = {
        paramsA,
        paramsB
    };
    
    const yourSpecificActions = self => ({
        specificActinA: { /** do action A **/},
    });
    }
    ```
5. Make a collection of attributes, generic methods, and specific methods into one object.
    ```js
    const YourClassName = (paramA, paramB) => {
    const self = {
        paramsA,
        paramsB
    };
    
    const yourSpecificActions = self => ({
        specificActinA: { /** do action A **/},
    });
    
    return Object.assign(self, yourGenericAction(self), yourSpecificActions(self))
    }
    ```

For example, from the Mail hierarchy that we created earlier. we will remodel and make it approach Object composition.
```js
// [1] list of abstractions
const canSendMessage = self => ({
    sendMessage: () => console.log('send message:', self.message)
  });

const checkIsValidPhone = self => ({
    isValid: () => console.log('valid phone', self.from)
  });

// [2] crate object composition
const personalEnterprise = (from, message, store) => {
  // [3] attributes
  const self = {
    from,
    message,
    store
  };
  // [4] method
  const personalEnterpriseBehaviors = self => ({
    createCatalog: () => console.log('Catalog has created: ', self.store)
  });
  
  // [5] create object composition
  return Object.assign(self, personalEnterpriseBehaviors(self), canSendMessage(self), checkIsValidPhone(self));
};

const pe1 = personalEnterprise('pengirim@gmail.com', 'hei produk baru nih', 'Dicoding Store');
pe1.createCatalog(); //Catalog has created:  Dicoding Store
pe1.sendMessage(); //send message: hei produk baru nih
```

The description of the code above:
1. We create an abstraction for commonly used methods (here, for example the method of sending messages, and validating cellphone numbers).
2. We create a new class with the name personalEnterprise, where as usual we can use the parameters to be used.
3. In this composition object, the use of parameters is usually used to register the attributes of the class. In the example above, we collect the attribute in a constant named self or state.
4. Methods, we can also add specific methods/functions that only exist in that class (the capability is only for that class/not common).
5. The process of creating an object with the command Object.assign(attribute, method1, method2, methodN).

From the code example above, we can create an object with the name `personalEnterprise` without having to inherit.

## Built-in Class
Date is a built-in object from the JavaScript programming language that is used for utilities related to date and time. This is very helpful when in the program that we make there is the use and manipulation of date and time.

To use it we can instantiate the Date object in 4 ways:
```js
// #1 without parameters, which means `myDate` will contain the current date and time
const myDate = new Date(); 
 
// #2 date parameter in string form, for example "January 01, 2021"
const myDate = new Date(dateString); 
 
// #3 parameter in the form of a number, for example 87400000
const myDate = new Date(miliseconds); 
 
// #4 date parameters in the form of number (7 parameters), [hour,minute,second,millisecond] are optional
const myDate = new Date(year,month,date,hour,minute,second,millisecond); 
```

In the Date object there are several methods that we can use. The following is a list of commonly used methods.
| Methods | Explanation | Examples of usage | 
| - | - | - | 
| getMonth() | The return value is the month as a number (0 to 11), 0 being January. | myDate.getMonth() |
| getFullYear() | Return value is year, say 2021. | myDate.getFullYear() | 
| getDate() | The return value is the date from 1 to 31. | myDate.getDate()
| getHours() | The return value is hours from 0 to 23 | myDate.getHours()
| getMinutes() | The return value is minutes from 0 to 59 | myDate.getMinutes() | 
| getSeconds() | The return value is seconds from 0 to 59 | myDate.getSeconds() | 
| getMilliseconds() | Return value is milli-seconds from 0 to 999 myDate. | getMilliseconds() | 
getTime() | The return value is the time in milli-second epochs (starting from January 1, 1970 which means 0) | myDate.getTime() | 
getDay() | The return value is the day of the week from 0 to 6. 0 means the week | myDate.getDay() | 

In addition, there are also static methods that can be used without the need for instantiation, namely:
| Method | Explanation | Example Usage | 
| - | - | - |
| parse(datestring) | used to convert the date in string format, into milliseconds epochs | Date.parse("2021-01-01") |
| UTC(year, [..params]) | used to convert the date in string format, into milliseconds epochs | Date.UTC(2021, 01, 01) | 

### Date String Format
| Explanation | Format | 
| - | - | 
| YYYY | 4 digit year, for example: 2021 | 
| MM | 2 digit month, for example: 01 means January | 
| DD | 2 digits date 0 to 31 | 
| HH | 2 digit hours 0 to 23 | 
| mm | 2 digit minute 0 to 59 | 
| ss | 2 seconds seconds 0 to 49 | 
| sss | 3 digit millisecond 0 to 999 | 
| - | Separator for date | 
| : | separator for time | 
| Z | Means the date will be set as UTC | 

### Example Code
The following is the code, suppose we want to calculate how old we are by using the date object.
```js
// the birthday parameter can be either milliseconds or a date string
const myAge = birthday => {
  const birtday = new Date(birthday);
  const today = Date.now(); // today returns the current value of milliseconds
  
  const diff_ms = today - birtday.getTime(); // calculate the difference in the value of today's milliseconds and date of birth
  const diffDate = new Date(diff_ms);
  
  return diffDate.getFullYear() - 1970; // 1970 is the 0 representation of milliseconds
};

myAge('2000-01-22'); // 21 years old
```

Besides Date, we can also use other built-in javascript classes.
```js
const listOfContent = [1,2,”President”, {}];
console.log(Array.isArray(listOfContent)); 
// result is true
 
const splitText = "12:20:00".split(':');
// result is [ '12', '20', '00' ]
```

