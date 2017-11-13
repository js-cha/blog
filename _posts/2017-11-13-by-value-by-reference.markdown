---
layout: post
title: "By value, by reference"
date: 2017-11-05 20:55:00 +1100
categories: primitives references backtobasics
---

JavaScript - Back to Basics

Primitive types:

* Null (empty object pointer, `typeof` evaluates to 'object')
* Undefined (this value is actually a derivative of `Null`)
* Boolean
* Number
* String

Reference types:

* Object
* Array
* Functions

### By value

Primitive types have a fixed size in memory. When a variable holds a primitive value, it holds the actual value.

When you copy the value of one variable to another, there are no side-effects because it is passed by value - this essentially creates a separate copy.

{% highlight javascript %}
  var a = 'apple';
  var b = a;
  b = 'banana';

  console.log(a); // apple
  console.log(b); // banana
{% endhighlight %}

### By reference
Reference types do not have a fixed size in memory, therefore when a variable holds a reference type it does not contain the reference value itself but it is simply a pointer to the object on the memory heap.

{% highlight javascript %}
  var a = ['apple', 'acqua', 'ace'];
  var b = a;
  a = null;

  console.log(a); // null
  console.log(b); // ['apple', 'acqua', 'ace']
{% endhighlight %}

Because both 'a' and 'b' are simply *pointers* to the same Object, deferencing 'a' does not affect 'b' because 'a' does not hold the value itself - the actual value cannot be accessed. In this example, deferencing is just another way of saying - I no longer want to point to/reference an object - connection closed.

### Functions
Interestingly, regardless of the type, all function arguments are passed in by value. Although they behave accordingly to their type, the values are passed in by value.

{% highlight javascript %}
  var person = {
    name: 'Joseph'
  };

  function setAgeProperty(obj) {
    obj.age = 25;
    obj = null;
    console.log(obj);
  }

  setAgeProperty(person); // null;
  console.log(person); // {name: 'Joseph'}

{% endhighlight %}

Inside the function `setAgeProperty` what is happening is the `person` object that was passed in, is now essentially a local variable that points to the same object as the global `person` object. Theoretically, if it was passed in by reference, console logging 'person' should yield null however its reference remains intact.