---
layout: post
title:  "Functions"
date:   2017-10-19 18:01:00 +1100
categories: functions
---

Random but important things about functions

### 1. function declaration

Function declarations are read and added to the execution context before the code is executed. This is why they can be used before they are declared. This is commonly known as _hoisting_. It is of noteworthy mention that hoisting is just a metaphor and it does not actually move your code to the top of the script.

{% highlight javascript %}

  sayHello() // 'Hello'

  function sayHello() {
    console.log('Hello');
  }

{% endhighlight %}

### 2. named functions are just pointers

Functions are Objects and Objects are reference types. Therefore named functions are simply pointers to the function and is not the function itself.

{% highlight javascript %}

  function someFunction() {
    console.log('1');
  }

  var a = someFunction;

  someFunction = null;

  a(); // 1

{% endhighlight %}

Both `a` and `someFunction` are simply pointers to the same function. This is verifiable when `someFunction` is deferenced. Because `someFunction` is simply a pointer and not the function itself, deferencing `someFunction` has no effect on `a`, `a` is still pointing to the 'real' function.


### 3. special objects
Two special objects exist inside a function: `arguments` and `this`.

The `arguments` object is an array-like object that contains all the arguments passed into the function. Arguments can be accessed via bracket notation and also has a length property.

{% highlight javascript %}

  function greet() {
    console.log('Hello' + ' ' + arguments[0]);
    console.log(arguments.length)
  }

  greet('John'); // Hello John
                 // 1

{% endhighlight %}

As you can see, the `greet` function does not have a named argument but because of the internal `arguments` object, we can pass in the string 'John' and reference this argument inside the function body.

Named function arguments are a convenience and not a necessity although it is still the preferred way of writing functions.

The `arguments` object also has a property called `callee`.

The `callee` property is a pointer to the function that owns the `arguments` object. This property is basically a reference to the function itself. This is useful in recursive functions when you need the correct function to be called, essentially decoupling it from a specific function name.

<br>
<hr>
<br>

> The `this` value is a reference to the context object that the function is operating on.

&ndash; Nicholas Zakas, Professional JavaScript for Web Developers

The `this` value is contingent upon the context object, whether it be the global context, function context, or an object.

{% highlight javascript %}

  var value = 'chicken';

  var object = {
    value: 'cow',
    sayThis: sayThis
  }

  function sayThis() {
    console.log(this.value);
  }

  function sayThis2(val) {
    this.value = val;
    console.log(this.value);
  }

  sayThis(); // Global context - chicken

  sayThis2('sheep'); // Function Context - sheep

  object.sayThis(); // object - cow

{% endhighlight %}
