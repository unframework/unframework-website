---
layout: page
title: Facebook Bot Setup
date: 2016-05-05
---

Bots are cool, I guess?

F8 rolled around and Messenger Bots were announced. Time to hack on new APIs. Actually, the more interesting bit is discovering a new kind of interaction pattern. Blah, blah, usual hype too, of course, but still several reasons to like the direction where things are going with the bot APIs. And, of course, WeChat has had this for a while, and LINE allows direct programmatic bot access too - some real market examples of this working. Trend noise is happening, and as usual a portion of it is just noise; but some of the substance is awesome and is here to stay.

I belong in the grumpy techie camp, and all the conversational/NLP/magical-Jarvis-AI elements of the chat-bot trend are just not connecting with me, intuitively. NLP is really awesome and hard to do: I actually tried out the Stanford NLP SDK package a few years ago and was amazed at the kind of annotated output I could get out of the box. Really cool tech. Something is already coming out of it, but just not in the consumer app UX area yet. People don't like uncertainty, and magical AI is uncertain. Do I have to be polite to it? Will people think I am a jerk if I am not? (I know I would!) It's just iffy UX.

Plus, in the current geo-economic climate it is often still more cost-effective to outsource the conversation layer to humans - and might as well share the dollars outside of the golden billion (maybe I am biased, since it's sort of where I come from). There are a couple pizza ordering example AI apps out there: I saw a good comment online describing how a typical Domino's will have people working the phone while they are idle already, so there are no real savings from automatic parsing in such cases. Of course, the conversation layer may not be needed, to begin with.

But the basic send/receive API is great, and with the extra postback interaction features + marketing push it may create ground for lots of tiny ubiquitous UX interactions, like SMS apps did way back (and which Twilio continues to rock with). A huge piece of value is the fact that Messenger contact ID is trusted, which skips a possible need for login (OAuth popups suck). As the [incisive Dan Grover article](http://dangrover.com/blog/2016/04/20/bots-wont-replace-apps.html) said, identity + eventual payment info is an enormous piece of meta-information to mix into the UX.

Who knows. At least it's an excuse to hack on things with a yet another new API.

Anyways, the core Facebook Messenger Send/Receive API is pretty trivial to get going with.

Some of the setup has nothing to do with tech, but just Social-Media-101. Like setting up FB pages.

FB pages are the Messenger contacts that are the bot "identity". Then there is the concept of the FB app: an actual bridge to specific custom code. One app ID seems to be able to service many different page identities - so it works just like any other page plugin. Theoretically, a SaaS-y kind of offering could just have many page admins signing up to it and then provide multi-tenant service.

So the steps I went through were:

- run my basic FB bot scaffold locally
    - simply exposes an HTTP endpoint for FB web hooks
- run [ngrok](https://ngrok.com/) to expose local server as external URL
    - HTTPS of course!
- create the FB app entry
    - skip the platform selection wizard, just start with simplest possible app ID
    - use the handy Messenger tab to set up web hook endpoint
    - FB bot scaffold should be running: it will need to respond to FB's initial subscription request
- create the FB page
    - create the page, skip wizard steps, and immediately hit the modesty checkbox (Settings / Unpublish)
    - go to the FB app's Messenger tab and generate page token that connects app to this new page
    - run that [Curl command from the FB docs](https://developers.facebook.com/docs/messenger-platform/quickstart) to authorize the page token
    - now the app has permission to listen on page messages and send messages on page's behalf

The official Messenger tutorial was a bit rough and definitely does not inspire good JS coding practices. But it was enough to get going. One thing that puzzled me is that I had to retry the Curl command a couple times because it did not seem to authorize the message send on first attempt.

A bit about the FB webhook setup:

- simple Express router, attached under a route like `/webhook`
- responds to basic webhook `subscribe` verification requests
- processes webhook POST requests, which are always a mixed payload
- important caveat: must verify the `X-Hub-Signature` header!
    - because otherwise people can spoof incoming requests, and that's bad
    - huge value is the trust in the sender contact identity, so this is crucial
- actual logic is separate from webhook machinery, just gets a callback to a different part of app code
- yes, I know there are a ton of existing npm modules that also do webhooks, I just followed the FB tutorial from scratch
    - I don't trust 95% of third-party modules, plus it's fun to reinvent the wheel!

Another weird confusing behaviour: FB infrastructure does not send the `X-Hub-Signature` header with the first few webhook requests. So the proper code setup cannot safely validate FB as the originator! Luckily, it seems to just start sending it after 10-15 minutes, maybe a strange timeout?

Sending messages back to the user is just an HTTP request to the Graph API. Not related at all to the webhook infrastructure, and uses page token to authenticate. There is a limitation on unsolicited messages: I think they need to be sent within a limited time window of a user's last outreach to the bot.

The cool feature that Facebook offers in that regard is the "Send to Messenger" button: it is a widget that a user can activate from a website/elsewhere that opens up that door for the bot to reach out first, without being denied as possible unsolicited spam. This is how apps can e.g. send a receipt via Messenger or any other activity that does not have the user messaging first. I did not actually try it, but it sounds very promising.

When testing with FB users other than oneself, they need to be added as testers so that they can see the development-mode artifacts. Both the FB page and the FB app each have their own tester lists to modify for this. FB pages have an "Analyst" role that is fairly low-impact but still can see the page in unpublished mode. So that is the first spot to add people to. Second spot is the FB app: test users can be added under the "Roles" section.

So, the basic hello-world bot setup is just that. I am skipping the boring boilerplate about running this stuff on Heroku, etc.

The *really* interesting findings so far were, of course, beyond the simple bot scaffolding setup: solving for actual real world chat-based UX and watching some initial non-techie users interact with my quick hacks thus far. Which deserves a separate write-up.
