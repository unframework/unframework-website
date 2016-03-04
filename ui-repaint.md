---
layout: page
title: 'UI Rendering: Change Detection Without Observables'
date: 2015-02-07
---

([original gist](https://gist.github.com/unframework/abe6a6b7bd8c25831bb5))

Reading an HN thread on view frameworks (one of many such threads), I was reminded of [my own past musings](/view-attention-span) with sample code of an extremely idealized UI rendering loop:

```js
// if only this was realistic...
setInterval(function () {
  // naively render the entire UI in its glory
}, 16); // 1000ms / 60fps
```

But actually, here's a real CoffeeScript snippet from a toy side project where I played with the [virtual-dom](https://github.com/Matt-Esch/virtual-dom) library (forgive the superfluous jQuery usage):

```coffee
# tree = current virtual DOM tree
# rootNode = reference to real container browser DOM node

redrawId = null
requestRedraw = ->
    # debounce redraw requests
    if redrawId is null
        redrawId = requestAnimationFrame ->
            redrawId = null

            # paint entire UI as virtual DOM
            newTree = renderMainView()

            # patch current real DOM
            rootNode = patch(rootNode, diff(tree, newTree))
            tree = newTree

$(window).on 'hashchange', ->
    requestRedraw()

$(document.body).on 'click', ->
    requestRedraw()

```

The inside of `requestRedraw` is a typical virtual DOM render-via-patch (wrapped in a debounced RAF callback). But unlike AngularJS and React style state dirty-checks, it's invoked simply any time a user interacts with the UI (obviously, this is a toy example as only clicks/hashchanges are handled). And it works, and is blazing-fast.

In other words, we do a full "repaint" (but only via virtual DOM) any time a user *might* have triggered interesting changes. We forego any other state change detection. This gets us almost all the simplicity of 60fps "dumb renders", without the performance overhead.

Real life is not as simple as this, of course, but this is food for thought.
