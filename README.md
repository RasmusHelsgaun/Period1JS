Period-1 Vanilla JavaScript, es2015/15.., Node.js, Babel + Webpack and TypeScript

Explain the differences between Java and JavaScript. You should include both topics related to the fact that Java is a compiled language and JavaScript a scripted language, and general differences in language features.
Java is an Object Oriented programming language and creates applications that run in a virtual machine or browser. In order to run it, the code has to be compiled first.
Java is also strongly typed and variables must be declared first to run.

Javascript is an OOP scripting language that is run on a browser only. Browsers has an interpreter, so the code is run at runtime, while dynamically being typed without being complied first like Java has to.
Explain the two strategies for improving JavaScript: ES6 (es2015) + ES7, versus Typescript. What does it require to use these technologies: In our backend with Node and in (many different) Browsers
Not all browsers are able to run ES6 and up, so we have to transpile it into code the browser knows. For this we use transpilers like Babel in order to utilize the newer features ES6 and up offers. Typescript and Babel both transpile code, but Typescript is also a strict superset of JavaScript and adds types, class-based object-oriented programming and much more to the language.
Explain generally about node.js, when it “makes sense” and npm, and how it “fits” into the node echo system.
Node.js is based on Google’s V8 Engine and therefore runs on a Virtual Machine. It is event driven and highly targeted against asynchronous programming.
Node is also single threaded and therefore non-blocking using a callback concept.
It allows you to write JavaScript and run it from other places than the browser like a server or IOT.

NPM (Node Package Manager) is a software package manager and installer, and is the largest of its kind with over 800.000 code packages. It is Open-source and lets developers use npm, to share software.
Explain about the Event Loop in Node.js
Since it’s a non-blocking language and only uses one thread, we have to be able to handle parallel programming. We use event looping to solve this by adding callbacks to the requests we send out, as we are not able to wait for the response. When the response comes back, the callback is used to extract and convert the response data into usable content.
Explain (some) of the purposes with the tools Babel and WebPack, using  examples from the exercises
Babel is a compiler that makes it possible to implement the new features of JS even though the browers doesnt understand it. So babel transpiles/converts it into code the browers understands.
The following example shows the arrow functions intoduced in ES6
someArray.map(x => x * 10)
Babel then transpiles the code into ES5 code, so the browers understands it:
someArray.map(function (x) {
  return x * 10;
});
Webpack is a bundler that bundles all of your files and scripts into code that is readable by the browser. This way you can easily have several files and scripts, so it doesn’t get too clustered when writing your code, since you can easily organize your code.
Explain the purpose of “use strict” and Linters, exemplified with ESLint 
“use strict” is a literal expression and has the purpose to indicate that the code should be executed in “strict mode”. With strict mode you can not e.g use undeclared variables. Strict mode is declared by adding "use strict"; to the beginning of a script or a function.
Declared at the beginning of a script, it has global scope (all code in the script will execute in strict mode):
"use strict";
x = 3.14;
This will cause an error because x is not declared
Linters can increase code quality by detecting potential bugs, as well as code that is difficult to maintain. So if you run your code in a linter, it will show you what to potentially improve.
Explain using sufficient code examples the following features in JavaScript. 
Variable/function-Hoisting
In javascript variables will get hoistered meaning, you can use a variable before declaring it.
Hoisting means the variable will be placed at the top of the scope when you run the code. This can either be the global scope or maybe the scope of a function depending on where it is declared and how.


this in JavaScript and how it differs from what we know from Java/.net.
The JavaScript this keyword refers to the object it belongs to.
It has different values depending on where it is used:
In a method, this refers to the owner object.
Alone, this refers to the global object.
In a function, this refers to the global object.
In a function, in strict mode, this is undefined.
In an event, this refers to the element that received the event.
Methods like call(), and apply() can refer this to any object.

In Java, this refers to the current instance object on which the method is executed.

Function Closures and the JavaScript Module Pattern
JavaScript variables can belong to the local or global scope.
The use of function closures can help you achieve “private” variables and function, which JS normally does not support. You do this by wrapping your variables or functions inside a function and then return a function or an object. This way only the function or the object has access to the variables and functions, as they’re inside the scope of the function rather than in the global scope.

var add = (function () {
  var counter = 0;
  return function () {counter += 1; return counter}
})();

add();
add();
add();


This will result in the counter now being 3.

Another way of making “private” variables and functions, is through the module pattern.
With modules you can split your code into several files and import/export them to each other. You can then choose to export e.g a function that points to a variable, which you cannot get a hold of elsewhere.

Immediately-Invoked Function Expressions (IIFE)
An IIFE (Immediately Invoked Function Expression) is a function that runs as soon as it is defined.
(function(){
    console.log("IIFE")
})()

JavaScripts Prototype
All JavaScript objects inherit properties and methods from a prototype.
If we make a constructer and want to add a new property, then you cannot do it to an existing object like so:
Person.nationality = "English";
Instead you have to add it to the constructor itself.

