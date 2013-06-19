# Self-Describing Code

## General
* **No line should exceed 90 characters.**
  * this is to make blame views, multiple tab editors, merging and side-by-side app and code debugging easier
  * to avoid running long, set descriptive variables, add returns on functions with lots of params, chained function calls like jquery should be returned with indents after each function call

## Variables

 * there should be no magic numbers

```js
// WRONG
x = force * 0.9;

// RIGHT
earthGravity = 0.9;
x = force * earthGravity;
```

---

## Functions


---

## Readability - White Space
* code in paragraphs.
  * empty line breaks should be used to break up chunks of functionality. Normally there are a few chucks of things your function is doing. Keeping those chucks together make it more scanable and readable.

```js
//WRONG
function updatePosition( x ) {
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
* 

---

## Error-Checking
* on a function's params be as explicit as possible

```js
// WRONG
function sendServiceRequest( data, success, callback ) { ... }

// RIGHT
function sendServiceRequest( userid, noteType, noteId, success, callback ) { ... } 
```
* error checking should handled at the beginning of the function
 * any check that's not completely understandable should be broken out into a boolean variable name. In 6 months you'll be able to still understand your code.

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

## Messaging Options

 * events
 * localize observing
 * data binding

---

## Work Flow

 * Break up all coding tasks into something that can be completed in 1 to 4 hours. Commit after each discrete task is complete. Sync code base at least once a day.
