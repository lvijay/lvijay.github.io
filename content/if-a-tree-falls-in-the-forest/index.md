---
title: "If a tree falls in the forest…"
description: "The popular Zen koan goes “If a tree falls in a forest and no one is around to hear it, does it make a sound?” Much ink has been spilt…"
date: "2018-02-25T14:01:55.775Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/if-a-tree-falls-in-the-forest-655e4cbcd5cb
redirect_from:
  - /if-a-tree-falls-in-the-forest-655e4cbcd5cb
---

undefined

Personally, I’m indifferent to the koan’s metaphysical consequences. The Wikipedia page discusses much but I’m an ordinary person with ordinary concerns.

When a Google Chromecast¹ is connected to my TV and the TV is on, the device shows wallpapers that can range from popular museum art to NASA’s photos of the universe. Obviously, the device must download these images thereby using bandwidth. This brings us to the reality based software version of the koan….

#### Iteration 1

If a Chromecast is connected to a TV but nobody’s in the room, does it still consume bandwidth?

**Answer:** yes, of course.

**Reasoning:** neither the TV nor the Chromecast have any means to detect if there exists a watcher in the room; hence the Chromecast would continue to consume bandwidth and display new wallpapers on the TV regardless of whether the room’s occupied.³ (I’d like to imagine that the answer is no but my electricity bill would quickly bring me to reality.⁴ )

The next question then becomes

#### Iteration 2

If a Chromecast is connected to a powered off TV does it still consume bandwidth?

**Answer:** _Maybe_.

**Method:** Switch off the TV, keep the Chromecast on, monitor the logs of the router to which the Chromecast’s connected. If the logs are noisy, the answer is yes; else the answer’s indeterminate — did we observe them long enough? how long is long enough?

If the answer to iteration 2 is _Yes_, we have a slight complication. Over to

#### Iteration 2.1

Can a Chromecast connected to a powered off TV and consuming bandwidth, be modified to not consume bandwidth when the TV is powered off?

That’s a pretty long question so I’ll break it down. We know the answer to iteration 1 is _Yes_. The proper answer to iteration 2 is really only dependent upon what knowledge the Chromecast has about the world. i.e., if the Chromecast has an _in-principle_ way to detect if the TV is powered on then it _could_ be modified to stop consuming bandwidth. If it has no such means then the Chromecast will always consume bandwidth.

(To skip straight to the punchline, go to the §Appendix below.)

Put differently, we don’t need to look at the router logs _beforehand_ to solve the problem; we can just consult the software’s capabilities — the API in techspeak — to see the Chromecast’s capabilities. If the Chromecast does not support such a feature, we don’t need to look at the logs and we already know that the Chromecast necessarily consumes bandwidth; otherwise, it depends on the implementation — perhaps this version of the Chromecast wastes bandwidth but future versions might not.

To put this across more strongly, I would make the case that since we do not know how the Chromecast’s software is implemented we must first look at the Chromecast API before looking at the router logs. For, consider this: maybe the Chromecast downloads (say) a hundred wallpapers early on and won’t actually consume bandwidth until it’s run through all these wallpapers (if each wallpaper is displayed for 12s, it needs to update itself only every 20 minutes). When we don’t know how it’s been implemented we don’t know how much time we’ll spend staring at the logs. Not the best use of our time.

#### Okay, already, what’s the answer?

The Google Chromecast API Reference⁴ documentation says:

> \[Says\] \[w\]hether the application’s HDMI input is in standby or not. If it can not be determined, because the TV does not support CEC commands, for example, the value returned is UNKNOWN.

The good news then, is that if your TV supports this capability your Chromecast will save bandwidth. Otherwise, the Chromecast is helpless.

Now we have a new question. Does my TV support CEC commands? If it does, then my Chromecast does not consume bandwidth; otherwise it does.

### Appendix

Does my Chromecast consume bandwidth when connected to a powered off TV?

**Answer:** I don’t actually care. At this point, I believe the answer is no and I’ve made reasonable steps in that direction. A philosopher’s job is to show that an answer is achievable and how it might be achieved. The rest are mere details.

To borrow a joke from the philosopher Dan Dennett:

> Here’s how a philosopher explains the sawing-the-lady-in-half trick. You know the sawing-the-lady-in-half trick?  
> The philosopher says, “I’m going to explain to you how that’s done. You see, the magician doesn’t really saw the lady in half. He merely makes you think that he does.”  
> And you say, “Yes, and how does he do that?”  
> He says, “Oh, that’s not my department, I’m sorry.” ⁵

### Footnotes

¹ I’ve used Google Chromecast in my examples because I happen to own one (thanks, [Dominic G](https://medium.com/u/ac1a13a659f5)!). The same questions would apply to an Apple TV, Amazon Fire TV, Roku, etc.

² In philosophical speak, the Chromecast’s ontology consists of signals from the TV and Google.

³ As the popular one-liner goes, “if you think no-one’s watching, miss a few payments”.

⁴ This API is available at [https://developers.google.com/cast/docs/reference/receiver/cast.receiver.CastReceiverManager.html#getStandbyState](https://developers.google.com/cast/docs/reference/receiver/cast.receiver.CastReceiverManager.html#getStandbyState)

⁵ Source: [https://en.tiny.ted.com/talks/dan\_dennett\_on\_our\_consciousness](https://en.tiny.ted.com/talks/dan_dennett_on_our_consciousness).
