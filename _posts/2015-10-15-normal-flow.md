---
layout: post
title: Browser DOM's Normal Flow and Positioning
---

Not understanding fundamental layout concepts can have a great impact on your web design and implementation. For instance, depending on the requirements, a modal dialog can be rendered by calculating its size relative to the viewport and positioning it absolutely, or a simpler technique using fixed positioning and margins performs much better, and the likelihood of bugs is decreased because you are doing significantly less DOM manipulation via JavaScript.

The two key concepts for understanding how the browser lays out a page are normal flow and positioning.

### Normal Flow
The browser renders elements by placing them on a page according to what is known as normal flow.

Per the W3C CSS 2.1 specification:
> Boxes in the normal flow belong to a formatting context, which may be block or inline,
> but not both simultaneously. Block-level boxes participate in a block formatting context.
> Inline-level boxes participate in an inline formatting context.


Let’s translate this W3C-speak into something someone other than a browser developer
can understand.

**“Boxes”** refers to the box model, which describes how boxes represent elements. Every element on the page is a box composed of pixels. Boxes have properties such as padding, margins, and borders that, combined with the box content, determine how much space an element will occupy on a page.

- **Block elements** flow vertically and fill their parent container if a width is not set.
- **Inline elements** flow horizontally (side by side) and occupy only as much width as the box context, left and right margins, and padding require.

### Positioning Elements
In the normal flow, an element’s default position value is **static**. A static element is technically not positioned. A **positioned element** is said to have a position value of **relative**, **absolute**, or **fixed**, and it is removed from the normal flow. Positioning does not cascade (i.e., it is not inherited by child elements), so you have to specifically set it on an element. Otherwise, the default value of static will be applied.

####offsetParent
When an element is **positioned**, it is considered to be a **containing element**. A containing element is a **reference point** for **positioning child elements** using the top, right, bottom, and/or left properties. This containing element then becomes the **offsetParent** for its child elements and any ancestors of the children that are not descendants of closer-positioned ancestors.

##### How the browser determines an element’s offsetParent ?
An element’s offsetParent property can be either null, the <body>, or an ancestor element other than the <body>. The browser uses the W3C specification to determine an element’s offsetParent value, as follows:

######offsetParent is null
Occasionally, an element’s offsetParent value will be null. This occurs when the element is the <body>, when the element does not have a layout box (i.e., its display is none) and when the element has not been appended to the DOM. The offsetParent will also be null if the element’s position is fixed because it is
positioned relative to the viewport, not another element. The following example illustrates these cases:

{% highlight html %}
<div id="div1" style="display: none"></div>
<div id="div2" style="position: fixed"></div>
{% endhighlight %}

{% highlight javascript %}
var $body = $('body');
console.log($body.offsetParent()[0]); // logs <html>
console.log($body[0].offsetParent); // logs null
{% endhighlight %}

{% highlight javascript %}
var $div1 = $('#div1');
console.log($div1.offsetParent()[0]); // logs <html>
console.log($div1[0].offsetParent); // logs null
{% endhighlight %}

{% highlight javascript %}
var $div2 = $('#div2');
console.log($div2.offsetParent()[0]); // logs <html>
console.log($div2[0].offsetParent); // logs null
{% endhighlight %}

While the value of offsetParent can be null, the return value from jQuery’s offsetParent method is never null. jQuery returns <html> as the offsetParent, ensuring that there is always an element against which to operate.

######offsetParent is body tag
If the element is not a descendant of a positioned element and it does not meet any of the null criteria, then its offsetParent will be the 'body'.

######offsetParent is an ancestor element other than body tag
If the element is a descendant of a positioned element, then the closest positioned ancestor will be its offsetParent. If an element is not a descendant of a positioned element but is a descendant of \<td\>, \<th\>, or \<table\>, then its offsetParent will be the closest of the aforementioned tags.

## Positioning
Positioning is frequently misunderstood. Often developers will set a different position value on an element in an attempt to fix a layout when things are not looking quite right. While this approach can “fix” a layout, it does not promote an understanding of how positioning actually works. Having a firm grasp of positioning can save you a great deal of time in the long run, because once you understand how it
works you will begin to construct pages in a much more efficient manner.

### Relative positioning
When an element is positioned relatively, the space it would have occupied in the normal flow is reserved. All other elements in the normal flow render around the space as if the element were in the normal flow. Visually, it is placed as if its position value were static. However, unlike with a static element,setting the top, right, bottom, or left values will shift the element accordingly. Positioning an element relatively is typically done to create a containing element for positioning child elements, or to apply a z-index (z-index is not applicable to statically positioned elements). Relative positioning is assigned as follows:

