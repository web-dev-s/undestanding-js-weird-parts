# undestanding-js-weird-parts
resumed ideas from [JavaScript: Understanding the Weird Parts- Anthony Alicea](https://www.udemy.com/course/understand-javascript/)


Execution Context and Lexical Environments:
-Lexical Environment (where declaration bodies reside)
-Execution Environment (stack execution order)
    { 
- Function execution context (at top stack)
- Global execution context (at bottom stack)
     }
-Scope Chain (propagation of scopes from parent to child)
-JavaScript Engine->event Queue (asynchronous behaviour is related to what happens outside JavaScript Engine-> resulted from  execution injection into stack)

Types and Operators:
-dynamic typing (no static typing)
-primitive types: data that represents a single value that is not an object ( 
* undefined -lack of existence, declared by engine
* null- lack of existence, declared by programmer
* boolean- true or false
* number- floating point number
* string- sequence of chars between ‘’, “” or ``
* symbol-starting from ES6

-operators-special function syntactically different written (infixed notation between 2 arguments that return result)

* Precedence (order of call from higher downer) and Associativity (same precedence execution ltr or rtl )
* Coercion -converting a value from one type to another
* Comparison Operators -coercion of booleans to integer boolean (0 or 1) (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
* Existence and Booleans : Boolean(0) coerce to false => a=0; if (a||a===0){’executes true’}
* Default Values : colliding imported libs in global context ,overriding with latest assignment same named global variable value 

Objects and functions:
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
Arrays
* Regular array is a zero based list or collection of items (item can be anything in same array: primitive, object, function, jsx)
Function Overloading
* Does not exist in javascript
* Can be achieved by patterns: creating a function that calls inside overloaded variants
Syntax parser 
* -> goes in code character by character making assumptions
* -> dangerous aside: automatic semicolon insertion. Semicolons insertion should not be let at JavascriptEngine attitude to complete (return {key:’’value} executes as return; {key:’’value} )
* -> whitespace : permissible (permits adding comments in-between declarations for example  with //)
* Immediately invokes function expressions (IIFE) (()=>{})() are creating their execution context that is disposed immediately after execution, avoiding collisions
* Parentheses is the grouping operator containing expressions or IIFE ,  (()=>{}())
Closures
* A closure represents the JS feature that computes for closing in all variables at which a function should have access at, making them available .  (Saves from disposed function exec. context all variables necessary for any other function exec. contexts that have dependencies pointing to space allocated for initial disposed fn context exec.)
    * When there are inner execution contexts disposed, the resulted free variables necessary  for outer scopes executions are stored in JS Engine memory at their latest assigned value. To prevent that could be created a inner IIFE, with local scoped necessary variables passed in as arguments that will return another function in which IIFE’s arguments will be used in execution/return
*  Function Factories -> are using closures for the inner logic of returned functions
* Callbacks  function is a function (cb) passed to another function (main) to be run when it’s (main) execution finishes
call(), apply(), bind()
    * call()-> calls the function with possibility to pass in first argument the this return object
    * apply()->calls the function with first argument the this return object and second argument an array with initial arguments as items
    * bind()-> creates a copy of function that changes this  return value to the object passed as first argument. If initial functions arguments are passed correspondently starting with second position into bind function will automatically  permanent preset values of initial function parameters at execution time (currying= creating copy of function with some preset parameters)
    * All could be used in function borrowing for changing this return object . Bind also could be used for function currying
Functional programming
* 

Object Oriented Javascript & Prototypal
* Inheritance = getting access at object level to other object’s properties and methods
    * Prototypal inheritance: simple, flexible, extensible, easy to understand
        * Any object has a proto object (pointing to where properties or methods are in memory), that could have his own proto object and so on=>prototype chain (ends when proto is Object {})
        * 2 objects can have same proto 
        * this will return object value with fallback to proto value.
* Reflection: an object can look at itself , listing and changing its properties and methods
