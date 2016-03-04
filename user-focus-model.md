---
layout: page
title: 'Modeling User Focus'
date: 2015-01-18
---

([original gist](https://gist.github.com/unframework/d3e045d76c4390813ad5))

Focus is simply a pinpoint of interest, that then can be queried at render time.
We shouldn't get caught up in thinking that it's a fixed enum thing;
instead, each focus point is a simple boolean: is it on or is it off?
Tab rendering is a particular application where one might multiplex the UI,
and only one choice of several is selected - that 'radio' behaviour is
another interesting thing.

If we go with habit and assume an hierarchy, what are the implications?
Radio behaviour means that only one point in the hierarchy is focused at any point.
But that may not be enough to represent things - multiple tab panels, etc.

Let's consider the parent-child relationship. It is the attention span time scope.
If parent is not focused, child is not focused.

So. If a focus scope exists, it is needed by the user. And hence all its children exist.

Some focus scopes can then exhibit radio-button state behaviours. They encompass
that state. The states might be un-bounded (but countable), and there might
be an underlying model, such as the route system.

Changing radio-button state with e.g. route system underneath would mean sending off
a request, and then listening for underlying state change.

Each state fundamentally encapsulates a promise - of scope being finished. Instead of
'onDestroyed' type of event, it is a 'whenDestroyed' promise.

Radio-button behaviour is actually representable by an arbitrary state variable and then
listening to a specific value of that variable.

```coffee
Promise = require 'bluebird'

class FocusRoot
    constructor: () ->
        @whenDestroyed = new Promise

class FocusState
    constructor: (parent) ->
        @_state = undefined

    when: (referenceValue, cb) ->
        onChange = () ->
            if @_state

        onChange()

        {
            remove: () ->
                $(this).off 'changed', onChange
        }
```
