---
layout: post
title: "Closures"
date: 2018-1-11 21:57:00 +1100
categories: scope closure backtobasics
---

### Closures

A closure is when an inner function has access to its outer scope's variables even after execution. Rather than being garbage-collected, the inner function closes over the parent function's scope and preserves the variable that it is referencing.

{% highlight javascript %}

function someFunc() {
  var a = "apple";
}

someFunc();

{% endhighlight %}

The variable `a` is defined within the function scope of `someFunc`. Because this variable is not referenced or used anywhere else within the function, it is marked for garbage collection.

If we were to somehow preserve the variable `a` even after invoking `someFunc`, we would need to introduce an inner function that references it from its scope thus preventing it from being garbaged collected.

{% highlight javascript %}

function someFunc() {
  var a = "apple";

  return function someOtherFunc(statement) {
      console.log(`${statement} ${a}`);
  }
}

var closure = someFunc(); // var a is still in memory

closure("I love"); // I love apple

{% endhighlight %}

Unlike the previous example, variable `a` is not garbaged collected and still kept in memory even after being invoked within the variable `closure`. We can invoke the function again returning the inner function where the variable is used. Once the inner function has run, the closure is no more and the variable is freed for garbage collection.
