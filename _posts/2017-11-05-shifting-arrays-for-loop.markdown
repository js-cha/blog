---
layout: post
title: "How to left/right shift an array using a for loop"
date: 2017-11-05 20:55:00 +1100
categories: algorithm techniques
---

### Right shift an array by 1:

{% highlight javascript %}
  function shiftArray(array) {
    var i;

    for (i = array.length - 2; i >= 0; i--) {
      array[i + 1] = array[i];
    }

    console.log(array);
  }

  shiftArray([4, 3, 6, 1]);
  // [4, 4, 3, 6]
{% endhighlight %}

### Left shift an array by 1:

{% highlight javascript %}
  function shiftArray(array) {
    var i;

    for (i = 1; i < array.length; i++) {
      array[i - 1] = array[i];
    }

    console.log(array);
  }

  shiftArray([4, 3, 6, 1]);
  // [3, 6, 1, 1]
{% endhighlight %}