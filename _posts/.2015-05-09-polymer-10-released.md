---
layout: post
title: Polymer 1.0 released
---

## What is polymer?

**Polymer** is a library that helps you build elements and apps out of web components. [Web Components](http://webcomponents.org/) are a cutting edge set of new standards that allow developers to extend the HTML vocabulary with their own custom elements. Because Web Components are designed to be a new primitive for the browser, it means that they’re very powerful but also very low level and working with them requires a fair bit of code. **Polymer** makes it easier to work Web Components by “sugaring” the syntax. It reduces the amount of boilerplate code you need to write, and adds a declarative style so creating Web Components is as easy as writing HTML.

Initially this project started as an experiment, with making and clubbing all the polyfills to bring the functionality of webcomponents to all browsers. Which in sometime became a library full of great features like data binding, attribute change watchers, automatic node finding, etc. But along with this there were many performance heads and had developer concerns like theming, complexity.

Since the 0.5 **“Developer Preview”** release, it has been re-written from the ground up, focusing on cross-browser performance while keeping the developer-friendly ergonomics.

**Polymer 1.0** has been rebuilt from the ground up for speed and efficiency. The new, leaner core library makes it easier than ever to make fast, beautiful, and interoperable web components. The new library is:

- 3x faster on Chrome,
- 4x faster on Safari, and
- 36% less code than in developer preview.

And it’s ready to be used in production applications. The news was announced via a blog post by **Taylor Savage, Product Manager, Polymer**.

In the news, Taylor wrote:

> “Today we released the 1.0 version of the Polymer library. Polymer is a new way of thinking about building web applications - a sugaring layer on top of Web Components, making it easy for you to create interoperable custom elements. These elements can then be put together to create app-like immersive experiences on the web.”

### Product Lines
In addition to the library, there is new “product lines” of elements, all updated to work with the 1.0 release of the library. The element product lines built by the **Polymer** team include:

- **paper-elements** - the reference implementation for material design on the web
- **iron-elements** - the core building blocks useful for any web application
- **google-web-components** - elements that wrap a multitude of Google services, making it easy to leverage maps, drive, signin, translate, and many more in your app with a single element.
- **platinum-elements** - add push notifications or offline caching to your app with a single element. The platinum product line wraps the new re-engagement API’s like service worker as easy-to-use elements.
- **gold-elements** - checkout flows are hard on the web, especially on mobile. The gold-elements make checkout easy with auto-validating elements for credit card fields, phone number fields, and more.


### The new library

Major new and updated features since the 0.5 “Developer Preview” release include:

- Brand-new, fast, and easy-to-use data binding system
- Element theming and styling using custom CSS properties - no more messy /deep/ and ::shadow
- Fast and lightweight shadow DOM shim named shady DOM, for non-supporting browsers
- “Behaviors” mechanism for sharing behavior between elements
- It’s easier than ever to create high-quality, production-ready elements using **Polymer**, to use in your app or share with other developers.


### Polymer Starter Kit

There is also a [Polymer Starter Kit](https://github.com/polymerelements/polymer-starter-kit) with ready-to-use boilerplate, and an end-to-end toolchain to use from development through production deployment.

### Resources

If you haven't used **Polymer** before, it's time to try it out. If you haven't tried it recently, time to take another look. There are lot of resources already there on [Polymer Project page](https://www.polymer-project.org/1.0/).

Here is a series of podcasts by **Rob Dodson** to learn about polymer - [Polycasts](https://www.youtube.com/watch?list=PLOU2XLYxmsII5c3Mgw6fNYCzaWrsM3sMN&v=omASiF85JzI).

If you have already worked on polymer and you need to migrate your work to 1.0 [here](http://chuckh.github.io/road-to-polymer/convert-code.html) is a tool for you, also there is a [Polymer Migration Guide](https://www.polymer-project.org/1.0/docs/migration.html).
