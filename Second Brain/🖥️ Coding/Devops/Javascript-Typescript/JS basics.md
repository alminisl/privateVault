---
banner_icon: 💻
banner: "https://coursework.vschool.io/content/images/size/w2000/2016/03/javascript-logo-banner.jpg"
banner_y: 0.928
---
```toc
```



# Intro 

Refreshing all the basics and things in JS 

[Most popular JS interview questions & answers | JS Remote jobs](https://jsremote.jobs/blog/javascript-interview-questions/)



## Event bubbling 

This is a thing where all the events are propagated to the parend DOM element. and that goes until it reaches the root parent. 

use `e.stopPropagation()` to make it not work. 

### AI Generated response 

Event bubbling is a mechanism in the DOM (Document Object Model) where an event that is triggered on an element is also propagated (or "bubbled up") to all its ancestor elements in the DOM tree. This means that if you have a nested set of elements, and an event is triggered on a child element, the event will also trigger on all of its ancestor elements, all the way up to the root element of the document.

Here's an example to illustrate the concept:

htmlCopy code

`<div id="outer">   <div id="inner">     <button id="button">Click me</button>   </div> </div>  <script>   const button = document.querySelector('#button');   const inner = document.querySelector('#inner');   const outer = document.querySelector('#outer');    button.addEventListener('click', function(event) {     console.log('Button clicked!');   });    inner.addEventListener('click', function(event) {     console.log('Inner div clicked!');   });    outer.addEventListener('click', function(event) {     console.log('Outer div clicked!');   }); </script>`

In this example, we have three nested elements: an outer `<div>`, an inner `<div>`, and a button element. We've added click event listeners to all three elements, with each listener logging a message to the console.

If we click the button element, we'll see that all three event listeners are triggered, and the messages are logged to the console in the following order:

cssCopy code

`Button clicked! Inner div clicked! Outer div clicked!`

This is because the button click event is propagated up the DOM tree, triggering the event listeners on all the ancestor elements.

Event bubbling can be useful in many scenarios. For example, it allows you to add a single event listener to a parent element, and handle events that occur on its child elements without having to add separate event listeners to each child. This can help simplify your code and make it more efficient.

However, event bubbling can also cause unintended behavior if you're not careful. For example, if you have multiple event listeners on nested elements that modify the same property of the same element, the order in which the events are triggered can affect the final outcome. In some cases, you may want to prevent event bubbling using the `event.stopPropagation()` method to ensure that only the intended event listener is triggered.


## Scopes 

```js
// Global Scope
var a = 1
let b = 2
const c = 3


// Block scope
if(true) {
 var a = 4
 let b = 5
 const c = 6
}

// Response from this is 
// block Scope = 4 5 6 
// global scope = 4 2 3
```

Using forloop

```js
for (let a = 0;a<10;a++) {
	console.log(a)
}

// Global scope = 1 
// With var a instead of let a = 10 

```


## Constructor and this keyword

```Js
[function Person(name, dob) {
	this.name = name
	this.birthday = new Date(dob)
	this.calculateAge = function() {
		const diff= date.now() - this.birthday.getTime()
		const ageDate = new Date(diff)
		return ageDate;
	}
}

const brad = new Person("test", '9-10-2000')
console.log(brad)](<function Person(name, dob) {
	this.name = name
	this.birthday = new Date(dob)
	this.calculateAge = function() {
		const diff= Date.now() - this.birthday.getTime()
		const ageDate = new Date(diff)
		return Math.abs(ageDate.getUTCFullYear() - 1970)
	}
}

const test = new Person("test", '9-10-1993')
console.log(test.calculateAge())>)

```

## Prototypes 

```js
function Person(firstName, lastName, dob) {
	this.firstName = firstName
	this.lastName = lastName
	this.birthday = new Date(dob)
	// this.calculateAge = function() {
	// 	const diff= Date.now() - this.birthday.getTime()
	// 	const ageDate = new Date(diff)
	// 	return Math.abs(ageDate.getUTCFullYear() - 1970)
	// }
}
Person.protoype.calculateAge = function() {
		const diff= Date.now() - this.birthday.getTime()
		const ageDate = new Date(diff)
		return Math.abs(ageDate.getUTCFullYear() - 1970)
	}

const test = new Person("test", "testo", "8-12-90")
const testet = new Person("testet", "testo", "8-10-90")




console.log(testet)


// __proto__ => Person.prototype
// __proto__ -> __proto__ => Object.prototype
```

all objects inherit stuff from prototype

`Object.prototype` 
`Person.prototype`


## Prototype inheritance 

```js
function Person(firstName, lastName) {
	this.firstName = firstname
	this.lastName = lastName 
}

Person.prototype.greeting = function () {
	return `Hello ${this.firstName}`
}

function Customer(firstName, lastName, phone, membership) {
	Person.call(this, firstName, lastName)
	this.phone = phone
	this.membership = membership
}

const customer1 = new Customer()
```


## Sync & Async

// Sync code - Blocking code, wait until something is fetched - slows the code down 
// Async code - NonBlocking code it will continue until its fetched.. 


- Callbacks
- Promises
- Async/Await 

Promises - A `Promise` is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value. It allows you to write asynchronous code in a more manageable way by providing a way to register callbacks to be called when the asynchronous operation completes or fails.

Example: 

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous operation
  setTimeout(() => {
    resolve('Success!');
  }, 1000);
});

