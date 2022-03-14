---
layout: post
title: Quick notes on Effective Go
---

[Effective Go](https://golang.org/doc/effective_go) is an excellent guide to being fluent in Go.

* [Appending a slice to a slice](https://go.dev/doc/effective_go#append)

    {% highlight go %}
    // Use ...
    x := []int{1,2,3}
    y := []int{4,5,6}
    x = append(x, y...)
    {% endhighlight %}

* [Short declaration re-assignments](https://golang.org/doc/effective_go#redeclaration) "Err appears in both statements. This duplication is legal: err is declared by the first statement, but only re-assigned in the second."

    {% highlight go %}
    // This is okay
    fp, err := os.Open(fName)
    d, err := fp.Stat()
    {% endhighlight %}

* [Defer](https://golang.org/doc/effective_go#defer) "It is an effective way to deal with situations such as resources that must be released regardless of which path a function takes to return."

* [Getters and setters](https://golang.org/doc/effective_go#package-names) "It's neither idiomatic nor necessary to put Get into the getter's name."

    {% highlight go %}
    // This is correct
    prop := foo.Property()
    {% endhighlight %}

    {% highlight go %}
    // Don't do this
    prop := foo.GetProperty()
    {% endhighlight %}

* [new](https://golang.org/doc/effective_go#allocation_new) "Beginners are confused by the distinction between the allocation routines make and new."

This [post](https://groups.google.com/g/golang-nuts/c/kWXYU95XN04/m/iRfB7YEt57UJ) by Rob Pike describes how new was almost removed.

    {% highlight go %}
	v := new(int)
	*v++
	fmt.Println(*v)
    {% endhighlight %}
