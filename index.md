---
layout: front
title: Personal website of Nick Matantsev
---

I am a product technical lead at [Myplanet](http://myplanet.com).

My primary research interest is in modelling real-life communication and business workflows and using that to improve human process and automation. That means both back-end topics like data versioning and consistency and front-end matters like HCI/UX. In addition, I spend time analyzing software development techniques themselves - founded on a belief that [programming is theory-building](http://www.dc.uba.ar/materias/plp/cursos/material/programmingAsTheoryBuilding).

See my [open source projects on GitHub](https://github.com/unframework), [Twitter profile](https://twitter.com/unframework) and [Medium posts](https://medium.com/@unframework). Plus occasional [presentation upload on my SpeakerDeck page](https://speakerdeck.com/unframework). I also dabble in pictures: [see my Flickr profile](https://www.flickr.com/photos/nickmatantsev/).

Favourite moments that shaped who I am as a techie:

* coding Bresenham lines for CGA and VGA display using INT10 in Turbo C as a pre-teen
* getting Quake3 level spline patches to load and render using OpenGL in my Verlet-based physics racer experiment (I used them to make a half-pipe)
* fixing a cgi-bin script written in Bash, in 1999
* live-editing MBR and swapping a Linux root partition to use software RAID-1 on a small office server
* getting over impostor syndrome by reading other people's Perl CPAN code
* taking a proper accounting class and secretly loving it (most useful university course ever)
* becoming comfortable with Prolog
* hacking together a simple constructive solid geometry (CSG) triangulation proof of concept (Java, BSP trees)
* eating humble pie by seeing live user tests break my UX assumptions on early freelancing projects
* sending basic graphics direct to a SunRay thin client display (Java, with help from reverse-engineered UDP protocol docs)
* watching live production traffic ramp up on a WebSocket-based chat I helped build for an N-million user social site

Some of my more recent write-ups and research work follow.

Ubiquitous UI/UX:

* The new wave of attention paid to chat-based interfaces points to some possible new massive shifts in "casual app" interaction
    * [My notes on initial development setup for Facebook Messenger bots](/facebook-bot-setup)
    * [Stream-oriented wrapper lib for Facebook Messenger API](https://github.com/myplanet/facebook-messenger-streams)

UI architecture work:

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
* [Auto-publishing Browserify to GitHub Pages](https://github.com/unframework/browserify-github-pages)
    * simple recipe to publish compiled Browserify projects to GitHub Pages using TravisCI

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

* [WebAudio music toy](/webaudio-music-toy): [live demo](http://unframework.github.io/eltrn/), [demo video](https://www.youtube.com/watch?v=uZM0nfuLfxM) and [source code](https://github.com/unframework/eltrn)
* [Motepad: rich text editor rendered in pure JS and DOM](https://github.com/unframework/motepad)
* [Cathode Green: side-scrolling bike physics platformer game in browser](https://github.com/unframework/cathode-green)
* [Minimal Socket.IO replacement layer for high-performance sites](https://github.com/unframework/fusio) (open-sourced from a defunct commercial project)