myPromise.then((value) => {
  console.log(value); // "Success!"
});
```


## MORE PROMISES 




## Closure

Closre is nothing more then a function which has a inner function that has access to the outerFunction properties, example: 

```javascript
// outer function
function greet() {
  // variable defined outside the inner function
  let name = 'John';

  // inner function
  function displayName() {
    // accessing name variable
    return 'Hi' + ' ' + name;
  }
  return displayName;
}

const g1 = greet();
console.log(g1); // returns the function definition
console.log(g1()); // returns the value "Hi John"
```

### Private / Public accessors
Module Pattern 
```js
const UICtrl = (function () {
	// Private scope
	let text = "Text";
	const changeText = function () {
		text = "poop";
	};

	return {
		// Public scope
		callChangeText: function () {
		changeText();
		console.log(text);
		},

	};

})();
UICtrl.callChangeText();
```

Revealing module pattern is very similar, just retur the values without a function wrapper and you can access everything. 


## Factory Pattern 



## Null vs Undefined

`null` and `undefined` are both used to represent the absence of a value, but they are used in slightly different ways:

-   `undefined` is the default value of a variable that has been declared but not assigned a value. It is also the value of a function parameter that has not been provided when the function is called. You generally don’t need to explicitly set a variable to `undefined`, as it will automatically be assigned this value if you don’t assign it a value.
    
-   `null`, on the other hand, is used to represent the intentional absence of any object value. You can use `null` to explicitly indicate that a variable should have no value. For example, you might use `null` to represent an empty value in an array or an object property that should be empty.
    

In general, you should use `undefined` when you want to indicate that a variable has not been assigned a value, and `null` when you want to explicitly indicate that a variable should have no value.

### Event loop & async/await 

- Single threaded runtime - js 
- Single callstack 
- one thing at a time
- Call stack - records where we - are push on top, pop from the top 
- While loops are sync 


Event Loop - async things go here 

- SetTimeout for example - when run goes to the webapis stack and then, when webAPI is done it goes to the taskQue and then back to the stack. 
- IF THE STACK IS EMPTY TAKE THE FIRST THING IN THE QUE 

// Factory example 

```js
const SignerFactory: Record<AlgorithmEnum, typeof ECDSASigner | typeof RSASigner> = {
 [AlgorithmEnum.EC]: ECDSASigner, 
 [AlgorithmEnum.RSA]: RSASigner, 
 }; 

export async function signTransaction( deviceId: string, data: string, persistence: Persistence ): Promise<SignatureResponse> {
 // ...
const Signer = SignerMap[device.algorithm]; 
if (!Signer) { throw new Error("Algorithm not supported"); } // ...
}
```

Why not use ENUMS? 



Here’s an example that demonstrates some differences between `type` and `interface` in TypeScript:

```typescript
// Primitive types
// Only type can be used to alias a primitive
type Nullish = null | undefined;
type Fruit = 'apple' | 'pear' | 'orange';
type Num = number | bigint;

// Extending
// An interface can be extended by another interface
interface User {
  name: string;
  age: number;
}

interface AdminUser extends User {
  role: string;
}

const adminUser: AdminUser = {
  name: "Jane Doe",
  age: 35,
  role: "Administrator"
};

// A type cannot be extended like an interface extension
type UserType = {
  name: string;
  age: number;
};

type AdminUserType = UserType & {
  role: string;
};

const adminUserType: AdminUserType = {
  name: "John Doe",
  age: 40,
  role: "Administrator"
};
```

In this example, we see that only `type` can be used to alias a primitive. [We also see that an `interface` can be extended by another `interface`, while a `type` cannot be extended like an `interface` extension](https://stackoverflow.com/questions/37233735/interfaces-vs-types-in-typescript)[1](https://stackoverflow.com/questions/37233735/interfaces-vs-types-in-typescript).