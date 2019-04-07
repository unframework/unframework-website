---
layout: front
title: Personal website of Nick Matantsev
---

I read books and work with software.

My primary interests are in domain modeling, analysis and automation. In addition, I follow topics such as generative art, HCI/UX, developer tooling and hobby electronics. A lot of my work is based on the idea that [programming is theory-building](http://www.dc.uba.ar/materias/plp/cursos/material/programmingAsTheoryBuilding) and is inspired by [domain-driven design](https://en.wikipedia.org/wiki/Domain-driven_design), CQRS, functional programming, etc.

I am currently a lead front-end developer with [Beamworks](https://beamworks.io), a small React agency.

Some links:

- [GitHub projects](https://github.com/unframework)
- [CodePen demos](http://codepen.io/unframework/)
- [Twitter profile](https://twitter.com/unframework)
- [Medium profile](https://medium.com/@unframework)
- [SpeakerDeck page](https://speakerdeck.com/unframework)
- [Flickr photos](https://www.flickr.com/photos/nickmatantsev/)

## A bit more about me

I was born into a family of engineers: my mom was a programming team lead and my dad worked in avionics and engineering. Tech was a presence in my life since early childhood: I grew up reading books about C and Assembly, graphics algorithms and computer internals, scavenged for bootleg CDs on flea markets and coded websites for my friends in high school. My first "computer job" was automating DevOps (before DevOps was a thing) and since then I have slowly climbed the web stack from the back-end to front-end, ending up with me founding a boutique dev shop focusing purely on React-based UI development.

## Misc fun hacks and demos

* CodePen demos
    * https://codepen.io/unframework/pen/pqorjJ - Matrix screensaver with analog CRT effect in WebGL
    * https://codepen.io/unframework/pen/XyayoM - quick 3D bar and pie charts using React + WebGL + CSS 3D
    * https://codepen.io/unframework/pen/OrOMBg - stylized animated flag in the wind
    * https://codepen.io/unframework/pen/LbaLvG - pure-CSS flip-clock animation
* [Midnight Tactix 3000](https://twitter.com/atesgoral/status/993972666540417024) (fun tribute to Outrun/ChaseHQ built as a game jam entry with my friend)
* [TinTTY terminal emulator](https://hackaday.io/project/27359-tiny-wearable-8-bit-vt100-console) (Arduino-based VT100 emulator for a 1in screen)
* [JS1k entry: Magic Hat](http://js1k.com/2017-magic/demo/2827) (JS animation demo in less than 1024 bytes)
* [WebAudio music toy](/webaudio-music-toy): [live demo](http://unframework.github.io/eltrn/), [demo video](https://www.youtube.com/watch?v=uZM0nfuLfxM) and [source code](https://github.com/unframework/eltrn)
* [WebAudio DTMF detection](https://github.com/unframework/dtmf-detect): [live demo](https://unframework.github.io/dtmf-detect/)
* [Office Space](https://github.com/unframework/office-space) (simple experiment with game crowd AI and WebGL): [live demo](https://unframework.github.io/office-space/)
* [Shift Pod: Nurses (2015)](https://play.google.com/store/apps/details?id=com.unframework.nursingshifttracker) (Android home screen widget for nurse shifts)
* [Cathode Green: side-scrolling bike physics platformer game in browser (2014)](https://github.com/unframework/cathode-green)
* [Motepad: rich text editor rendered in pure JS and DOM (2013)](https://github.com/unframework/motepad)
* [Minimal Socket.IO replacement layer for high-performance sites (2013)](https://github.com/unframework/fusio) (open-sourced from a defunct commercial project)

## UI architecture work, sketches and write-ups

Note: a lot of this predates popular use of React, GraphQL and other modern tooling.

* Modeling UX affordances as a backbone concept for a ubiquitous UI component library
    * [react-dynamics: integrating Promises into React](https://github.com/beamworks/react-dynamics)
    * [react-collectable: flexible form validation with uncontrolled input components](https://github.com/beamworks/react-collectable)
* sketch: [UI Rendering: Change Detection Without Observables](/ui-repaint)
    * [vdom-live: minimalist virtual DOM render loop with no observables](https://github.com/unframework/vdom-live)
    * [html2hyperscript: Convert legacy HTML to Hyperscript](https://github.com/unframework/html2hyperscript) (quick helper utility for virtual-dom)
    * [vdom-stache](https://github.com/unframework/vdom-stache) (experiment in using vanilla Mustache to drive a React-style render cycle)
* [Experimenting with RPC for UI/Backend Communication](https://medium.com/@unframework/experimenting-with-rpc-for-ui-backend-communication-8b6e214a7f7f#.oqw1js3u0)
    * [remote-control: Call functions on node server from browser web UI for quick prototype wire-up (2015)](https://github.com/unframework/remote-control)
* misc sketches on applying domain-driven design to UI
    * [MVC and Modeling User Attention Span](/view-attention-span)
    * [Modeling user focus](/user-focus-model)
* [Atomic Routes: decentralized nested client-side routing with Promises (2015)](https://github.com/unframework/atomic-routes)
* [HTML/CSS Encapsulation At Runtime (2015)](/html-css-encapsulation-at-runtime)
    * [Airtight CSS Lint: enforcing encapsulation using BEM-like syntax](https://github.com/unframework/airtight-css-lint)
* [Angular UX Tips (2015)](http://ng-ux.tips)
* [Wrapping Facebook Messenger API in a stream interface (2016)](/wrapping-facebook-messenger-stream-api)
    * [facebook-messenger-streams: Facebook Messenger API Stream Wrapper](https://github.com/myplanet/facebook-messenger-streams)
    * [My notes on initial development setup for Facebook Messenger bots](/facebook-bot-setup)

## Database persistence and ORM work

* [Fxrm Store: DDD-inspired alternate ORM library (2015)](https://github.com/fxrm/fxrm-store)
* sketch: [Enterprise Apps: ORM vs Key-Value Storage Model](/orm-vs-key-value)
    * [somewhat discouraging responses on Reddit :)](https://www.reddit.com/r/programming/comments/2t36ra/disappointed_in_orm_keyvalue_store_might_be_a/)

## Workflow-related projects

* opening up Git to non-technical contributors
    * [git-inbox: Slack bot to convert uploads into Git commits/PRs](https://github.com/unframework/git-inbox)
    * [S3 Password Agent: password-protect Amazon AWS S3 download links for static sites like Jekyll / GitHub Pages](https://github.com/unframework/s3-password-agent)
* [Browserify to GitHub Pages quickstart](https://github.com/unframework/browserify-github-pages)
    * write-up: [Creating a simple recipe to publish compiled Browserify projects to GitHub Pages using TravisCI](/browserify-github-pages-quickstart)
