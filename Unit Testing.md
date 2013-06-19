# Goals of Unit Testing

1. Guarantee (as close as possible) that your code will work flawlessly when in production.
2. Understand where your code is coupled to the rest of the code base. 
3. Limit the use of non-local variables, especially in private functions.
3. Test the PUBLIC interface to make sure it responds appropriately.  

_“In general, you don’t want to break any encapsulation for the sake of testing (or as Mom used to say, “don’t expose your privates!”). Most of the time, you should be able to test a class by exercising its public methods. If there is significant functionality that is hidden behind private or protected access, that might be a warning sign that there’s another class in there struggling to get out.” - [Pragmatic Unit Testing](http://pragprog.com/book/utj/pragmatic-unit-testing-in-java-with-junit)_  

# Process

1. Write unit tests for the riskiest items first. Examples of risky items are:
  1. networking requests - because you don't control the server
  2. business logic - because if this fails you could be losing millions of dollars
  3. state machines - because they are very hard to get right
2. Unit testing means Isolate testing on ONE single function.
  1. Any parameters used, implied data structure used, objects/classes used in your function are all dependancies
  2. Dependancies needs to be minimized in your function as MUCH AS POSSIBLE. This means implied data structures in your params as well.
  3. Every dependency is a chance for your code to break.
3. Find all the ways your function could break.
  1. Any time you call this.*someMethod* you have a dependancy. 
  2. Any params that are passed in can be bad. You should only pass in the smallest amount of data into a function that is need. It's better to have multiple params then if/when a huge data model changes you need to update multiple classes all over the code base.

# Code smell

* **Large Mocks and/or Stubs.** if you're making lots of mock and stubs it probably means your function is doing too much or have too many dependancies
* **Dispatching Events.** if you dispatch an event it means in production anyone can listen for it and you can't guarantee that the next action will be correct. 
  * Instead reverse the connection. Let external objects observe when you change a property so that they can take actions. This isolated side-effects because only those who have gotten reference to your object have the ability to take actions. Also it means the other class needs to test that they can capture the value change, you're class doesn't have to test anything.
