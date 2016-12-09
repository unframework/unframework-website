---
layout: page
title: 'Wrapping Facebook Messenger API in Node.js Streams'
date: 2016-12-09
---

I have been hacking on the [Facebook Messenger API](https://developers.facebook.com/docs/messenger-platform) for a while now, building tiny bot concepts, prototypes, etc, on top of it. My platform of choice for this has been Node.js, but instead of using one of the several pre-made npm packages that wrap the bot API I have been rolling my own webhook code - to learn the API better, to keep up with its changes and quirks more easily. Messenger platform sends incoming user messages as webhook POST requests, and the bot can respond by submitting a REST payload to the Graph API endpoint: not too complex, and it was definitely worth learning the underlying mechanisms.

But of course there was still always a need to roll up the reusable FB API wrapper code and isolate it in a separate module. At the very least my own new prototypes could then get a quicker start, with code that I already know. Plus, this was also a handy opportunity to practice API design, even if the consumer would still just be me.

So, I started to consider a better way to reinvent this wheel... And after a while, inspiration hit me - why not use a stream abstraction?

The series of Messenger events that is sent to the bot, and the outgoing messages back to the user - those are just like Unix input and output streams! Conceptually, the bot can be visualized as accepting a pipe of incoming messages from Facebook servers, and then directing its output into the pipe going back to the Messenger platform.

I have a soft spot for elegant abstractions, and this seemed like a really fun one to try.

Of course, actually using `stdin` and `stdout` of the bot process would be a bit overkill, and would not be flexible enough. Instead, Node.js already has a [widely adopted stream IO subsystem](https://github.com/substack/stream-handbook) which also happens to support "object mode" streams for arbitrary data - perfect match for a wrapper library interface.

The first piece I implemented was a "master input stream" object. It is a Node.js `Readable` stream, instantiated with the appropriate app secret and webhook verification string, ready to pipe into any application logic code. Behind the scenes, it instantiates a normal Express middleware with appropriate safety checks and POST handling, and then wires it up to emit the `Readable` data events more or less unchanged from the original HTTP JSON form. The app just needs to attach the webhook middleware to its main Express server under the appropriate route path, and it is ready to go:

```js
var fbInputStream = new FBInputStream(
    'mysecrettoken',
    process.env.APP_SECRET
);

fbInputStream.on('data', function (data) {
    var senderId = data.sender.id;

    console.log('got data from user', senderId, data);
});

var app = express();
app.use('/webhook', fbInputStream.webhookRouter);
app.listen(process.env.PORT || 3000);
```

To send back responses, the bot can then instantiate "user output stream" objects. The latter is created per-user, based on the recipient ID and the sender page token. It is a `Writable` stream, so simply writing a plain JS object into it will submit the data as JSON over HTTP back to Facebook inside the user-addressed "envelope":

```js
// when user session starts...

var userOutputStream = new FBUserOutputStream(
    process.env.PAGE_TOKEN,
    recipientId
);

userOutputStream.write({ text: 'Hi there!' });
```

And that's kind of it. I did not add code to parse/construct actual FB data contents: that may really vary per project anyway, and should then just be a separate module too.

Using this stream-oriented abstraction helps organize the code better and makes the bot logic core easier to reason about.

Another useful benefit is that the resulting interface is clean and testable: instead of mocking/stubbing the entire HTTP plumbing infrastructure, it is possible to just create mock streams as test fixtures.

Finally, I just like this abstraction and the Unix-y mindset behind it; so far it seems like a fairly novel approach to this specific API. I am a huge fan of simple and modular building blocks, and hopefully this library can count as an example of those as well!

The resulting code has been published as the [facebook-messenger-streams npm module](https://www.npmjs.com/package/facebook-messenger-streams), with [usage examples and source code available on GitHub](https://github.com/myplanet/facebook-messenger-streams). Take a look at the implementation (it's pretty tiny at around ~50-80 LoC) and leave a star or a comment in the issues section!
