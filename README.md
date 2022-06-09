# JavaScript ES6
- ES stands for ECMAScript while ES6 stands for ECMAScript 6. ECMAScript was created to standardize JavaScript, and ES6 is the 6th version of ECMAScript.
- ECMAScript is a standard while JavaScript is it's implementation.
- Different versions of ECMAScript:
    - [ v1, v2, v3, v4, v5, v5.1, **v6** ]
- ES6 is a new version of JavaScript released in 2015 and is also known as ECMAScript 2015 or ES2015.

### Babel
- Babel is a free and open-source JavaScript transcompiler that is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript that can be run by older JavaScript engines. Babel is a popular tool for using the newest features of the JavaScript programming language.

### Topics
1. [The 'forEach' helper method](#1-the-foreach-helper-method)
2. [The 'map' helper method](#2-the-map-helper-method)
3. [The 'filter' helper method](#3-the-filter-helper-method)
4. [The 'find' helper method](#4-the-find-helper-method)
5. [The 'every' and 'some' helper method](#5-the-every-and-some-helper-method)
6. [The 'reduce' helper method](#6-the-reduce-helper-method)
7. [const/let keywords](#7-constlet-keywords)
8. [Template strings](#8-template-strings)
9. [Arrow functions](#9-arrow-functions)
10. [Default function arguments](#10-default-function-arguments)
11. [Rest and Spread operators](#11-rest-and-spread-operators)
12. [Destructuring](#12-destructuring)
13. [Promises and Fetch](#13-promises-and-fetch)
14. [Enhanced Object Literals](#14-enhanced-object-literals)
15. [Classes](#15-classes)

## 1. The 'forEach' helper method
- The **forEach** array helper method calls a function once on each item in an array. In ES5 or below, if we want to iterate over an array, we would make use of a for loop.

```js
var colors = ['red', 'green', 'blue'];
// ES5 and below
for(var i = 0; i < colors.length; ++i) {
    console.log(colors[i]);
}

// ES6 way
colors.forEach(function(color) {
    console.log(color);
});

// ES6 way with arrow function.
colors.forEach((color) => {
    console.log(color);
});
```
```
Output:
red
green
blue
red
green
blue
red
green
blue
```

```js
// Sum up all the numbers in an array. (ES6 way)
var numbers = [1, 2, 3, 4, 5];
var sum = 0;

numbers.forEach(function(number) {
  sum = sum + number;
});

console.log(sum);
```
```
Output:
15
```

[Back To Top](#javascript-es6)

## 2. The 'map' helper method
- The **map** array helper method returns a new array with the results of a function that is passed to it. **map** calls a function once for each element in an array.

```js
var numbers = [1, 2, 3, 4, 5];

// ES5 and below
var doubleNumbers = [];
for(var i = 0; i < numbers.length; ++i) {
 doubleNumbers.push(numbers[i] * 2); 
}
console.log(doubleNumbers);

// forEach helper method (Somewhat better)
doubleNumbers = [];
numbers.forEach(function(number) {
  doubleNumbers.push(number * 2); 
});
console.log(doubleNumbers);

//map helper method (Best)
doubleNumbers = numbers.map(function(number) {
  return number * 2;
});
console.log(doubleNumbers);

// map helper method with arrow function (Bow down)
doubleNumbers = numbers.map(number => number * 2);
console.log(doubleNumbers);
```
```
Output:
[ 2, 4, 6, 8, 10 ]
[ 2, 4, 6, 8, 10 ]
[ 2, 4, 6, 8, 10 ]
[ 2, 4, 6, 8, 10 ]
```

-  **NOTE:** In practical applications, we normally avoid mutating the original array.

```js
var cars = [
  {model: 'Buick', price: 'cheap' },
  {model: 'Camaro', price: 'expensive' },  
  {model: 'Volvo', price: 'expensive' },  
];

// This is called plucking. 
var models = cars.map(car => car.model);
console.log(models);
```
```
Output:
[ 'Buick', 'Camaro', 'Volvo' ]
```

[Back To Top](#javascript-es6)

## 3. The 'filter' helper method
- The **filter** array helper method creates a new array with all elements that pass the test implemented by the provided function.

```js
var products = [
  { name: 'cucumber', type: 'vegetable', quantity: 0, price: 1},
  { name: 'banana', type: 'fruit', quantity: 10, price: 15},
  { name: 'celery', type: 'vegetable', quantity: 30, price: 9},
  { name: 'orange', type: 'fruit', quantity: 3, price: 5},
];

// ES5 and below
var filteredProducts = [];
for(var i = 0; i < products.length; ++i) {
  if(products[i].type === 'fruit'){
    filteredProducts.push(products[i]);
  }
}
console.log(filteredProducts);

// filter helper method where type is 'fruit'
filteredProducts = products.filter(function(product) {
  return product.type === 'fruit';
});
console.log(filteredProducts);

// Strong filter where type is 'vegetable', quantity > 0, and price < 10
filteredProducts = products.filter(function(product) {
  return product.type === 'vegetable' && product.quantity > 0 && product.price < 10;
});
console.log(filteredProducts);
```
```
Output:
[ { name: 'banana', type: 'fruit', quantity: 10, price: 15 },
  { name: 'orange', type: 'fruit', quantity: 3, price: 5 } ]
[ { name: 'banana', type: 'fruit', quantity: 10, price: 15 },
  { name: 'orange', type: 'fruit', quantity: 3, price: 5 } ]
[ { name: 'celery', type: 'vegetable', quantity: 30, price: 9 } ]
```

[Back To Top](#javascript-es6)

## 4. The 'find' helper method
- The **find** helper method is used to find an element from the array of elements. **find** method returns the first element that satisfies the provided condition. The key difference here, when compared to **filter** is, **filter** returns all the elements that satisfies the condition whereas **find** returns the first element.

```js
var products = [
  { name: 'cucumber', type: 'vegetable', quantity: 0, price: 1},
  { name: 'banana', type: 'fruit', quantity: 10, price: 15},
  { name: 'celery', type: 'vegetable', quantity: 30, price: 9},
  { name: 'orange', type: 'fruit', quantity: 3, price: 5},
];

// ES5 and below
var product;
for(var i = 0; i < products.length; ++i) {
  if(products[i].name === 'celery'){
    product = products[i];
    break;
  }
}
console.log(product);

// ES6 way
product = products.find(function(product) {
    return product.name === 'celery';
});
console.log(product);

// Strong find operation
product = products.find(function(product) {
  return product.type === 'fruit' && product.price === 15; 
});
console.log(product);
```
```
Output:
{ name: 'celery', type: 'vegetable', quantity: 30, price: 9 }
{ name: 'celery', type: 'vegetable', quantity: 30, price: 9 }
{ name: 'banana', type: 'fruit', quantity: 10, price: 15 }
```

[Back To Top](#javascript-es6)

## 5. The 'every' and 'some' helper method
- The **every** array helper method tests whether all elements in the array pass the test implemented by the provided function. The purpose of the **some** array helper method is to execute a function for every array element and test if it meets a certain condition. Both helper methods return a boolean value.
```js
// Task: I have a set of computers and I want to run a program to check, whether I am able to run the program on all computers or on some computers with ram size 16 gigs.
var computers = [
  { name: 'Apple', ram: 24 },
  { name: 'Compaq', ram: 4 },
  { name: 'Acer', ram: 32 },
];

var allComputersCanRunProgram = true;
var someComputersCanRunProgram = false;

// ES5 and below
for(var i = 0; i < computers.length; ++i){
  var computer = computers[i];
  if(computer.ram < 16) {
    allComputersCanRunProgram = false;
  } else {
    someComputersCanRunProgram = true;
  }
}
console.log(`Can all computers run program: ${allComputersCanRunProgram}`);
console.log(`Can some computers run program: ${someComputersCanRunProgram}`);

// ES6 (every helper method)
allComputersCanRunProgram = computers.every(function(computer){
	return computer.ram > 16;
});
// OR
// allComputersCanRunProgram = computers.every(computer => computer.ram > 16);
console.log(`Can all computers run program: ${allComputersCanRunProgram}`);
allComputersCanRunProgram = computers.every(computer => computer.ram > 16);

// ES6 (some helper method)
allComputersCanRunProgram = computers.some(function(computer){
	return computer.ram > 16;
});
// OR
// allComputersCanRunProgram = computers.some(computer => computer.ram > 16);
console.log(`Can some computers run program: ${someComputersCanRunProgram}`);
```
```
Output:
Can all computers run program: false
Can some computers run program: true
Can all computers run program: false
Can some computers run program: true
```

[Back To Top](#javascript-es6)

## 6. The 'reduce' helper method
- The **reduce** array helper method executes a reducer function for array element. It returns a single value: the function's accumulated result. It does not execute the function for empty array elements. It does not change the original array.

```js
var numbers = [10, 20, 30, 40, 50];

// ES5 and below
var sum = 0;
for(var i = 0; i < numbers.length; ++i){
  sum += numbers[i]; 
}
console.log(sum);

// ES6 reducer helper
sum = numbers.reduce(function(curSum, num){
  return curSum + num;
}, 0);
console.log(sum);

var primaryColors = [
  {color: 'red'},
  {color: 'yellow'},
  {color: 'blue'},
];

// ES6 map helper method
var opMap = primaryColors.map(function(primaryColor){
	return primaryColor.color;
});
console.log(opMap);

// ES6 reduce helper method
var opReduce = primaryColors.reduce(function(prev, pc){
    prev.push(pc.color);
    return prev;
}, []);
console.log(opReduce);
```
```
Output:
150
150
[ 'red', 'yellow', 'blue' ]
[ 'red', 'yellow', 'blue' ]
```
- **Question:** Check whether paranthesis are balanced or not.
```js
// Example 1: "()()()()" - Balanced
// Example 2: "(((())))" - Balanced
// Example 3: "(()))()(" - Not Balanced

function areParanthesisBalanced(parans){
  return !parans.split("").reduce(function(prev, charParan){
    if(prev < 0) return prev;
    if(charParan == "(") return ++prev;
    if(charParan == ")") return --prev;
    return prev;
  }, 0);
}

areParanthesisBalanced("()()()()");
areParanthesisBalanced("(((())))");
areParanthesisBalanced("(()))()(");
```
```
Output:
true
true
false
```

[Back To Top](#javascript-es6)

## 7. const/let keywords
- In JavaScript E6, we are not going to use var. Instead, we use **const** or **let**. We use **const** when we know that the value is never going to change.(NEVER EVERRR!!!!). We use **let** when we know that the value is going to change overtime.

```js
// ES5 way
// var name = 'Jane';
// var title = 'Software Engineer';
// var hourlyWage = 40;

// ES6 way
const name = 'Jane';
let title = 'Software Engineer';
let hourlyWage = 40;

// -- Some time later --
title = 'Senior Software Engineer';
hourlyWage = 60;
```

[Back To Top](#javascript-es6)

## 8. Template strings
- Template strings are a powerful feature of modern JavaScript released in ES6. It lets us insert/interpolate variables and expressions into strings without needing to concatenate like in older versions of JavaScript. It allows us to create strings that are complex and contain dynamic elements.

```js
// Normal string concatenation
function getMessage() {
  const year = new Date().getFullYear();
  return "The year is: " + year;
}

// Template string
function getTemplateMessage() {
  const year = new Date().getFullYear();
  return `The year is: ${year}`;
}

console.log(getMessage());
console.log(getTemplateMessage());

const device_id = 4;
const guid = 20;
const username = "hello";

// Template string
const data = `{"device_id":"${device_id}", "guid":"${guid}", "username":"${username}"}`;
console.log(data);
```
```
Output:
The year is: 2022
The year is: 2022
{"device_id":"4", "guid":"20", "username":"hello"}
```

[Back To Top](#javascript-es6)

## 9. Arrow functions
- An arrow function expression is a compact alternative to a traditional function expression, but is limited and can't be used in all situations.
- There are differences between arrow functions and traditional functions, as well as some limitations:
  1. Arrow functions don't have their own bindings to this, arguments or super, and should not be used as methods.
  2. Arrow functions don't have access to the new.target keyword.
  3. Arrow functions aren't suitable for call, apply and bind methods, which generally rely on establishing a scope.
  4. Arrow functions cannot be used as constructors.
  5. Arrow functions cannot use yield, within its body.

```js
// Normal function
const add = function(a, b){
  return a + b;
};
console.log(add(1, 2));

// Arrow function
const addArrow = (a, b) => {
  return a + b;
};
console.log(addArrow(1, 2));

// Implicit return of Arrow function
const condensedAddArrow = (a, b) => a + b;
console.log(condensedAddArrow(1, 2));

// Compact Arrow function
const doubleNum = number => 2 * number;
console.log(doubleNum(8));

// Double each number in an array
const numbers = [1, 2, 3, 4, 5];
const doubleNums = numbers.map(num => num * 2);
console.log(doubleNums);

const team = {
  members: ['Jane', 'Bill'],
  teamName: 'Super Squad',
  teamSummary: function() {
    var self = this;
    return this.members.map(function(member){
    	return `${member} is on team ${self.teamName}`;
    });
  }
};

const teamArrow = {
  members: ['Jane', 'Bill'],
  teamName: 'Super Squad',
  teamSummary: function() {
    return this.members.map(member => {
    	return `${member} is on team ${this.teamName}`;
    });
  }
};

team.teamSummary();
teamArrow.teamSummary();
```
```
Output:
3
3
3
16
[ 2, 4, 6, 8, 10 ]
[ 'Jane is on team Super Squad', 'Bill is on team Super Squad' ]
[ 'Jane is on team Super Squad', 'Bill is on team Super Squad' ]
```

[Back To Top](#javascript-es6)

## 10. Default function arguments
- Default function parameters allow named parameters to be initialized with default values if no value or undefined is passed.
```js
const makeAJAXRequest = (url, method = 'GET') => {
    return `URL: ${url}, Method: ${method}`;
}

console.log(makeAJAXRequest('https://www.google.com'));
console.log(makeAJAXRequest('https://www.google.com', undefined));
console.log(makeAJAXRequest('https://www.google.com', null));
console.log(makeAJAXRequest('https://www.google.com', 'POST'));
```
```
Output:
URL: https://www.google.com, Method: GET
URL: https://www.google.com, Method: GET
URL: https://www.google.com, Method: null
URL: https://www.google.com, Method: POST
```

[Back To Top](#javascript-es6)

## 11. Rest and Spread operators
- The **rest** operator (…) allows us to call a function with any number of arguments and then access those excess arguments as an array. The rest operator also allows us in destructuring array or objects. The **spread** operator (…) allows us to expand an iterable like array into its individual elements.

```js
// Rest operator to capture all arguments
const addNumbers = (...numbers) => {
  return numbers.reduce((sum, num) => sum + num, 0);
};

console.log(addNumbers(1,2,3,4,5))
console.log(addNumbers(1,2,3,4,5,6));
console.log(addNumbers(1,2,3,4,5,6,7,8));

// Spread Operator
const defaultColors = ['red', 'green'];
const userFavColors = ['orange', 'yellow'];

// Way 1 - Using concat method
const arr1 = defaultColors.concat(userFavColors);
console.log(arr1);

// Way 2 - Using Spread operator
const arr2 = ['purple', ...defaultColors, 'blue', ...userFavColors];
console.log(arr2);

// Rest and Spread Mix
function unshift(array, ...rest) {
  return [...rest, ...array];
}
```
```
Output:
15
21
36
[ 'red', 'green', 'orange', 'yellow' ]
[ 'purple', 'red', 'green', 'blue', 'orange', 'yellow' ]
```

[Back To Top](#javascript-es6)

## 12. Destructuring
- The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

```js
// Example 1
const expense = {
    type: 'Business',
    amount: '45 USD'
};

// Normal way
// var type = expense.type;
// var amount = expense.amount;

// ES6 (Destructuring)
const { type, amount } = expense;
console.log(`Type: ${type} and Amount: ${amount}`);

// Example 2
const saveFiled = {
    extension: 'jpg',
    name: 'repost',
    size: 14040
};

function fileSummary({name, size, extension}){
    return `The file ${name}.${extension} is of size ${size}`;
}
console.log(fileSummary(saveFiled));

// Example 3
// Destructuring array
const companies = ['Google', 'Facebook', 'Uber'];
const [name1, name2, name3] = companies;
console.log(name1);
console.log(name2);
console.log(name3);

const [firstCompany, ...restCompanies] = companies;
console.log(firstCompany);
console.log(restCompanies);

// Example 4
const allCompanies = [
    {name: 'Google', location: 'Mount View'},
    {name: 'Facebook', location: 'Menlo Park'},
    {name: 'Uber', location: 'San Francisco'},
];
const [{location: googleLocation}] = allCompanies
console.log(googleLocation);

// Example 5
const Google = {
    locations: ['Mountain View', 'New York', 'Londan']
};
const {locations: [ _ ,location]} = Google
console.log(location);

// Example 6
const points = [
    [4, 5],
    [10, 1],
    [0, 30]
];

const allPoints = points.map(([x, y]) => {
    return {x, y};
});
console.log(allPoints);

// Example 7
const classes = [
  [ 'Chemistry', '9AM', 'Mr. Darnick' ],
  [ 'Physics', '10:15AM', 'Mrs. Lithun'],
  [ 'Math', '11:30AM', 'Mrs. Vitalis' ]
];

const classesAsObject = classes.map(([subject, time, teacher]) => {
    return {subject, time, teacher};
});
console.log(classesAsObject);
```
```
Output:
Type: Business and Amount: 45 USD
The file repost.jpg is of size 14040
Google
Facebook
Uber
Google
[ 'Facebook', 'Uber' ]
Mount View
New York
[ { x: 4, y: 5 }, { x: 10, y: 1 }, { x: 0, y: 30 } ]
[ { subject: 'Chemistry', time: '9AM', teacher: 'Mr. Darnick' },
  { subject: 'Physics', time: '10:15AM', teacher: 'Mrs. Lithun' },
  { subject: 'Math', time: '11:30AM', teacher: 'Mrs. Vitalis' } ]
```

[Back To Top](#javascript-es6)

## 13. Promises and Fetch
 - Read [MDN - Using Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises). 
```js
// Promise
console.log("Helloo!!");
const promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve(), 3000);
}).then(() => {
    console.log("Finisheddd!!!!");
}).then(() => {
    console.log("Finisheddd!!!! Also!!!");
}).catch(() => {
    console.log("Rejecteddd!!!!");
});
console.log("I rannn first!!!!");
```
```
Output:
Helloo!!
I rannn first!!!!
Finisheddd!!!!
Finisheddd!!!! Also!!!
```
- Read [MDN - Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
```js
// Fetch (Run this in browser's console)
const url = "https://jsonplaceholder.typicode.com/posts/";
fetch(url)
    .then(response => response.json())
    .then(data => console.log(data[0].id))
    .catch(err => console.log('BAD', err);
```

[Back To Top](#javascript-es6)

## 14. Enhanced Object Literals
- For better readability

```js
const inventory = [
  {title: 'Harry Potter', price: 10},
  {title: 'Eloquent JavaScript', price: 15},
];

function createBookShop(inventory) {
  return {
    inventory: inventory,
    inventoryValue: function() {
      return this.inventory.reduce((total, book) => total + book.price, 0);
    },
    priceForTitle: function(title) {
      return this.inventory.find(book => book.title === title).price;
    }
  };
}

function createEnhancedBookShop(inventory) {
  return {
    inventory,
    inventoryValue() {
      return this.inventory.reduce((total, book) => total + book.price, 0);
    },
    priceForTitle(title) {
      return this.inventory.find(book => book.title === title).price;
    }
  };
}

// const bookShop = createBookShop(inventory);
const bookShop = createEnhancedBookShop(inventory);
console.log(bookShop.inventoryValue());
console.log(bookShop.priceForTitle('Harry Potter'));
```
```
Output:
25
10
```

[Back To Top](#javascript-es6)

## 15. Classes
- Prototypal Inheritance (DIFFICULT!!!!)
```js
function Car(options){
    this.title = options.title;
}

Car.prototype.drive = function(){
    return 'Vroom!!!';
}

function Toyota(options) {
    Car.call(this, options);
    this.color = options.color;
}

Toyota.prototye = Object.create(Car.prototype);
Toyota.prototype.constructor = Toyota;

Toyota.prototype.honk = function(){
    return 'beep';
}

const toyota = new Toyota({title: 'Daily Driver', color: 'red'});
console.log(toyota);
```
```
Output:
Toyota { title: 'Daily Driver', color: 'red' }
```

- Class (EASY!!!!)
```js
class Car {
    constructor({ title }){
        this.title = title;
    }
    drive(){
        return 'Vroom!!!';
    }
}

class Toyota extends Car {
    constructor(options){
        super(options);
        this.color = options.color;
    }
    honk() {
        return 'beep';
    }
}

const car = new Toyota({ title: 'Daily Driver', color: 'red' });
console.log(car);
console.log(car.drive());
console.log(car.honk());
```
```
Output:
Toyota { title: 'Daily Driver', color: 'red' }
Vroom!!!
beep
```
[Back To Top](#javascript-es6)
