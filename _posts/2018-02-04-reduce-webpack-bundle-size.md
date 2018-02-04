---
layout:     post
title:      Moment.js - Reduce Webpack Bundle Size
date:       2018-02-03 23:11
summary:    How to reduce the packaged webpack bundle size of moment.js
categories: react
---

A very good library which helps with date handling in Javascript is [Moment.js](http://momentjs.com/).
Unfortunately when bundling  moment.js using webpack (v3) with default settings, it results in a rather large package of 455kb size.

Using the helpful plugin [Webpack Bundle Analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer)
it is easy to spot that the package size results of including all supported locales:

![Before]({{ "/images/moment-webpack-before.png" | absolute_url }})

To reduce the bundle size, we configure webpack using `webpack.ContextReplacementPlugin` to only bundle locales used within the application, in following case DE & EN locales.

We add following snippet to the `webpack.config.js` file:

{% highlight javascript %}
new webpack.ContextReplacementPlugin(
  /moment[\/\\]locale$/,
  /de|fr/
)
{% endhighlight %}

![After]({{ "/images/moment-webpack-after.png" | absolute_url }})

The result is a reduced package size of 125kb.
