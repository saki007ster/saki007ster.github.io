---
layout: post
title: Sass Styleguide
---


We are now using css pre-processors [sass/less/styl] in almost all the projects, thus it would be better if we follow some guideline so that our code is consistent and maintainable.

Take this as a sass style guide but you need to follow css style guide as well, which we are following already.
- Be consistent with indentation
- Be consistent about where spaces before/after colons/braces go
- One selector per line, One rule per line
- List related properties together
- Have a plan for class name naming
- Minimise the use if ID's

## 1. List @extend(s) First

{% highlight css %}
.weather {
  @extends %module;
  ...
}
{% endhighlight %}

Knowing right off the bat that this class inherits another whole set of rules from elsewhere is good.


## 2. List "Regular" Styles Next
{% highlight css %}
.weather {
  @extends %module;
  background: LightCyan;
  ..
}
{% endhighlight %}

List @include(s) Next

{% highlight css %}
.weather {
  @extends %module;
  background: LightCyan;
  @include transition(all 0.3s ease-out);
  ...
}
{% endhighlight %}

This visually separates the @extends and @includes as well as groups the @includes for easier reading.


## 3. Nested Selectors Last

{% highlight css %}
.weather {
  @extends %module;
  background: LightCyan;
  @include transition(all 0.3s ease);
  > h3 {
    border-bottom: 1px solid white;
    @include transform(rotate(90deg));
  }
}
{% endhighlight %}

Nothing goes after the nested stuff. And the same order as above within the nested selector would apply.


## 4. All Vendor Prefixes Use @mixins

You must update mixins (or the libraries you use will update) to reflect those changes. Even if the mixin ends up being a one-liner, that's OK.



## 5. Maximum Nesting: Three Levels Deep

{% highlight css %}
.weather {
  .cities {
    li {
      // no more!
    }
  }
}
{% endhighlight %}

Chances are, if you're deeper than that, you're writing a crappy selector. Crappy in the sense that it's too reliant on HTML structure (fragile), overly specific (too powerful), and not very reusable (not useful). It's also on the edge of being difficult to understand.

If you really want to use tag selectors because the class thing is getting too much for you, you may want to get pretty specific about it to avoid undesired cascading. And possibly even make use of extend so it has the benefit on the CSS side of re-usability.

{% highlight css %}
.weather
  > h3 {
    @extend %line-under;
  }
}
{% endhighlight %}

## 6. Maximum Nesting: 50 Lines


If a nested block of Sass is longer than that, there is a good chance it doesn't fit on one code editor screen, and starts becoming difficult to understand. The whole point of nesting is convenience and to assist in mental grouping. Don't use it if it hurts that.


## 7. Break Into As Many Small Files As Makes Sense

There is no penalty to splitting into many small files. Do it as much as feels good to the project. I know I find it easier to jump to small specific files and navigate through them than fewer/larger ones.

{% highlight css %}
@import "global/header/header/";
@import "global/header/logo/";
@import "global/header/dropdowns/";
@import "global/header/nav/";
@import "global/header/really-specific-thingy/";
{% endhighlight %}

I'd probably do this right in the global.scss, rather than have global @import a _header.scss file which has its own sub-imports.



## 8. Partials are named _partial.scss

This is a common naming convention that indicates this file isn't meant to be compiled by itself. It likely has dependancies that would make it impossible to compile by itself. Personally I like dashes in the "actual" filename though, like _dropdown-menu.scss.


## 9. Be Generous With Comments

It is rare to regret leaving a comment in code. It is either helpful or easily ignorable. Comments get stripped when compiling to compressed code, so there is no cost.

{% highlight css %}
.overlay {
  /* modals are 6000, saving messages are 5500, header is 2000 */
  z-index: 5000;
}
{% endhighlight %}

And speaking of comments, you may want to standardize on that. The // syntax in Sass is pretty nice especially for blocks of comments, so it is easier to comment/uncomment individual lines.



## 10. Variablize All Colors Common Numbers, and Numbers with Meaning


If you find yourself using a number other than 0 or 100% over and over, it likely deserves a variable. Since it likely has meaning and controls consistency, being able to tweak it enmasse may be useful.

If a number clearly has strong meaning, that's a use case for variablizing as well.

{% highlight css %}
$zHeader: 2000;
$zOverlay: 5000;
$zMessage: 5050;

.header {
  z-index: $zHeader;
}
.overlay {
  z-index: $zOverlay;
}
.message {
  z-index: $zMessage;
}
{% endhighlight %}

Those numbers are probably in a separate file @import-ed as a dependency. That way you can keep track of your whole z-index stack in one place.

Variations on that color can often be handled by the Sass color functions like lighten() and darken() - which make updating colors easier (change in one place, whole color scheme updates).



## 11. Nest and Name Your Media Queries

The ability to nest media queries in Sass means 1) you don't have to re-write the selector somewhere else which can be error prone 2) the rules that you are overriding are very clear and obvious, which is usually not the case when they are at the bottom of your CSS or in a different file.



## 12. Quick Fixes in the Last

In your global stylesheet, @import a _quickfix.scss file last.

{% highlight css %}
@import "compass"

...

@import “quickfix"
{% endhighlight %}

If you need to make a quick fix, you can do it here. Later when you have proper time, you can move the fix into the proper structure/organization.


Hope above guideline would be helpful for you guys.
