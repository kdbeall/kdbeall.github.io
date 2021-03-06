---
layout: post
title: Two Ways of Creating Object Literals in Python
---
First, before diving into Python, let's talk about JavaScript. Here's a refresher of JavaScript's object model from the [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects).

> JavaScript is designed on a simple object-based paradigm. An object is a collection of properties, and a property is an association between a name (or key) and a value.

Because of this simplicity, JavaScript allows for object literals. You don't need a constructor to define an object! This is especially useful for one-off objects.

{% highlight javascript %}
    let car = {
      model: "Skyline",
      manufacturer: "Nissan",
      year: "1996",
      race: function() {
        console.log("Vroom vroom!");
      }
    };
{% endhighlight %}

Here's two approaches to doing the same in Python.

First, from [Programming Ideas with Jake](https://programmingideaswithjake.wordpress.com/2016/05/07/object-literals-in-python/) we can create an Object class and give it a constructor that puts every attribute-value pair into \_\_dict\_\_. Recall that \_\_dict\_\_ is "a dictionary or other mapping object used to store an object’s (writable) attributes."

{%highlight python %}
    class Object:
       def __init__(self, **attributes):
          self.__dict__.update(attributes)

    car = Object(
        model = "Skyline",
        manufacturer = "Nissan",
        year = "1996",
        race = lambda: print("Vroom vroom!")
    )
{% endhighlight %}

So far so good right? There's a few issues that I see. What if *race* were a much more complex function? I would like to have an inline function. Python's lambdas have [caveats](https://www.artima.com/weblogs/viewpost.jsp?thread=147358); things like multi-line lambdas are not allowed. So, instead, we can use class variables and class methods.

{% highlight python %}
    class Car:
        model = "Skyline"
        manufacturer = "Nissan"
        year = "1996"

        @classmethod
        def race(cls):
            print("Vroom vroom!")
            print("Skrrrrt!")
{% endhighlight %}

We can access and use attributes as we would a typical Python object.

{% highlight python %}
      Car.model = "Mustang"
      Car.manufacturer = "Ford"
      Car.race()
{% endhighlight %}

Why is this possible? Because, in Python, classes themselves are objects!