In order to add something without having to add it to the constructor itself, you can make use of the prototype property like so:
function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
}

Property: 
Person.prototype.nationality = "English";
Method: 
Person.prototype.name = function() {
  return this.firstName + " " + this.lastName;
};

User-defined Callback Functions (writing your own functions that take a callback)
Some predefined methods takes callbacks(functions), but you can also make your own functions, that takes a callback

function filterArray(array, callback){
    const res = []
    for (element of array){
        if(callback(e)){
            res.push(e)
        }
    }
    return res;
}


const array = [1, 3, 5 ,6 ,8 ,9, 10]

const filtered = filterArray(array, (element) => element % 2 == 0)
console.log(filtered);

Explain the methods map, filter and reduce
const array = [1 ,2 ,5 ,7 ,8, 11, 23]

// Changes all elements and returns a new array with the same size
const mapped = array.map(e => e * e);
console.log(mapped);

// filters the array and returns a new array with same size or less
const filtered = array.filter(e => e > 7)
console.log(filtered);

// reduces the array to a single value
const reduced = array.reduce((accumulator, currentValue) => accumulator += currentValue, 0)
console.log(reduced);

Your reducer function's returned value is assigned to the accumulator, whose value is remembered across each iteration throughout the array and ultimately becomes the final, single resulting value.
The value 0 is optional, but indicates the initial values. This could be used, if you have a value you want the reduced value to be added to.

Provide examples of user-defined reusable modules implemented in Node.js
const filterDir = require("./module")
This imports your module. (module is the name of the file)
module.exports = function(pathToFile, extension, callback) {
   extension = '.' + extension
   fs.readdir(pathToFile, (err, data) => {
       if (err) {
           return callback(err)
       }
       const filtered = data.filter((filename) => path.extname(filename) === extension)
       return callback(null, filtered)
   })
}
if you export it using module.exports, then you can import whatever you exported in another file by importing it with require.
ES6,7,8... and TypeScript
Provide examples and explain the es2015 features: let, arrow functions, this, rest parameters, de-structuring assignments, maps/sets etc.
//Throw error because let does not hoist
function testLet() {
    console.log(x);
    if (false) {
        let x = "hej"
    }
}


// Arrow functions makes this behave more like java lambda expression
setTimeout(() => {
    console.log("Arrow functions are nice");
}, 1000);

//This is points to the global object unless it is attached to an object
const obj = {
    string: "hej object",
    printString: function () { console.log(this.string) },
    printString2: function () {
        setTimeout(function () {
            console.log(this.string);
        }, 1000)
    }
}

obj.printString()
obj.printString2()


// rest parameters allows us to represent an indefinite number of arguments as an array. 
function sum(...theArgs) {
  return theArgs.reduce((previous, current) => {
    return previous + current;
  });
}

// de-structuring assignments lets you handpick which properties of the object you want.
const person = {
    name: "Kurt Wonnegut",
    street: “Lyngbyvej 7”
}

const { name, street } = person
console.log(name, age);

//Maps key/value
let map = new Map();

map.set('foo', 123);
map.get('foo')
123

map.has('foo')
true
map.delete('foo')
true
map.has('foo')
false

//Sets lets you store unique values in an iterable data structure.
let set = new Set([blue, yellow, 'green']);
set.add('red')

set.has('red')
true
set.delete('red')
true
set.has('red')
false

Explain and demonstrate how es2015 supports modules (import and export) similar to what is offered by NodeJS.
In ES2015 we can use “export default” just like module.exports. You can ofcourse also write export to further export something, but if you can only have 1 default, as this is what the initial import gives you. 
To import it we use “import mySpecialFile from ‘./filename’”
You can in this context also import by deconstructing:
import {someThingSpecial} from ‘./thisSpecialFile’
Provide an example of ES6 inheritance and reflect over the differences between Inheritance in Java and in ES6.
class Teacher extends Person {
   constructor(first, last, age, gender, interests, subject, grade) {
       super(first, last, age, gender, interests);
       // subject and grade are specific to Teacher
       this._subject = subject;
       this.grade = grade;
   }

   get subject() {
       return this._subject;
   }

   set subject(newSubject) {
       this._subject = newSubject;
   }
 }
ES6 and Java inheritance are pretty similar in the way they work, but ES6 is built around prototype assignments.
Provide examples with es-next, running in a browser, using Babel and Webpack
Provide a number of examples to demonstrate the benefits of using TypeScript, including, types, interfaces, classes and generics
function logger2(a: number, b: string) {
   console.log(`Value of number: ${a}, Value of msg: ${b}`);
}

interface IPerson { name: string }
interface IAddress { street: string }

function logger3(p: IPerson, a: IAddress) {
   console.log(`Person name: ${p.name}, Address of person: ${a.street}`);
}
class Person implements IPerson {
   public name: string;
   constructor(name: string) {
       this.name = name
   }
}

class Address implements IAddress {
   public street: string;
   constructor(street: string) {
       this.street = street
   }

