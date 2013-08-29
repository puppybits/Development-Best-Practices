# JavaScript Coding Standards

## General
* **No line should exceed 90 characters.**
  * this is to make blame views, multiple tab editors, merging and side-by-side app and code debugging easier
  * to avoid running long, set descriptive variables, add returns on functions with lots of params, chained function calls like jquery should be returned with indents after each function call
  * any templates that allow for mixing javascript with html, javascript code should be avoided as much as possible
  * When you read you're code again 6 months later you should understand what and why the code is doing something.
  * never use `eval`.
  * always use strict equals `=== ` and strict not equals `!===`.
  * use `||` to set defaults. Set defaults as close to the top of the function as possible.

---

## Variables

 * there should be no magic numbers

```js
// WRONG
x = force * 0.9;

// RIGHT
earthGravity = 0.9;
x = force * earthGravity;
```

* all `var` declarations inside a function get hoisted to the top of the function when the code is processed. Declare any key properties at the top of the function.
* constants should `BE_LIKE_THIS`
* any jQuery cached selectors should start with a dollar sign.
* don't create variables inside of a loop.

```js
// WRONG
var arr = [1,2,3,4,5,6,7];
for (var i = 0; i < arr.length; i++)
{
  arr.filter( function( j ) { return j < 5; } );
}

// RIGHT
var arr = [1,2,3,4,5,6,7],
highThanFive = function( j ) { return j < 5; };
for (var i = 0; i < arr.length; i++)
{
  arr.filter( highThanFive );
}
// WHY? calling function or var inside a loop will allocate space in the heap and create a new instance each time through the loop. So in the example instead of creating just one function it will check 7 functions that need to be marked for garbage collection as soon as the loop is complete. This is a waste of memory and resources and has been impacts on old computers and mobile devices where there's not much to go around.

```

* don't pollute the global namespace. **Always** use var in front of a variable that is declared for the first time. Not doing so will make it global.
* name variables with something descriptive and don't abbreviate.
* always favor descriptive variable names over adding more comments in the code. Inline comments means you're code isn't understandable enough by itself or you're doing something fairly complex.

---

## Functions

* Favor the Module pattern for creating complex objects. 
* NEVER put instructions in a return statement. This includes returning Object with public methods. This makes for harder debugging and makes code less readable.
* don't try to be too smart or do fancy tricks; it just causes confusion. Write code others can understand.

```js
//WRONG
function calculateForce( previousX, x ) 
{
  return mass * Math.abs(previousX - x) / new Date().getTime();
}

//RIGHT
function calculateForce( previousX, x ) 
{
  acceleration = Math.abs(previousX - x) / new Date().getTime();
  force = mass * acceleration;
  
  return force;
}

```

 * self-invoked functions should have the parenthesis inside

```js
//WRONG
var thing = (function ( ) 
{
  .. code
})();

//RIGHT
var thing = (function ( ) 
{
  .. code
}());

```


* stay away from passing large nondescript objects as a parameter for a function. Be as explicit as possible.

```js
// WRONG
function sendMessageServiceRequest( data, success, callback ) { ... }

// RIGHT
function sendMessageServiceRequest( userid, messageId, messageBody, success, callback ) { ... } 

// WHY? This helps you to see the dependancies of the function better. It helps other developers who didn't write this function, nor should they need to read the detail steps of every function, understand the requirements to use the function.
```

* If an error check can early return out of a method, do the check as close to the top as possible.
 * any check that's not completely understandable should be broken out into a boolean variable name. 


```js
// WRONG
if ( myVar === param1 && param1 !== otherVar )
{
  ...
}

// RIGHT
var isVarUnique = ( myVar === param1 && param1 !== otherVar );
if (isVarUnique) { ... }
```


---

## Readability - White Space
* code in paragraphs.
  * empty line breaks should be used to break up chunks of functionality. Normally there are a few chucks of things your function is doing. Keeping those chucks together make it more scanable and readable.

```js
//WRONG
function updatePosition( x ) 
{
  acceleration = Math.abs(previousX - x) / new Date().getTime();

  force = mass * acceleration;

  x += force; 

  this.move( x );
}

//RIGHT
function updatePosition( x ) 
{
  acceleration = Math.abs(previousX - x) / new Date().getTime();
  force = mass * acceleration;
  x += force; 

  this.move( x );
}
//WHY? Because the updatePosition function does 2 things. It calculates the forces, then it moves the object to the new position.  Keeping like functionality together helps to make your code more readable, scanable and understandable.


```

* functions should have the opening bracket on the following line.
* braces should be on separate lines unless it's a short object literal. ie `var obj = {myProperty:myValue}`
* any complex checks should be set to a descriptive variable. This improves readability and understandability of code as well as making it easier to debug.

```js
//WRONG
if ( b !== c && b !== a && ( b > 0 && b < 100) )
{
  ...
}

//RIGHT
var isBUniqueAndUnder100 = ( b !== c && b !== a && ( b > 0 && b < 100) );
if ( isBUniqueAndUnder100 )
{
  ...
}

```

---

## Dependency Management

* all dependancies should be listed in require's define method, except a few global objects like jquery.
* any private functions should have any and all dependancies injected as a param of the function. 

```js
//WRONG
function calculateXPosition( x ) 
{
  acceleration = Math.abs(previousX - x) / new Date().getTime();
  force = mass * acceleration;
  x += force; 

  return x;
}

//RIGHT
function calculateXPosition( x, previousX, mass, acceleration ) 
{
  acceleration = Math.abs(previousX - x) / new Date().getTime();
  force = mass * acceleration;
  x += force; 

  return x;
}
// WHY? This to keep private functions unit testable. If all the dependancies are injected as a param then when the function is ran it will count towards code completion because everything was testable and nothing needed to be mocked out. It also helps to spot dependancies much quicker and address way to eliminate them. 


```

* Ways to remove dependancies 
  * minimize the imports in require's define function.
  * try to use the smallest data model that has the data that is needed.
  * if a few properties are needed from another model, check if the properties will be static and can be passed in as a string instead of the entire model.


---

## Messaging Options

 * events
 * localize observing
 * data binding

---

## Work Flow

 * Break up all coding tasks into something that can be completed in 1 to 4 hours. Commit after each discrete task is complete. Sync code base at least once a day.
