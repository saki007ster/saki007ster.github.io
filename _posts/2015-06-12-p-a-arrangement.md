---
layout: post
title: Arrangement order of Paragraph and anchor tags
---

## Question
If you have text in a box that you want to turn into a hyperlink, which is correct...

Option #1:
{% highlight html %}<p><a href=''>Call for an appointment</a></p> {% endhighlight %}

Option #2:
{% highlight html %}<a href=''><p>Call for an appointment</p></a>{% endhighlight %}

## Solution

In html5 either are valid2 as 'a' elements can now contain flow-content as well as phrase content (but not interactive elements like other anchors or objects etc ).

Again context is the key and if you have a text block that needs to be a link you can do this.

{% highlight html %}
<a href="link.html">
  <h3>A heading</h3>
  <p>Something to do with the heading lorem ipsum dolor sit amet lorem ipsum dolor sit amet lorem ipsum dolor sit amet lorem ipsum dolor sit amet lorem ipsum dolor sit amet.</p>
  <p>Read more</p>
</a>
{% endhighlight %}

(If you use the above method its best to set the anchor to display:block to help older browsers).

If you just have the one phrase then just put the anchor around the phrase.

{% highlight html %}
<p> <a href=''>Call for an appointment</a></p>
{% endhighlight %}