   public get getStreet(): string {
       return this.street
   }
}
function logger4<T, U>(p: T, a: U) {
   console.log(`Person name: ${p}, Address of person: ${a}`);
}
class GenericLogger<T, U> {
   log = (a: T, b: U) => console.log(`Hej 1 ${a}, Val 2 ${b}`);
}
const personLogger = new GenericLogger<IPerson, IAddress>()
It is very handy to have TypeScript as it enables you to declare what types you want your variables, inputs and even lets you have generic types on classes.
Explain the ECMAScript Proposal Process for how new features are added to the language (the TC39 Process)
Stage 0 (Strawman):
No real spec
Public for feedback
Allows for input
Stage 1 (Proposal):
Make the case for the addition
Describe the shape of a solution
Identify potential challenges
Stage 2 (Draft):
Precisely describe the syntax
Describe semantics using formal spec language
Stage 3 (Candidate):
Indicate that further refinement will require feedback from implementations and users
Stage 4 (Finished):
Indicate that the addition is ready for inclusion in the formal ECMAScript standard
Callbacks, Promises and async/await

Explain about promises in ES-6 including, the problems they solve, a quick explanation of the Promise API and:
Promises are used for operations like fetch, that does not complete immediately and has to wait for a response.
Promises works with a resolve and reject function. If everything went alright you will receive your data thought resolve(res) and if an error occurs you will get a reject(error) with the error.
Example(s) that demonstrate how to avoid the callback hell  (“Pyramid of Doom")
//Pyramid of doom
setTimeout(() => {
    console.log("hej");
    setTimeout(() =>{
        console.log("med");
        setTimeout(() =>{
            console.log("dig");
            setTimeout(() =>{
                console.log("hvad");
                setTimeout(() =>{
                    console.log("laver");
                    setTimeout(() =>{
                        console.log("du");
                    }, 1000)
                }, 1000)
            }, 1000)
        }, 1000)
    }, 1000)
},1000)

//with promises

function clgPromise(string) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log(string)
            resolve(string)
        }, 1000);
    })
}

clgPromise("hej")
    .then(() => clgPromise("med"))
    .then(() => clgPromise("dig"))
    .then(() => clgPromise("hvad"))
    .then(() => clgPromise("laver"))
    .then(() => clgPromise("du?"))

Example(s) that demonstrate how to execute asynchronous (promise-based) code in serial or parallel
function myPromise(msg, delay) {
   return new Promise((resolve, reject) => {
       setTimeout(() => {
           let error = false; // Math.random() * 10 < 2;
           if (error) {
               return reject(new Error("UPPPs"));
           }
           return resolve(msg.toUpperCase());
       }, delay);
   })
}

module.exports = myPromise
Serial:
const myPromise = require("./myPromise")

let results = []

myPromise("hello", 2000)
   .then(msg => {
       results.push(msg)
       return myPromise("hello again", 2000)
   })
   .then(msg => {
       results.push(msg)
       return myPromise("hello again again", 2000)
   })
   .then(msg => {
       results.push(msg)
   })
   .catch(e => {
       console.log(e);
   })
   .finally(() => console.log(results))
Parallel:
const p1 = myPromise("hello", 500)
const p2 = myPromise("hello again", 400)
const p3 = myPromise("hello again again", 100)
let promises = [p1, p2, p3]

Promise.all(promises)
   .then((d) => console.log(d))
   .catch(e => console.log(e))
   .finally(() => console.log("FINALLY"))

Example(s) that demonstrate how to implement our own promise-solutions.
Example(s) that demonstrate error handling with promises
const fetch = require("node-fetch")
const URL = "https://swapi.co/api/people/14353"
fetch(URL)
   .then((res) => {
       console.log(res.ok, res.status);
       if (res.status >= 400) {
           return Promise.reject({ status: res.status, fullError: res.json() })
       }
       return res.json()
   })
   .then(data => console.log("OK: ", data))
   .catch((error) => {
       if (error.status) {
           error.fullError.then(msg => console.log("UPS: ", msg))
       } else {
           console.log("UPPS: ", error)
       }
   })
   .finally(() => console.log("Finally got here"))
With promises you wanna use .catch to get the error and then manage it the way you want. With async/await you can just use try catch as we know from Java.

Explain about JavaScripts async/await, how it relates to promises and reasons to use it compared to the plain promise API.

Async/await can be used to wrap around promises to make the code more readable and make it appear as if it was synchronous.
This especially takes place when we handle errors via try/catch and we can also avoid using .then all the time, and instead assign the promise to a variable as shown below.


An async function can contain an await expression that pauses the execution of the async function and waits for the passed Promise's resolution, and then resumes the async function's execution and returns the resolved value.
The await keyword is only valid inside async functions. If you use it outside of an async function's body, you will get a SyntaxError.

getEmployees = async () => {
       const empUrl = URL + "employee"
       try {
           const opts = makeOptions("GET", true);
           const res = await fetch(empUrl, opts);
           const json = await handleHttpErrors(res);
           return { emp: json, status: res.status };
       } catch (e) {
           return e;
       }
   }

