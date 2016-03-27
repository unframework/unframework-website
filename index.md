---
layout: front
title: Personal website of Nick Matantsev
---

I am a product technical lead at [Myplanet](http://myplanet.com).

My primary research interest is in modelling real-life communication and business workflows and using that to improve human process and automation. In addition, I spend time analyzing software development techniques themselves - founded on a belief that [programming is theory-building](http://www.dc.uba.ar/materias/plp/cursos/material/programmingAsTheoryBuilding).

See my [open source projects on GitHub](https://github.com/unframework), [Twitter profile](https://twitter.com/unframework) and [Medium posts](https://medium.com/@unframework). Plus occasional [presentation upload on my SpeakerDeck page](https://speakerdeck.com/unframework).

Workflow and ops hacks:

* I am really interested in Git as representing both a snapshot state store and a malleable chain of worksets: it seems useful beyond coding, especially when bridging with non-tech workflows
    * [git-inbox: Slack bot to convert uploads into Git commits/PRs](https://github.com/unframework/git-inbox)
    * [S3 Password Agent: password-protect Amazon AWS S3 download links for static sites like Jekyll / GitHub Pages](https://github.com/unframework/s3-password-agent)

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

Database persistence and ORM work:

* [Fxrm Store: DDD-inspired alternate ORM library](https://github.com/fxrm/fxrm-store)
* [Enterprise Apps: ORM vs Key-Value Storage Model](/orm-vs-key-value)
    * [Somewhat discouraging responses on Reddit :)](https://www.reddit.com/r/programming/comments/2t36ra/disappointed_in_orm_keyvalue_store_might_be_a/)

Exploration of mobile product UX and packaging:

* [Shift Pod: Nurses](https://play.google.com/store/apps/details?id=com.unframework.nursingshifttracker) (Android home screen widget for nurse shifts)
