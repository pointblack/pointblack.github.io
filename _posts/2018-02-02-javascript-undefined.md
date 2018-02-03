---
layout:     post
title:      Javascript condition & 0 value
date:       2018-02-02 11:21:29
summary:    How to prevent headaches with 0 values and javascript conditions
categories: react
---

Recently i had to debug an error caused by a javascript condition:

{% highlight javascript %}
  if (utcOffset) {
    // do fancy things
  }
{% endhighlight %}

The problem with `utcOffset` param is that i can be a `0` value.

Unfortunatley there is no better way to solve this using the following condition:

{% highlight javascript %}
  if (utcOffset !== undefined && utcOffset !== null) {
    // do fancy things
  }
{% endhighlight %}

This way a `0` value will be passing the condition.
