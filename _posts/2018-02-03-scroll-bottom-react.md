---
layout:     post
title:      Scroll Bottom With React
date:       2018-02-03 11:21:29
summary:    Scrolling with React using the Lifecycle Methods and Dom Reference
categories: react
---

One example could be to have a react component to render comments with CSS Scrolling. When adding a new comment it should autoscroll to the bottom to always view the last comment.

To solve this we are going to use React Lifecycle methods `componentWillUpdate` and `componentDidUpdate`

{% highlight javascript %}
<div ref={(node) => { this.node = node; }}>
  <Comments />
</div>
{% endhighlight %}

In the `componentWillUpdate` we use the ref to set a boolean `shouldScrollBottom` using scrollTop and `offsetHeight`

{% highlight javascript %}
componentWillUpdate() {
    const node = this.node;
    this.shouldScrollBottom = node.scrollTop + node.offsetHeight === node.scrollHeight;
}
{% endhighlight %}

In `componentDidUpdate` we use the bool `shouldScrollBottom` to scroll to the bottom.

{% highlight javascript %}
componentWillUpdate() {
    const node = this.node;
    this.shouldScrollBottom = node.scrollTop + node.offsetHeight === node.scrollHeight;
}
{% endhighlight %}
