

01  Javascript for Server Side Development
===

## Table of Contents
- [01  Javascript for Server Side Development](#01--javascript-for-server-side-development)
  * [Functions](#functions)
    + [1st Class Functions](#1st-class-functions)
    + [Higher-Order Functions](#higher-order-functions)
    + [Closures](#closures)
  * [Javascript and Callbacks](#javascript-and-callbacks)
    + [Example](#example)
    + [Handling Errors in Callbacks](#handling-errors-in-callbacks)
    + [Arrow Functions](#arrow-functions)


Functions
---
### 1st Class Functions
- anonymous func = func w/o name
- funcs are objs in js
    - can assign funcs to vars, arrays elements and to other objs
    - can be passed as args to other funcs/returned from them
- 1st class func = func that is defined and can be treated as a var

```javascript=
var funct1 = function () { // anonymous function
  console.log(“Printing!!”);
}
funct1();
```

### Higher-Order Functions
- higher-order funcs = funcs that take other funcs as args
    - eg. `setInterval(func, milliseconds)`

```javascript
function run() {
    console.log(‘Running….’);
}
setInterval(run, 1000);    // higher order
```

### Closures
- closure = feature in js whr inner func has access to outer enclosing func's vars
    - 3 key properties
        - has access to vars defined in itself
        - has access to outer func's var
        - inner func will continue to have access to vars from outer scope even after outer func has returned

```javascript
function outerFunction(x) {
    var variableInOuterFunction = x;
    inner=function innerFunction() {
        console.log(“In inner function…”);
         // Access a variable from the outer scope
        console.log(variableInOuterFunction);
    }
    return inner;
}
inner=outerFunction('hello world!'); 
inner()
```


Javascript and Callbacks
---
- js is synchronous by default and single threaded
    - code executed one line after another
- how to respond to user actions with a sync programming model?
    - ans = environment
    - browser provides way by providing a set of APIs that can handle this functionality
        - hence js is event driven
- nodejs also introduces a non blocking I/O env to extend this concept to file access, network calls etc.
- to know when user is going to click btn, u define an event handler for the click event
    - event handler accepts a func which is called when the event is triggered
    - AKA callback

```javascript=
document.getElementById('button').addEventListener('click', function() {
  //item clicked
})
```
- __callback__ - func that's passed as value to another func and will only be executed when parent func wants it to be executed
    - done with 1st class and higher order funcs

### Example
```javascript=
function firstFn(){
  // Simulate a code delay
  setTimeout( function(){
    console.log(1);
  }, 2000 );
}
function secondFn(){
  console.log(2);	
}
firstFn();
secondFn();
```
- even though firstFn() was invoked first, result of secondFn() gets printed first
    - js didnt wait for response from firstFn() before moving on to execute secondFn() since setTimeout is an async func
    - callbacks enable support of non-blocking I/O env in nodejs

![](https://i.imgur.com/4nbQSsq.png)

### Handling Errors in Callbacks
- 1st param in any callback is the error obj
    - if no error, return null
    - if have error, will also contain description of error

```javascript=
const fs = require('fs');
fs.readFile('/file.txt',’utf-8’, function(err, data){
  if (err !== null) {
    //handle error
    console.log(err)
  }else

  //no errors, process data
  console.log(data)
})
```

### Arrow Functions
- introduced in es6
- make code more concise and simplify func scoping
    - avoid having to type func and return keyword

```javascript=
const fs = require('fs');
  fs.readFile('/file.txt', (err, data)=>
  {
    if (err !== null) {
      //handle error
      console.log(err)
    }else
  
    //no errors, process data
    console.log(data)
  });


// another example
multiplyFunct = (x, y) => x * y;
console.log(multiplyFunct(2,3));
```




###### tags: `BED` `DISM` `School` `Notes`