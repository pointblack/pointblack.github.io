---
layout:     post
title:      Moment.js - Reduce Webpack Bundle Size
date:       2018-02-03 23:11
summary:    How to reduce the packaged webpack bundle size of moment.js
categories: react
---

Working with Javascript using Vanilla Javascript can be tricky sometimes. Especially, when introducing different time zone support to an application.

A very good library helping with date handling is [Moment.js](http://momentjs.com/).
Unfortunately, when bundling moment.js using webpack (v3) with default settings, it results in a rather large package size of 455kb.

Using the plugin [Webpack Bundle Analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer)
helps to spot that the large package size is a result of including all different locales:

![Before]({{ "/images/moment-webpack-before.png" | absolute_url }})

To reduce the bundle size, we configure webpack using `webpack.ContextReplacementPlugin` to only bundle locales used within the application, in following case DE & EN locales.

We add following snippet to the `webpack.config.js` file:

{% highlight javascript %}
new webpack.ContextReplacementPlugin(
  /moment[\/\\]locale$/,
  /de|en/
)
{% endhighlight %}

![After]({{ "/images/moment-webpack-after.png" | absolute_url }})

The result is a reduced package size of 125kb.
