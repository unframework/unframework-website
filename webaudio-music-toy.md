---
layout: page
title: WebAudio Music Toy
date: 2016-05-15
---

Back when I was around 9, my brother brought home a drum machine. He would pretty often procure neat gadgets to play with, and this was definitely a memorable one. As I recall, it had a standard 16 step pattern program, and the usual set of drum samples that these things come with. Music hardware is always a bit obtuse to figure out (intentionally?), so it was a really fun puzzle to understand how to use that thing.

Me being a 9-(or so)-year-old with no musical training, this was also my first insight into how e.g. a typical beat works. It's not so intuitive! Biggest example is learning the fact that hi-hat notes just keep repeating thoughout a measure - something not very apparent because half the hits get swallowed up by snare and kick drum.

Of course, I eventually got bored and moved on: after figuring out the basics I couldn't get anywhere actually decent anyway. Later on, when I picked up drums, those visual examples really helped! I just played the patterns that I remembered, but with actual sticks and drums.

Electronic music widgets are still a bit of a mystery to me. I did play with basic MIDI in early teens and FruityLoops synths a bit later; however, without formal musical training, I would always hit a wall of incompetence and quickly lose interest. But it was good to understand the basics of oscillators, note structure and sequencing. It's just the "making it sound good" part that I never got right.

A few years ago, I grabbed a copy of the Korg iElectribe app for my iPad. It emulates the physical Electribe synth box, in pass-time-on-the-toilet format. It's actually pretty good (for my not-actually-making-music needs). Same step pattern setup, decent choice of synth waveforms, drum samples and effects. Fun to play with, and comes with a ton of informative presets.

And more recently, I have been listening to some interesting hip-hop instrumental producers, made popular by vloggers like Casey Neistat. I think a big part of the enjoyment for me is due to that prior exposure to music-making tools - it is relatable, but also actually sounds good (unlike my prior tinkering).

So all of this background exposure finally got me building a music toy of my own.

One day last week, I was in the middle of a multi-hour coding streak and listening to one of these folks ([Jeff Kaale](https://soundcloud.com/jeff-kaale) maybe?). In the back of my mind, I couldn't help but try and imagine the tools that might be used for the kind of intricate sampling that's involved. And I just visualized one of those 2D LCD grid controller things that modern producers seem to use, with one axis being the pattern timeline and the other being the source sample slice selector. I am 100% sure that's a real kind of sampler interface that already exists, but in that moment I just wanted to try to implement it regardless, just to see if it is usable.

I got home and re-opened an old hack project that I started in order to explore the WebAudio API. In-browser audio is actually a really neat kind of platform. It works much like a classic source/sink audio setup would - kind of how like classic 70s synths would plug into each other with patch cables, forming a processing pipeline. Browsers even support things like reverb and low-pass filter out of the box. Also, it deals with timing really nicely, allowing to schedule a timeline of audio events in advance.

Adding a minimal reactive UI scaffold from my experiments a while back, I whipped up a basic 16x16 grid of buttons. Then I fed the data from button toggle selections into a scheduled sequence of 1/16 sample slices. The X axis defines the step time in the pattern, and the Y axis picks which of the 16 source sample slices to use. A quick search for the [Amen Break sample](http://www.economist.com/blogs/prospero/2011/12/amen-break), and I had a demo going (somehow that phrase reminds me of [this](https://www.youtube.com/watch?v=Sr2PlqXw03Y)).

Because all playback was done in 1/16 slices, there were some artifacts in the continuous playback portions (e.g. when scheduling a full consecutive 1/4th slice). I had to add an optimization where several contiguous slices would be merged into one longer "note" play. Also, to emulate the standard loop preview of a pattern sequencer, I had to add a 10ms interval check to detect when the current pattern would finish playing and schedule up the next instance.

This was also a good opportunity to use my Camtasia Studio, finally, and record a demo video. Almost a year ago I installed Camtasia because I was hoping to record some coding tutorials. That went nowhere, but then this February I still decided to shell out for a full license (I believe in just buying a decent tool instead of spending time researching free hacks/pirating). Cost a couple hundred bucks, so I hope I make more than just that one video!

And here is the resulting [demo clip of me playing with the sampler](https://www.youtube.com/watch?v=uZM0nfuLfxM). The [source code](https://github.com/unframework/eltrn) is available on GitHub.

I have done some more work on top of that, actually, converting the UI to be WebGL-based (drawing from another set of building blocks in my work folder), and supporting pitch changes and reverse-play, but that needs a separate write-up.
