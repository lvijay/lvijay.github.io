---
title: "Wonderful Life: HTTP and the Nature of History"
description: "HTTP is now the most successful internet protocol. In today’s world there are handful of other protocols (NTP, SMTP, ICMP to name a few)…"
date: "2023-05-13T11:44:38.007Z"
categories: []
published: false
---

HTTP is now the most successful internet protocol. In today’s world there are handful of other protocols (NTP, SMTP, ICMP to name a few) that are still in use but they are nowhere near the scale of HTTP. This wasn’t always the case. In fact, at the origin of the internet, there was an explosion of protocols of which HTTP was but one. Most of the other protocols are now dead. This fact has a curious parallel with biological evolution and that’s what we’ll be looking at in this post.

In today’s internet, practically everything over the internet occurs over HTTP. (In this post I use HTTP but it should be read as HTTP/HTTPS.) There has been a lot of innovation within the internet ecosystem and much of this innovation has occurred _within_ HTTP, or has been built on top of HTTP. In fact, a lot of the innovation has been much to circumvent the inherent limitations of HTTP — websockets for example. As we go on, we’ll see how the framework of HTTP is expected to limit the kinds of innovations that _do_ occur, why that’ll be hard to change (if you’re of a humorous bent, you could say HTTP is now Too Big To Change ;-), and why none of this is necessarily a bad thing.

The title of this post is a play on _Wonderful Life: The Burgess Shale and the Nature of History_, a 1989 book written by the legendary paleontologist and science historian, Stephen Jay Gould (1941–2002). We will see why in due course.

### The Cambrian Explosion

Around 570 million years ago, modern multicellular animals made their first appearance in the fossil record. This event is called the _Cambrian explosion_. And an explosion it was. It “mark\[ed\] the advent of virtually all major groups of modern animals—and all within the minuscule span, geologically speaking, of a few million years”.
