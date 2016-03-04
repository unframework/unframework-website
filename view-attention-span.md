---
layout: page
title: 'MVC and Modeling User Attention Span'
date: 2015-01-14
---

([original gist](https://gist.github.com/unframework/5a3973d473bc1e9db492))

A lot of user-facing app architecture can be simplified down to two main categories of code - **model** and **presentation**. Or *M* and *VC* of MVC (or *MC* and *V*, depending on one's interpretation of that venerable acronym).

Which code is considered which? I think the philosophical difference is that model is state that persists even when user is not directly interacting or watching it (non-visually as well, of course), and presentation is specifically tied to user attention span. That's a very vague definition, but it's food for some thought.

The pattern that typically ends up making sense is to of course make the model agnostic to how it is being rendered. User input mostly is "fed" into the model via direct imperative method calls. Resulting view of the model is given read-access to model state, to "pull" data out on demand.

But when to "pull" new data when the model changes?

Let's pretend that we are rendering a web UI and have the horsepower to just brute force the re-rendering of the entire view at 60fps (like many videogames can). We wouldn't need to worry about detecting changes to the model - the screen constantly refreshes at near-zero lag. The presentation code would be very simple.

```js
// if only this was realistic...
setInterval(function () {
  // naively render the entire UI in its glory
}, 16); // 1000ms / 60fps
```

Simple vanilla code would have the model send some events to notify of changes. It's technically keeping the model decoupled from presentation, but of course model code has to be peppered with event triggers - in the right spots, no less. Still not ideal.

```js
// don't need no frameworks when you got jQuery?
var model = {
  counter: 1,
  poke: function () { this.counter += 1; $(this).trigger('poked'); }
};

function View(model) {
  $dom = $('.... whatever ....').text(model.counter);
  $(model).on('poked', function () {
    $dom.text(model.counter);
  });
  // ...plus some sort of destructor to avoid event listener leaks, etc, etc
}
```

One of the middle-ground solutions is a digest cycle like in AngularJS. Every view declares what parts of the model it is rendering (via `$scope.$watch(...)`), and then there is a brute-force "redraw" of those watch-expressions every time something interesting happens (input event, wrapped network operation or timeout, etc). The hierarchy of "scope" objects helps clean up watch-expressions when parts of the view become obsolete.

So what is a "scope" then? Why are they hierarchical (separately from DOM tree)? [AngularJS docs](https://docs.angularjs.org/guide/scope) are, in my opinion, kind of skirting the philosophy of these questions. Questions like that may be rhetorical, but they get heavier over time and line-count; plus learning curve is not helped when there is no simple human equivalent to a framework concept.

Comparing the brute-force rendering approach with model-events-as-change-detection as extremes (and the middle-ground solutions) highlights one common concern that views have to deal with - **user attention span**.

When something is on screen and other data consumption devices, it is implied to be *relevant*. It is a representation that is expected to be reasonably up-to-date with the underlying app state. The user will likely act based on that represented information, so it better not be stale/wrong. When the representation is no longer on screen or non-visual prompt focus, it has no need to keep refreshing and staying up-to-date.

And so the AngularJS idea of "scope" actually directly maps to the concept of user attention span. It is the scope of relevance to the user. While a view is, well, in view - its scope object is alive and firing digest cycles. When it has been discarded (the user's attention moved on to other things), the scope object is unhooked from further notifications and left to be garbage-collected. Hierarchy means that if a user is done with a parent scope of attention, all the child scopes are also no longer relevant. Which maps cleanly to implementations of aggregate views delegating portions of display to sub-views.

In some ways, it's not a DOM or viewport area scope, but a timeline scope.

But I wonder what can be achieved if we went further in explicitly modeling that attention span. Maybe tie it somehow to visual relevance of view state for better performance. Or reduce impedance mismatch in architecture of non-visual UIs. @todo consider that :)