{% highlight css %}
.some-class-selector {
  position: relative;
}
{% endhighlight %}

### Absolute positioning
When an element is positioned absolutely, it is taken out of the normal flow of the document and the space the element would have occupied collapses. The element can then be positioned by setting the top, right, bottom, and left values. Absolute positioning is useful for creating components such as tooltips, overlays,or anything that should be positioned at a precise location outside of the normal flow.

### Fixed positioning
An element is also taken out of the normal flow of the document when its position is fixed. It is positioned relative to the viewport, not the document, so when the page is scrolled the element remains fixed in place as if it were part of the viewport itself.

This is useful for creating sticky headers and footers, and modal overlays. Here’s an example:
{% highlight html %}
/*
Covers the viewport when applied to an element that is a child of the \<body\>. It stretches the element across the \<body\> by fixing its position and setting all the position properties to 0. This makes it impossible to interact with any elements that are in lower rendering layers.
*/

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: #000;
  opacity: .5;
}

/*
Centers an element in the viewport by setting the top and left properties to 50%. It then accounts for the height and width of the element by taking half the height and width, and sets the top and left properties respectively by negating these values.
*/
.modal-content {
  position: fixed;
  top:50%;
  left:50%;
  margin-top: -100px;
  margin-left: -200px;
  width: 400px;
  height: 200px;
  background: #fff;
  padding: 10px;
  overflow: auto;
}
<div class="modal-overlay"></div>
<div class="modal-content">I am the modal content. Fear me.</div>
{% endhighlight %}



### Calculating an Element’s Position
In addition to understanding positioning, it is important to know how to get an element’s position relative to the viewport and the document. This is useful for positioning elements relative to each other when creating components such as tooltips, dialogs, sliders, etc.

#### Relative to the Viewport
Getting an element’s position relative to the viewport alone is typically not that useful. Most of the time you want the element’s position relative to the document, so you can absolutely position another element next to it.

However, the method used to retrieve the position relative to the viewport, element.getBoundingClientRect, returns the top, right, bottom, and left values, which allows you to easily calculate an element’s width and height. This information, in conjunction with an element’s position relative to the document, is useful when creating components that need to align with another element or be constrained by another element’s size, such as drop-downs or tooltips.

Alternatively, you could just use $.outerWidth and $.outerHeight to obtain an element’s dimensions, but element.getBoundingClientRect is significantly faster. Also, **element.getBoundingClientRect** can be used with a couple of other properties to quickly look up an element’s position relative to the document:

{% highlight html %}
<body>
  ...
    <form>
      ...
        <input name="fname" />
      ...
    </form>
  ...
</body>

var $input = $('[name="fname"]');
var rect = $input[0].getBoundingClientRect();
{% endhighlight %}

#### Relative to the Document
Getting an element’s position relative to the document is useful for absolutely positioning an element so that it remains positioned as the page scrolls, and for positioning elements relative to each other within the document. It is a fairly straightforward process. You traverse the DOM, finding each offsetParent, and get its offsetLeft and offsetTop. These values are the offset from the next offsetParent, so you have to sum the values until you reach the \<body\>:

{% highlight js%}
function getElOffsets(el) {
  var offsets = {
    left: el.offsetLeft || 0,
    top: el.offsetTop || 0
  };

  // loop through ancestors while ancestor is an offsetParent
  while (el = el.offsetParent) {
    // sum the offset values
    offsets.left += el.offsetLeft || 0;
    offsets.top += el.offsetTop || 0;
  }
  return offsets;
}
{% endhighlight %}

A quick Internet search for “JavaScript get element position relative to the body” will result in numerous examples that are roughly the same as the one outlined here. However, there is a much better way of doing this in conjunction with element.getBoundingClientRect, courtesy of jQuery:

{% highlight js %}
// https://github.com/jquery/jquery/blob/master/src/offset.js#L105
// box is the el.getBoundingClientRect()
// win is the window object
// docElem is <html> (see
// https://developer.mozilla.org/en-US/docs/Web/API/document.documentElement)
//
// calculating left and top return values
// 1. get the distance of top or bottom from the viewport
// 2. get the distance between the viewport top or left from the top of the page
// & add it to the value from distance of top or bottom from the viewport
// 3. subtract any top or left offsets of <html>, e.g., margins
offset: function( options ) {
  ...
  return {
    top: box.top + win.pageYOffset - docElem.clientTop,
    left: box.left + win.pageXOffset - docElem.clientLeft
  };
}
{% endhighlight %}

I recommend just using $.offset as it performs consistently across browsers, and jQuery has been well tested and vetted by a very large user community. $.offset is an excellent example of the benefits of using a DOM manipulation library: you get the collective intelligence of a community wrapped up in a nice API.
