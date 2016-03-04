---
layout: page
title: HTML/CSS Encapsulation At Runtime
date: 2015-01-13
---

([original gist](https://gist.github.com/unframework/51dcee7e33912268a347))

Web-based UIs are hard to componentize into encapsulated widgets. DOM + CSS and the browser runtime have their roots in a document-based, progressive-rendering mentality, and that creates friction when attempting to develop components that don't step on each others' feet.

My ultimate starting point when dealing with encapsulation in-browser is to **consider the runtime state produced by the combination of JS, DOM API and CSS behaviour**.

In purest form, there are just JS objects that exist in memory of the browser and interact with each other via vanilla method calls and data access. The surface of encapsulation of a pure-Javascript component is just its public methods and properties.

When it comes to displaying things on screen, part of the widget component contract becomes rendering something visible in the browser viewport. Of course, we typically use DOM and CSS to do that (although Canvas-driven app UIs do exist). It makes sense to look at DOM and CSS as a sort of a basic rendering and input API that forms a foundation for a higher level of code abstraction. Thus, a widget simply creates DOM elements, attaches styles and manages the element lifecycle, hiding these implementation details from the rest of application code.

But DOM elements as screen-drawing primitives come with a lot of baggage. A DOM element belongs to the page hierarchy, is sized and positioned by page layout rules (margins, floating, position), participates in event logic, inherits CSS properties, etc. All of that is extra surface added to the owning component, and it creates unwanted interactions between unrelated pieces of code.

Example scenario: a `div` in a container widget has a font property that leaks into a `span` element that was created by a child widget. The child `span` DOM element inherits font properties by default, and that is a piece of behaviour that breaks encapsulation of the child widget component as an aggregate whole. The answer might be to force any inherited properties of the `span` to have some specific values. Another option is to have a convention to not set font properties on anything but "leaf" elements in the rendered DOM hierarchy. Web Components API helps tremendously as well in this case. But there are other ways DOM elements interact in unwanted ways.

Some interdependencies to consider:

- inline flow vs block flow for layout
- margin collapse rules
- absolute positioning origin
- `z-index` and display order
- width calculation
- inherited CSS properties
- event propagation and bubbling
- focus tab-order
- (@todo add more)
