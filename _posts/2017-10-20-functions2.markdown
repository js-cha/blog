---
layout: post
title: "Prototype Chaining"
date: 2017-10-20 1:4:00 +1100
categories: prototype chaining
---

### Constructors

Constructors are functions that create a specific type of object.

There are native constructors such as `Object` and `Array`.

Instances can be created by calling the constructor with the `new` operator. Alternatively, you can use the literal syntax.

{% highlight javascript %}

  var obj = new Object(); // creates a new Object
  var obj2 = {}; // literal syntax, same as above

  var arr = new Array(); // creates a new Array
  var arr2 = []; // literal syntax, same as above

{% endhighlight %}

<br>

### \__proto__

Every instance of a particular object has a special internal property that points back to the constructor's prototype, this is called: `[[Prototype]]` or `__proto__` (interchangeably used).

Essentially, this signifies a direct link between the instance and the constructors `prototype`.

{% highlight javascript %}

  var obj = new Object();
  console.log(obj); // __proto_: Object

  var arr = new Array();
  console.log(arr); // __proto_: Array(0)

{% endhighlight %}

<br>

### prototype

*Not to be confused with the internal `[[Prototype]]` property.*

Every function has a `prototype` property.

This property is an object containing all the methods and properties shared by instances of this particular type. It also has a constructor property that points back to the constructor.

If we examine the `Array` constructor's `prototype` property, we can observe the following:

{% highlight javascript %}
console.log(Array.prototype);

// All the methods and properties
concat: ƒ concat()
constructor: ƒ Array()
copyWithin: ƒ copyWithin()
entries: ƒ entries()
every: ƒ every()
fill: ƒ fill()
filter: ƒ filter()
find: ƒ find()
findIndex: ƒ findIndex()
forEach: ƒ forEach()
includes: ƒ includes()
indexOf: ƒ indexOf()
join: ƒ join()
keys: ƒ keys()
lastIndexOf: ƒ lastIndexOf()
length: 0
map: ƒ map()
pop: ƒ pop()
push: ƒ push()
reduce: ƒ reduce()
reduceRight: ƒ reduceRight()
reverse: ƒ reverse()
shift: ƒ shift()
slice: ƒ slice()
some: ƒ some()
sort: ƒ sort()
splice: ƒ splice()
toLocaleString: ƒ toLocaleString()
toString: ƒ toString()
unshift: ƒ unshift()
Symbol(Symbol.iterator): ƒ values()
Symbol(Symbol.unscopables):
{copyWithi: true, entrie: true, fil: true, fin: true, findInde: true, …}
__proto__: Object
{% endhighlight %}

The above list is a collection of all the methods and properties available to instances of the `Array` object.

This is the reason why we can use methods such as `push` and `pop` on our array literal.

{% highlight javascript %}

  var arr = ['apricot', 'blueberry', 'clementine'];

  arr.push('dragon fruit')

{% endhighlight %}

Notice at the end, the prototype also has an internal `__proto__` property pointing to `Object`. This is because all reference types inherit from `Object` and are therefore objects.

But more importantly, this is the primary method of inheritance in JavaScript, prototype chaining.

### Tying it all together

What if our constructor's prototype was an instance of another type?

{% highlight javascript %}

  function Animal() {
    // ...
  }

  Animal.prototype.howManyLegs = 4;
  Animal.prototype.hasTail = true;

  function Cat() {
    // ...
  }

  Cat.prototype = new Animal();

  Cat.prototype.meow = function() {
    return 'Meow';
  }

  var cat = new Cat();

  console.log(cat.hasTail); // true
  console.log(cat.meow());  // 'Meow'
  console.log(Animal.prototype.isPrototypeOf(cat)); // true
  console.log(Cat.prototype.isPrototypeOf(cat));    // true

{% endhighlight %}

By manipulating the constructor's prototype property to be an instance of another type, we can a create prototype chain. This is how a subtype inherits properties and methods from a supertype.

### Conclusion

Inheritance is achieved through prototype chaining by altering the constructor function's prototype to be an instance of another type.