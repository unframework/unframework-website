---
layout: page
title: 'Quickstart Setup to Push Browserified Code to GitHub Pages'
date: 2016-12-09
---

This is a write-up about how I arrived at the [Browserify GitHub Pages setup quickstart doc](https://github.com/unframework/browserify-github-pages): some background motivation and ensuing challenges.

I have been using [Browserify](http://browserify.org/) to build a ton of side project hacks. Accessing the vast multitude of npm libraries in the browser is super useful for quickly setting up a prototype; and it is easy to share code back as an open source module.

But I would always hit a snag when trying to deploy the projects online. To run the code locally, I usually just use the [beefy](http://didact.us/beefy/) server (there are many alternatives, too). Online, I could use a Heroku deploy, but of course the free instances take a huge delay to spin up after sleeping, and in general my code would be client-side only, so using a full-stack host seemed like overkill.

Instead, I prefer to host these kinds of projects on GitHub Pages: quick and easy and trusted. To do that, I would manually compile the `index.js` file and push to the `gh-pages` branch for every deploy. It works really nicely, but the manual steps are annoying and error-prone.

Naturally, automating this via a freebie solution like [Travis CI](https://travis-ci.org) starts making sense. Plus, that gives an opportunity to actually run tests for the more advanced projects.

But I also wanted the solution to be repeatable and easy to set up: worrying about CI plumbing is a big context switch, and pushing built artifacts *from* Travis is actually not that easy, given that there have to be publish keys, credentials, etc.

I ended up creating a quick and compact reusable `.travis.yml` file that simply hooks into the `after_success` Travis event and does the following:

- compile the `index.js` entry point in place using Browserify
- add a baseline `index.html` if not already present
- commit the two files inside existing Travis repo clone
- force-push the commit to the `gh-pages` branch of the origin repo

Instead of standard SSH authentication, I decided to use the GitHub personal token auth over HTTPS: it is very easy to generate and put into Travis settings as an encrypted parameter. Getting git to work with that was tricky; I used the `GIT_ASKPASS` mechanism to pipe the token into the git credential helper from an auto-generated dummy script (see [.travis.yml source](https://github.com/unframework/browserify-github-pages/blob/master/.travis.yml) for details).

For every new Browserify-based project that I want to set up to auto-deploy to GitHub Pages, I simply:

- create GitHub personal token
- enable Travis on the repo
- put the GitHub personal token into encrypted Travis variable
- copy-paste the `.travis.yml`, no changes needed
- commit, push and watch things deploy

This works for browser-only projects, of course: I have used it for e.g. WebGL hacks, virtual DOM experiments, WebAudio toys, etc.

General quickstart instructions and the drop-in `.travis.yml` file are published here in a dedicated [unframework/browserify-github-pages repo](https://github.com/unframework/browserify-github-pages). Happy auto-deploying!
