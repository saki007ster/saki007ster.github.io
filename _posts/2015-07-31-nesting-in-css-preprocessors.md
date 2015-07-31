---
layout: post
title: Nesting in CSS Preprocessors
---

Nesting is supposed to make your CSS easier to read, extend, and maintain. For some situations, it does, but for designing CSS systems at scale, nesting your CSS is almost always a terrible idea. Allow me to explain with some general assumptions and examples.

### Assumptions
No matter the build tool or preprocessor, there are a small set of general CSS guidelines I think most folks can agree on:

- Less number of compiled CSS lines is better.
- Less specificificity of CSS selectors is better.
- Smaller compiled file size is better.
- Component-based CSS is better for readability.

### Nesting elements
I find this to be the most common form of nesting and is probably just fine for most sites. It’s not necessarily bad, but nesting like this makes your CSS more specific. It also doesn’t force you to write reusable components, which is what you want for building most apps.

{% highlight css %}
.parent {
  h1 { }
  span { }
  a { }
}
{% endhighlight %}

Consider rewriting that code to something like:

{% highlight css %}
.parent-heading { }
.parent-subheading { }
.parent-permalink { }
{% endhighlight %}

Those classes have lower specificity, more meaningful selectors, and are component-based.

Nesting classes
Nested classes means you’re heading in the right direction, but are held back by overly specific CSS.

{% highlight css %}
.parent {
  .parent-child { }
  .parent-child2 { }
  .parent-modifier { }
  .parent-modifier2 { }
}
{% endhighlight %}

You’ve got a parent element encapsulating all the children classes, but those children classes are already properly scoped as legit classes. Rewrite it just by removing the parent:

{% highlight css %}
.parent-child { }
.parent-child2 { }
.parent-modifier { }
.parent-modifier2 { }
{% endhighlight %}

The result is the same number of selectors, but with lower specificity.

### Un-nesting with &
The un-nesting example is perhaps the most confusing way to nest CSS.

{% highlight css %}
.child {
  .parent & { }
}
{% endhighlight %}

When used at the end of a nested selector, the & puts everything to the left of it before the parent selector. So the above example compiles to .parent .child { }. This is confusing in a few ways:

The & puts that selector at the beginning of the top-most parent.
It’s the opposite of how regular nesting works.
It clouds your vision of the compiled CSS.
Rather than go that route, try something like this:

{% highlight css %}
.child { }
.child-modifier { }
{% endhighlight %}

The result is a component-based approach with lower specificity and clearer insight into what your compiled CSS will be.

### BEM nesting with &
Nesting for BEM—or any other flavor CSS architecture—is helpful at first, but comes as a cost.

{% highlight css %}
.block {
  &__element { }
  &--modifier { }
}
{% endhighlight %}

While you’re saving a few bytes in your source file by not writing .block each time, you lose out on the ability search for your classes. When you’re debugging something with a browser’s Inspector, you only see the final, compiled class. So, when you need to search your code base for .block__element, you won’t find it. That’s easy enough to get around, but that’s unnecessary cognitive overhead.

Instead, keep it simple and just write it all out:

{% highlight css %}
.block__element { }
.block--modifier { }
{% endhighlight %}

Easy to read, easy to search, and with no sacrifice to your compiled CSS.

### Nesting pseudo-classes with &
Nesting with pseudo-classes feels like the only practical way to nest your CSS.

{% highlight css %}
.btn {
  &:hover,
  &:focus { }

  &:active { }
}
{% endhighlight %}

What makes it different from the previous example is that this is all one element and class, just with different states. It’s not multiple half-classes that do different things. That means searching your codebase for it is super easy and more intuitive—just find .btn.

Moreover, and perhaps more helpful, is this makes your code more mixin- and extend-friendly (though the true merits of the latter are up for debate).

### Wrapping up
Bottom line? If you’re building pretty simple sites, nest to your heart’s content. However, if you’re building large apps or sites—Twitter, Bootstrap, GitHub, NY Times, etc—avoid it and keep your CSS simple, performant, and easy to parse.
