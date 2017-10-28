---
layout: post
title: "Event flow"
date: 2017-10-28 21:52:00 +1100
categories: event flow
---

A DOM event flow has three phases:

  * event capturing
  * at target
  * event bubbling

### event capturing
The first phase of the event occurs from the root node `document` and travels down to the target specific node.

### at target
At target is literally when the event flow has reached the target

### event bubbling
This last phase is the inverse of the first phase, the event flow travels back up to the highest node in the DOM. This phase can be stopped by calling `stopPropagation()`.

Example scenario: second `li` element is clicked.
{% highlight html %}
  <ul>
    <li>one</li>
    <li onclick="function() { console.log('hello') }">two</li>
    <li>three</li>
  </ul>
{% endhighlight %}


Phase 1: event capturing
```
--> document
  -->  html
    -->  body
      -->  ul
        -->  li
```

Phase 2: at target
```
--> li
```

Phase 3: event bubbling
```
        --> document
      --> html
    --> body
  --> ul
--> li
```

### Why?

Because the DOM is represented as a tree-like heirarchy of nodes, nested within each other&mdash;An element does not exist in it's own space but rather is contained within other elements.

Consider a series of concentric circles&mdash;if a user clicked in the middle, it essentially would touch every circle.

Event bubbling is the mechanism for event delegation&mdash;when the parent element is responsible for handling events triggered from its child elements.