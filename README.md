# undestanding-js-weird-parts
resumed ideas from [JavaScript: Understanding the Weird Parts- Anthony Alicea](https://www.udemy.com/course/understand-javascript/)


## Execution Context and Lexical Environments:

### Conceptual asides:

# Syntax parser: 
`a program that reads your code and determines what it does and if its gramar is valid`
<img width="749" alt="Screenshot 2022-03-19 at 20 16 46" src="https://user-images.githubusercontent.com/54862062/159133561-6916572e-845e-47d2-a513-a38124c00ec1.png">

# Lexical Environment   

`where something sits phisically in the code you write`

# Execution Context 

`a wrapper to help manage the code that is running`

-  can contain things beyond you've written in code
-  _this_ : special variable in javascript
-  Global: means mostly "not inside a function"

<img width="799" alt="Screenshot 2022-03-19 at 20 43 42" src="https://user-images.githubusercontent.com/54862062/159134960-21207843-e66d-4e6a-81c2-01609e7112ec.png">


-  Name/Value pair: 
    - `a name that maps to a unique value`
                     -  Name may be defined more than once, but can have only one value in any given context
                     -  Value may be more name/value pairs
-  Object  
   -  `collection of name/value pairs`

<img width="1039" alt="Screenshot 2022-03-19 at 20 32 34" src="https://user-images.githubusercontent.com/54862062/159134025-e32f6f64-e350-4c43-b261-44cb48006c06.png">

-  Hoisting
   - ``when creating execution context first allocates memory space for all decalred variables and functions and after having them all then executes code (assigments and functions calls)`` 
   -  ``JavaScript's default behavior of moving declarations to the top``
   
<img width="616" alt="Screenshot 2022-03-19 at 21 04 59" src="https://user-images.githubusercontent.com/54862062/159135154-bf37849c-af10-4a9c-bc42-9f6bab9d426f.png">

-  Scope Chain (propagation of scopes from parent to child)
-  JavaScript Engine->event Queue (asynchronous behaviour is related to what happens outside JavaScript Engine-> resulted from  execution injection into stack)

## Types and Operators:
- dynamic typing (no static typing)
- primitive types: data that represents a single value that is not an object ( 
* undefined -lack of existence, declared by engine
* null- lack of existence, declared by programmer
* boolean- true or false
* number- floating point number
* string- sequence of chars between ‘’, “” or ``
* symbol-ES6

- operators-special function syntactically different written (infixed notation between 2 arguments that return result)

* Precedence (order of call from higher downer) and Associativity (same precedence execution ltr or rtl )
* Coercion -converting a value from one type to another
* Comparison Operators -coercion of booleans to integer boolean (0 or 1) (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
* Existence and Booleans : Boolean(0) coerce to false => a=0; if (a||a===0){’executes true’}
* Default Values : colliding imported libs in global context ,overriding with latest assignment same named global variable value 

## Objects and functions:
* An object literal contains name-value pairs with values being primitives or objects or methods(functions attached to object)
* Namespaces are containers.For avoiding collisions can be faked by allocating content to an object 
* JSON are not object literals, are mostly string transfer data
* Functions are objects
    * First class functions: everything you can do with other objects can be done with functions also (assign to objects, pass the around, assign them on the fly) 
    * Function is a special type of object with more hidden type of properties
        * Assignment :primitive, objects, functions
        * Name->optional (can be anonymous)
        * Code-> makes them callable (invokable) (represents body of function)
        * Function expressions are not hoisted, therefore declaration first and only after is possible the invoke
        * Can receive parameter other functions (functional programming)
        * Have inner special functions (call, apply, bind)
* Expressions is a unit of code that results in a value at runtime . “I am a string” is a valid expression.  
* Function Statement is basically the literal code of function (declaration)
* Function Expression is basically a variable that is assigned with function body code 
* Functions can be Immediately invoked and into an expression will be the returned value 
* JS implicit Statements  are not assignable expressions returning accessible values: var x= if(a=b)  cannot be done;

* Conceptual (mutate=change:) 
    * By value or by reference:
        * for primitives by value: b= a-> b=copy of a pointing to a new location in memory  (changing a will not mutate b)
        * for object by reference: b=a ->b=copy of a pointing to same location in memory (changing a will also mutate b ) . Is valid even if are used as parameters. If used afterwards b=c  will recreate pointing to a new reference and will not mutate a (changing b will not affect a)
* this->means of it depends on where is used.
    * Points to global object into a function body use, at function call runtime
    * Points to containing object when used inside an attached function body at  function call runtime.  For propagating this value(containing object ) to consecutive nested declared function should be stored in a var of inner scope: var self=this; then used into attached function scope other declared functions bodies trough self. 
        *   Execution Context of a function has :
            * Variable Environment 
            *  reference to Outer Environment (determines scope chain search for variables) 
            * the keyword this
            * arguments (all parameters values passed to function grouped in array-like  [ , , ,] special keyword arguments )
## Arrays
* Regular array is a zero based list or collection of items (item can be anything in same array: primitive, object, function, jsx)
##  Function Overloading
* Does not exist in javascript
* Can be achieved by patterns: creating a function that calls inside overloaded variants
##  Syntax parser 
* -> goes in code character by character making assumptions
* -> dangerous aside: automatic semicolon insertion. Semicolons insertion should not be let at JavascriptEngine attitude to complete (return {key:’’value} executes as return; {key:’’value} )
* -> whitespace : permissible (permits adding comments in-between declarations for example  with //)
* Immediately invokes function expressions (IIFE) (()=>{})() are creating their execution context that is disposed immediately after execution, avoiding collisions
* Parentheses is the grouping operator containing expressions or IIFE ,  (()=>{}())
##  Closures
* A closure represents the JS feature that computes for closing in all variables at which a function should have access at, making them available .  (Saves from disposed function exec. context all variables necessary for any other function exec. contexts that have dependencies pointing to space allocated for initial disposed fn context exec.)
    * When there are inner execution contexts disposed, the resulted free variables necessary  for outer scopes executions are stored in JS Engine memory at their latest assigned value. To prevent that could be created a inner IIFE, with local scoped necessary variables passed in as arguments that will return another function in which IIFE’s arguments will be used in execution/return
*  Function Factories -> are using closures for the inner logic of returned functions
* Callbacks  function is a function (cb) passed to another function (main) to be run when it’s (main) execution finishes
call(), apply(), bind()
    * call()-> calls the function with possibility to pass in first argument the this return object
    * apply()->calls the function with first argument the this return object and second argument an array with initial arguments as items
    * bind()-> creates a copy of function that changes this  return value to the object passed as first argument. If initial functions arguments are passed correspondently starting with second position into bind function will automatically  permanent preset values of initial function parameters at execution time (currying= creating copy of function with some preset parameters)
    * All could be used in function borrowing for changing this return object . Bind also could be used for function currying
##  Functional programming
* see ramda

## Object Oriented Javascript & Prototypal
* Inheritance = getting access at object level to other object’s properties and methods
    * Prototypal inheritance: simple, flexible, extensible, easy to understand
        * Any object has a prototype object (pointing to where properties or methods are in memory), that could have his own prototype object and so on=>prototype chain (ends when prototype is Object {})
        * 2 objects can have same prototype 
        * this will return object value with fallback to prototype value.
* Reflection: an object can look at itself , listing and changing its properties and methods

## Building Objects
* Function Constructors- a normal function used to construct objects
    * this variable points to a a new empty object. That object is returned from function
        * new  operator changes this return for the newly created object (inside a function constructor)
    * Prototype is automatically created ,but  is used only by the new operator for creating new object
    * Called without new operator will return undefined
    * Conventionally named starting with Capital letter 
    * Built-In function constructors- Number.prototype.isPositive=function(){return this>=0};var a= new Number(3) ;  a.isPositive();
    * Array, String, Number are function constructors
* Object.create includes pure prototypal inheritance
    * Polyfill- code that adds feature which the engine may lack
* Classes - not present in javascript
        * syntactic sugar = a different way to type something that doesn’t change how it works under the hood
    * class keyword represents objects 
    * is better to use them instead of  function constructors
    * keyword extends sets prototype
## Odds and ends
* Initialization- body of object according with jsEngine expectations
* typeof  -operator that  returns primitive type name as string
    * For objects like d=[]  better use Object.prototype.toString.call(d)
    * typeof null returns ‘object’->is a known bug
    * Typeof function returns string ‘function’ for first class functions
* instance-of - returns true of false if object is result of a defined function constructor
* strict mode -extra function that prevents some errors (mostly typos derived errors)
    * Can be used even independently in function execution context level (“use strict”)
    * Every jsEngine implements use strict differently (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

## Examining Famous Frameworks and Libraries
* Learning from other’s good code
    * Open source code (Angular, jQuery, React, Vue, etc)
    * https://github.com/collections/front-end-javascript-frameworks
* Deep dive into source code
    * DOM (document object model) is separate from jsEngine
    * Method chaining- calling one method after another and each method affects the parent object (done by returning at the end of method this variable)
## Building a Framework/Library
* Structuring safe code
    * Create execution context trough IIFE, passing global context as first param and other libs as consecutive params
* Our object and it’s prototype
    * Share prototype of inner function constructor with lib prototype and expose lib into global object
* Properties and Chainable methods
    * Props declared inside IIFE (protected against mutation)
    * Declare literal functionalities into lib prototype (incapsulated if necessary), making methods chainable by returning this
* Adding support from 3rd party lib (jQuery in example)
    * adding into prototype of lib methods that uses functionalities from incapsulated consecutivelly passed parameters after global context into IIFE structure (or from global context if are available)
* Good commenting
    * is important , being helpful to explain intentions, for knowing later on what was in there at creation time
* Using Framework
    * ; in front of IIFE makes sure code is not parsed wrong when minified along previous code

## Bonus lecture
* Transpile: convert the syntax of one programming language to another
            * Languages that don’t really ever run anywhere are processed by ‘transpilers’ that generate javascript
* Transpiled languages:
    * Typescript (http://www.typescriptlang.org) (http://www.typescriptlang.org/Playground)
    * Traceur   (https://github.com/google/traceur-compiler)
Ecmascript 6.0
*     Existing and upcoming features: (https://github.com/lukehoban/es6features)
Promises, Async and await
* JS is synchronous and single threaded
* https://youtube.com/tonyalicea
* Functions are First class objects: Function that takes another function as parameter, does some work  and runs the parameter after it (concept named as Callback )
* Execution stack have execution contexts , once executed are removed from stack
* JS are embedded in other systems more complex (from where more features ar borowed and handled according to their implementation -  like setTimeout)
* Js provide concept of queue :
    * Modern JS can have multiple queues
    * Queue determines the order of execution in Execution Stack
    * At timeoutHandler end is run a callback 
* Promise:
    * concept: standardised approach to deal with asynchronous events and callbacks
    * Represents a future value that we may get but we do not have yet
* Thinkable object= an object that has a then function
* Syntactic sugar = a different way to type something that doesn’t change how it works under the hood
* Syntactic sugar = features designed to make writing code more efficient, clean, or understandable but, in reality, don’t let you do things that you couldn’t already accomplish before in another way.
* async - await
    * Are syntactic sugar part of JS Engine
    * Rely in promises as concept
    * When await is encountered execution context is paused (sent aside to queue). After Promise waited finishes, the paused execution context is reinserted in stack and continues executions 
    * Code using async - await should be thought as Promises compliant

