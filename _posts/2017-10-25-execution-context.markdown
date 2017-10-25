---
layout: post
title: "Execution Context"
date: 2017-10-25 21:52:00 +1100
categories: execution context
---

The execution context defines what variables and functions it has access to.

There are two primary execution contexts:

- Global context
- Function context

The global execution context is the outermost context and is equivalent to the root parent. It is from the global context that all variables and functions are declared.

In a web browser, the `window` object is said to be the global context.

### *variable object*
Each execution context has a *variable object*. This object contains all the variables and functions defined within its context. This object is not accessible by code and is used behind the scenes.

### *activation object*
Functions use an *activation object* instead of the variable object, but they play an identical role in the scope chain. The activation object is first initialised with its own internal array-like `arguments` object.


### scope chain
A scope chain is an ordered list of variable/activation objects. Whenever code is executed, an associated scope chain is created to provide access to variables and functions that it has access to. The front of the scope chain is always the variable/activation object of the current context that the code is executing on. While the end/back of the scope chain is always the global context/window object.

{% highlight javascript %}

var globalcontext = 'root'

function parent() {
  var surname = 'Doe';

  function child() {
    var name = 'James' + ' ' + surname;
  }
}
{% endhighlight javascript %}

In the above example, three scope chains are created, one for the global context, one for `parent()` and one for `child()`.


Within the global execution context, the scope chain consists of a single variable object that holds the `globalcontext` variable and the `parent` function. It can only call the `parent` function but cannot access the data that is inside of it.

```
Scope Chain:
[0]: variable object: {
  globalContext: 'root',
  parent: Function
}
```

The `parent` function context has a scope chain that consists of two objects: the variable object of the global context, and its own activation object.

```
Scope Chain:
[1]: variable object: {
      globalContext: 'root',
      parent: Function
    }
[0]: activation object: {
      arguments: [...]
      surname: 'Doe'
    }
```

The `child` function execution context has a scope chain that consists of everything inside the parent scope chain, plus its own activation object.

```
Scope Chain:
[2]: variable object: {
      globalContext: 'root',
      parent: Function
    }
[1]: activation object: {
      arguments: [...]
      surname: 'Doe'
    }
[0]: activation object: {
      arguments: [...]
      name: James' + ' ' + surname;'
    }
```

The reason why the inner function can access the parent function's variable is because of the look-up that happens in the scope chain. If something can't be found within the front the scope chain, i.e. its own variable object, it will then continue looking up the chain until the identifier is found.

### Conclusion
The scope chain always looks up. The parent context can never look down and access anything inside of its children&mdash;likewise with the global execution context.

It is likened to a parent child relationship. The child inherits and receives its traits and characteristics from the parent. But the inverse is never true. The parent does not inherit anything from it's child.