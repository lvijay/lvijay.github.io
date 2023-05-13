---
title: "If a tree falls in the forest (Part II)"
description: "Philosophy is great if you're only asking questions but if you actually want answers, you need engineering."
date: "2018-04-22T15:53:37.444Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/but-does-it-5807b7596f90
redirect_from:
  - /but-does-it-5807b7596f90
---

undefined

If a tree falls in the forest, does it make any sound?

#### Does it?

In an [earlier post](https://medium.com/galileo-onwards/if-a-tree-falls-in-the-forest-655e4cbcd5cb) I discussed the kinds of things to look for to figure out if my Google Chromecast consumed bandwidth even when it was connected to a powered off TV. While I didn’t actually answer the question I discovered that the Chromecast had the capability to stop consuming bandwidth if the TV was off (tl;dr it depends on the TV and how the Chromecast software’s written).

There were too many gaps in my earlier post and I cringe that I published it with _no_ verification. Anyway, I hope to correct those mistakes here. Those mistakes include:

1.  Considering the wallpapers app is all well and good but what happens in the case of time bound streams? Suppose I’m listening to a 3 hour Carnatic kutcheri, switch off the TV, turn it on again in 15 minutes. I expect that the kutcheri has progressed for 15 minutes. While the Chromecast _can_ be programmed in a manner to not use bandwidth under these conditions, it doesn’t answer _if_ it actually happens. ¹
2.  When I connect to the Chromecast app on my phone, it actually shows me _what_ wallpaper’s now on display. Again, this too _can_ be implemented such that it doesn’t consume bandwidth but is it so implemented? ² Let’s find out.

So let’s devise some experiments. The easiest is to see what traffic goes in and out of the Chromecast when nothing but wallpapers are shown keeping the TV on as a control case. Depending on the results, see what happens when the TV is off.

When I run my trusted `tcpdump` against it (as below) the weird thing is all traffic was only between the Chromecast and my laptop.

```
$ tcpdump -i en0 -tvvvX 'host chromecast-ip'
IP (tos 0x0, ttl 64, id 8530, offset 0, flags [DF], proto TCP (6), length 52)
    laptop_ip.56795 > chromecast_ip.8009: Flags [.], cksum 0x70e1 (correct), seq 1956, ack 2154, win 4092, options [nop,nop,TS val 869102325 ecr 2721150], length 0
...
IP (tos 0x0, ttl 64, id 29161, offset 0, flags [DF], proto TCP (6), length 167)
    laptop_ip.56795 > chromecast_ip.8009: Flags [P.], cksum 0x5c53 (correct), seq 1956:2071, ack 2154, win 4096, options [nop,nop,TS val 869102325 ecr 2721150], length 115
...
IP (tos 0x0, ttl 64, id 60177, offset 0, flags [DF], proto TCP (6), length 52)
    chromecast_ip.8009 > laptop_ip.56795: Flags [.], cksum 0x7f40 (correct), seq 2154, ack 2071, win 294, options [nop,nop,TS val 2721154 ecr 869102325], length 0
...
```

(I’ve replaced the IPs with `chromecast_ip` and `laptop_ip` just to give it some context. I’ve also deleted the actual data exchanged. It was uninteresting.) Looking into which process on my machine was doing this communication (on `port 56795` above) gave the answer: Google Chrome browser.

![](./asset-2.png)O Okay, my Chrome browser is constantly chatting with the Chromecast as a way to show the cast-to-Chromecast icon (shown left). Fair enough.

To eliminate this noise I close the Chrome browser. And once again resume my listening:

```
$ tcpdump -i en0 -tvvvX 'host chromecast-ip'
```

And, as I predicted in my earlier post, the logs gave me nothing. Mind you, this is with the TV on and wallpapers changing. 10 minutes… nothing.

Suddenly there’s a lot of noise.

```
IP (tos 0xc0, ttl 1, id 0, offset 0, flags [DF], proto IGMP (2), length 48, options (RA))
    chromecast_ip > igmp.mcast.net: igmp v3 report, 2 group record(s) [gaddr 239.255.255.250 is_ex { }] [gaddr 224.0.0.251 is_ex { }]
 0x0000:  46c0 0030 0000 4000 0102 42e3 c0a8 0066  F..0..@...B....f
 0x0010:  e000 0016 9404 0000 2200 0907 0000 0002  ........".......
 0x0020:  0200 0000 efff fffa 0200 0000 e000 00fb  ................
IP (tos 0xc0, ttl 1, id 0, offset 0, flags [DF], proto IGMP (2), length 48, options (RA))
    chromecast_ip > igmp.mcast.net: igmp v3 report, 2 group record(s) [gaddr 239.255.255.250 is_ex { }] [gaddr 224.0.0.251 is_ex { }]
 0x0000:  46c0 0030 0000 4000 0102 42e3 c0a8 0066  F..0..@...B....f
 0x0010:  e000 0016 9404 0000 2200 0907 0000 0002  ........".......
 0x0020:  0200 0000 efff fffa 0200 0000 e000 00fb  ................
```

It turns out to be IGMP messages. Until today I didn’t know such a thing as IGMP existed. Wikipedia says:

> The **Internet Group Management Protocol (IGMP)** is a communications protocol used by hosts and adjacent routers on IPv4 networks to establish multicast group memberships. IGMP is an integral part of IP multicast.

> IGMP can be used for one-to-many networking applications such as online streaming video and gaming, and allows more efficient use of resources when supporting these types of applications. ³

Here, I have a personal problem. When I set out to work on this problem (an exercise that began with the previous post), I wanted to find the answer but without actually _learning_ things. ⁴ But here I am, finding about the existence of a protocol. Anyway, a discovery protocol can’t be how the Chromecast gets its wallpapers. Ignore and carry on.

```
$ tcpdump -i en0 -tvvv 'host chromecast_ip and not igmp'
```

And… nothing. I cast a video through my cellphone and still nothing. Google gives me the answer: when your WiFi security policy is WPA2-PSK you can’t directly listen in on traffic. There are several instructions to follow and they’re all provided in a blog titled “Decrypt WPA2-PSK using Wireshark”. ⁵

But I’m not going to do any of that. Instead, I will switch my WiFi to use no encryption, update the Chromecast to use the new WiFi, connect, test it out. Then, once I’ve discovered the answer, I’ll reconfigure my WiFi, reconfigure the Chromecast… Fuck it. I can live without the answers to some questions.

The End.

#### Footnotes

⁰ Image is a composite of Chromecast image from Wikipedia and the tcpdump logo from the official website. Chromecast Image accessed at: [https://en.wikipedia.org/wiki/Chromecast#/media/File:Chromecast-2015.jpg](https://en.wikipedia.org/wiki/Chromecast#/media/File:Chromecast-2015.jpg) and tcpdump logo accessed at [http://www.tcpdump.org/](http://www.tcpdump.org/). Image licensed CC-BY-SA, same as the Wikipedia image.

¹ If you’re curious about the how, it’s pretty straightforward. Imagine you’re in high school and supposedly reading your history textbook under the watchful eyes of a parent. When the parent leaves, you do what actually interests you, fifteen minutes later, when you hear the parent coming back, just turn the book forward (say) 15 pages and continue reading.

² This technique too is rather similar to that described above. I’m unable to think of an analogy so I’ll describe the (potential) implementation itself. We know from the earlier post that the Chromecast can listen for TV events such as switch-off and switch-on. Now, downloading an image would take about 400ms but a TV takes a second or more to switch on. That difference of 600ms is all an implementation needs. The phone can show any images but the Chromecast would do nothing. If you turn on your TV, it’ll send a signal to the Chromecast, which then has enough time to download the same image as shown on your phone.

³ Wikipedia article available at [https://en.wikipedia.org/wiki/Internet\_Group\_Management\_Protocol](https://en.wikipedia.org/wiki/Internet_Group_Management_Protocol) and accessed on Apr 15 2018.

⁴ My attitude is much like that described by Bill Watterson. Specifically the comic — shown below — published on Jan 5, 1993, available at [http://www.gocomics.com/calvinandhobbes/1993/01/05](http://www.gocomics.com/calvinandhobbes/1993/01/05).

undefined

⁵ “Decrypt WPA2-PSK using Wireshark” available at [https://mrncciew.com/2014/08/16/decrypt-wpa2-psk-using-wireshark/](https://mrncciew.com/2014/08/16/decrypt-wpa2-psk-using-wireshark/).
