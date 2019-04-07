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

I was born into a family of engineers: my mom was a programming team lead and my dad worked in avionics and engineering. Tech was a presence in my life since early childhood: I grew up reading books about C and Assembly, graphics algorithms and computer internals, scavenged for bootleg CDs on flea markets and coded websites for my friends in high school. My first "computer job" was automating DevOps (before DevOps was a thing) and since then I have slowly climbed the web stack from the back-end to front-end, ending up with me founding a boutique dev shop focusing purely on React-based UI development.

Some of my more recent write-ups and research work follow.

Ubiquitous UI/UX:

* [Wrapping Facebook Messenger API in a stream interface](/wrapping-facebook-messenger-stream-api)
    * [facebook-messenger-streams: Facebook Messenger API Stream Wrapper](https://github.com/myplanet/facebook-messenger-streams)
* The new wave of attention paid to chat-based interfaces points to some possible new massive shifts in "casual app" interaction
    * [My notes on initial development setup for Facebook Messenger bots](/facebook-bot-setup)

UI architecture work:

* Modeling UX affordances as a backbone concept for a ubiquitous UI component library
    * [react-dynamics: integrating Promises into React](https://github.com/beamworks/react-dynamics)
    * [react-collectable: flexible form validation with uncontrolled input components](https://github.com/beamworks/react-collectable)
* [UI Rendering: Change Detection Without Observables](/ui-repaint)
    * [vdom-live: minimalist virtual DOM render loop with no observables](https://github.com/unframework/vdom-live)
    * [html2hyperscript: Convert legacy HTML to Hyperscript](https://github.com/unframework/html2hyperscript) (quick helper utility for virtual-dom)
* [Experimenting with RPC for UI/Backend Communication](https://medium.com/@unframework/experimenting-with-rpc-for-ui-backend-communication-8b6e214a7f7f#.oqw1js3u0)
    * [remote-control: Call functions on node server from browser web UI for quick prototype wire-up](https://github.com/unframework/remote-control)
* [MVC and Modeling User Attention Span](/view-attention-span)
* [Modeling user focus](/user-focus-model)
    * [Atomic Routes: decentralized nested client-side routing with Promises](https://github.com/unframework/atomic-routes)
* [HTML/CSS Encapsulation At Runtime](/html-css-encapsulation-at-runtime)
    * [Airtight CSS Lint: enforcing encapsulation using BEM-like syntax](https://github.com/unframework/airtight-css-lint)
* [Angular UX Tips](http://ng-ux.tips)
* [Creating a simple recipe to publish compiled Browserify projects to GitHub Pages using TravisCI](/browserify-github-pages-quickstart)
    * Repo with the resulting [Browserify to GitHub Pages quickstart doc](https://github.com/unframework/browserify-github-pages)

Database persistence and ORM work:

* [Fxrm Store: DDD-inspired alternate ORM library](https://github.com/fxrm/fxrm-store)
* [Enterprise Apps: ORM vs Key-Value Storage Model](/orm-vs-key-value)
    * [Somewhat discouraging responses on Reddit :)](https://www.reddit.com/r/programming/comments/2t36ra/disappointed_in_orm_keyvalue_store_might_be_a/)

Workflow and team operations:

* I am really interested in Git as representing both a snapshot state store and a malleable chain of worksets: it seems useful beyond coding, especially when bridging with non-tech workflows
    * [git-inbox: Slack bot to convert uploads into Git commits/PRs](https://github.com/unframework/git-inbox)
    * [S3 Password Agent: password-protect Amazon AWS S3 download links for static sites like Jekyll / GitHub Pages](https://github.com/unframework/s3-password-agent)

Exploration of mobile product UX and packaging:

* [Shift Pod: Nurses](https://play.google.com/store/apps/details?id=com.unframework.nursingshifttracker) (Android home screen widget for nurse shifts)

Misc hacks:

* [ChartGL](https://chartgl.zone): quick fun experiment with 3D bar and pie charts using React + WebGL + CSS 3D
* [JS1k entry: Magic Hat](http://js1k.com/2017-magic/demo/2827) (JS animation demo in less than 1024 bytes)
* [WebAudio music toy](/webaudio-music-toy): [live demo](http://unframework.github.io/eltrn/), [demo video](https://www.youtube.com/watch?v=uZM0nfuLfxM) and [source code](https://github.com/unframework/eltrn)
* [Motepad: rich text editor rendered in pure JS and DOM](https://github.com/unframework/motepad)
* [Cathode Green: side-scrolling bike physics platformer game in browser](https://github.com/unframework/cathode-green)
* [Minimal Socket.IO replacement layer for high-performance sites](https://github.com/unframework/fusio) (open-sourced from a defunct commercial project)
