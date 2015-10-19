---
layout: post
title: Web Components and Polymer - Introduction to the future web
---

The web now has evolved a lot, it has grown from static sites those in 90's to dynamic application building platform. It is a growing universe of interlinked web pages and web apps, teeming with videos, photos, and interactive content. What the average user doesn't see is the interplay of web technologies and browsers that makes all this possible.

Over time web technologies have evolved to give web developers the ability to create new generations of useful and immersive web experiences. This is shown [here](http://www.evolutionoftheweb.com/#/evolution/day). But as it grows it is becoming more complex, at the time of static sites it used to few pages, no heavy markup but now going through the html markup of the application is a headache and we have css, js of more than thousands of lines which makes it impossible to comprehend in a single go.

Also the evolution signifies that the most famous client side projects are fated to die, though a pretty strong statement but true. Think of stuffs what happened in past like flash which had no replacement in its time, with all fancy transitions, animations. Then technology like canvas and css transitions came into picture and platform realised that people need something to do animations so it was integrated in browsers and flash was dead. Similarly with jQuery, when it came it was very difficult to manipulate DOM as we had different browsers implementing DOM rendering differently, but John Resig made DOM manipulations very easy with jQuery and thus it became very popular. There was a time when people used to learn jQuery before javascript as it was easy and more effective. But with the advent of Angular.js for DOM manipulation the web developers have more power in their hands. Also platform has realised that DOM manipulation is basic need for web apps, so it must be integrated as browsers standards thus webcomponents have come to the picture. So the gist is that the projects which becomes need and are important in long run get integrated in the browsers, this is how the browsers are evolving with time making the web platform more robust and flexible. 

The way we develop our applications is not upto the mark, today in order to complete our task in time with too many feature we tend to rely on the already developed feature which may or may fit into our requirement but we tweak it little bit hoping that it would work fine if not then we go to similar implementation by some different vendor, without realizing the complexity we are adding in. 
For example if we have to develop some kind of image slider we just google it and we find n numbers of sliders already implemented, we download any particular implementation trying to fit in our project, if it does not work we go to other - repeating the steps till it satisfies our need 

As a problems like divitis, unmaintainability creeps in the due to complexity in the large application there must be some way out of it. If we analize our modern web applications they are not only complex to design but also quite difficult to develop. Given the range of tools involved, amount of testing required, and the combination of libraries/frameworks used, the development process has become harder. As the application scales over a period of time, it becomes harder to maintain the code and make enhancements.

For instance, take a look at the frontend code of these few popular websites:


[image]


The complex DOM structure of morder web applications is largely due to indiscriminate use of divs and spans. HTML5 was brought into picture to resolve this issue with symantic markup, but it still falls shart due to following reasons: 

- We have too many similar components in our web page that fall under the same semantic structure. To distinguish them from each other, we use classes, IDs, or other attributes.
- The available list of semantic tags are simply not enough to target the wide variety of components that constitute our design. As a result, we fall back to traditional tags like div or span.

## Web componets to the rescue

The W3C aims to address this problem by introducing Web Components. Web components are a collection of specifications that enable developers to create their web applications as a set of reusable components. 

Each component lives in its self-defined encapsulated unit with corresponding style and behavior logic. These components can not only be shared across a single web application but can also be distributed on the web for use by others.

It is the combinations following 4 specifications:

- **Custom Elements** – These enable developers to create their own elements that are relevant to their design as part of the DOM structure with the ability to style/script them just like any other HTML tag.
- **HTML Templates** – These let you define fragments of markup that stay consistent across web pages with the ability to inject dynamic content using JavaScript.
- **Shadow DOM** – This is designed to abstract all the complexities from the markup by defining functional boundaries between the DOM tree and the subtrees hidden behind a shadow root.
- **HTML Imports** – Similar to import one CSS file into another, these allow you to include and reuse HTML documents in other HTML documents.

## Custom Elements
Custom Elements allow web developers to define new types of HTML elements.

Web Components don't exist without the features unlocked by custom elements:

- Define new HTML/DOM elements
- Create elements that extend from other elements
- Logically bundle together custom functionality into a single tag
- Extend the API of existing DOM elements

### Registering a custom element

{% highlight html %}
<my-element></my-element>
{% endhighlight %}

{% highlight js %}
var proto = Object.create(HTMLElement.prototype);

proto.createdCallback = function() {
  this.textContent = "Hello, this is my-element !!";
};

document.register('my-element', {
  prototype: proto
});
{% endhighlight %}

### Lifecycle callback methods

- **createdCallback** - an instance of the element is created
- **attachedCallback** - an instance was inserted into the document
- **detachedCallback** - an instance was removed from the document
- **attributeChangedCallback(attrName, oldVal, newVal)** - an attribute was added, removed, or updated

All of the lifecycle callbacks are optional.


## HTML Templates

HTML Templates are another new API primitive that fits nicely into the world of custom elements.

The &lt;template&gt; element allows you to declare fragments of DOM which are parsed, inert at page load, and instantiated later at runtime. They're an ideal placeholder for declaring the structure of custom element.

Example: registering an element created from a &lt;template&gt; and Shadow DOM:

{% highlight html %}
<template id="mycustomtemplate">
  <style>
    p { color: orange; }
  </style>
  <p>I'm in Shadow DOM. My markup was stamped from a &lt;template&gt;.</p>
</template>

<script>
  var proto = Object.create(HTMLElement.prototype, {
    createdCallback: {
      value: function() {
        var t = document.querySelector('#mycustomtemplate');
        var clone = document.importNode(t.content, true);
        this.createShadowRoot().appendChild(clone);
      }
    }
  });
  document.registerElement('x-foo-from-template', {prototype: proto});
</script>
{% endhighlight %}


## Shadow DOM

Shadow DOM is a powerful tool for encapsulating content. Use it in conjunction with custom elements and things get magical!

Shadow DOM gives custom elements:

- A way to hide their guts, thus shielding users from gory implementation details.
- Style encapsulation.

Creating an element from Shadow DOM is like creating one that renders basic markup. The difference is in createdCallback():

{% highlight js %}
var XFooProto = Object.create(HTMLElement.prototype);

XFooProto.createdCallback = function() {
  // 1. Attach a shadow root on the element.
  var shadow = this.createShadowRoot();

  // 2. Fill it with markup goodness.
  shadow.innerHTML = "<b>I'm in the element's Shadow DOM!</b>";
};

var XFoo = document.registerElement('x-foo-shadowdom', {prototype: XFooProto});
{% endhighlight %}


## HTML Imports

HTML Imports, part of the Web Components cast, is a way to include HTML documents in other HTML documents. You're not limited to markup either. An import can also include CSS, JavaScript, or anything else an .html file can contain. In other words, this makes imports a fantastic tool for loading related HTML/CSS/JS.

Include an import on your page by declaring a <link rel="import">:

{% highlight html %}
<head>
  <link rel="import" href="/path/to/imports/stuff.html">
</head>
{% endhighlight %}

The URL of an import is called an import location. To load content from another domain, the import location needs to be CORS-enabled:

{% highlight html %}
<!-- Resources on other origins must be CORS-enabled. -->
<link rel="import" href="http://example.com/elements.html">
{% endhighlight %}


## What is Polymer?

The specifications introduced above are quite new and it is hardly surprising to know that browser support is not very good. But, thanks to the Polymer library, created by the awesome folks at Google, we can use all these features in modern browsers today. Polymer provides a set of polyfills that enables us to use web components in non-compliant browsers with an easy-to-use framework. Polymer does this by:

- Allowing us to create Custom Elements with user-defined naming schemes. These custom elements can then be distributed across the network and used by others with HTML Imports.
- Allowing each custom element to have its own template accompanied by styles and behavior required to use that element.
- Providing a suite of ready-made UI and non-UI elements to use and extend in your project.


