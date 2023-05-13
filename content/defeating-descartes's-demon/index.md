---
title: "Defeating Descartes’s Demon"
description: "In an earlier piece (click here) I introduced René Descartes’s Demon, “a malignant genius” intent upon deceiving you and equated this Demon…"
date: "2023-05-13T11:45:25.975Z"
categories: []
published: false
---

In an earlier piece (click [here](https://medium.com/@lvijay/ren%C3%A9-descartes-security-engineer-777a3d051864)) I introduced René Descartes’s Demon, “a malignant genius” intent upon deceiving you and equated this Demon with an evil hacker equally determined to take over your computer.

In this — much longer — piece I consider some ways to overcome doubts that your computer has been hacked. (Spoiler: we’ll fail.) Then we’ll briefly discuss Internet security: in turn, peer-to-peer (P2P, i.e. person-to-person) secure encryption, then browser security (i.e. how safe are your credit cards when sent over the browser), and finally the new peer-to-peer encryption technologies popularized by the mobile chat applications, Signal, WhatsApp, and Telegram and how Descartes’s Demon gets in the way in each. Long story short: there’s no escaping the evil genius’s clutches.

#### Beating the Demon/Evil Hacker

1.  **Starvation**  
    You decide that you’ll let your laptop (or phone) die from a lack of charge. And then switch it on. When your computer powers up with charge, it’ll start without the Demon’s program, right? Sadly, no. There are two problems:  
    (**a**) remember, the Demon has taken control of your _software._ Thus any indicator of your battery-charge-remaining is in the Demon’s control. And, as Descartes says, this Demon is “a malignant genius, as powerful as he is cunning and deceitful, who has used all his zeal to deceive \[you\]” ¹, so we must expect he’ll be wise to this. All the Demon needs to do is to show the battery as draining much earlier than it actually does. For example, while there’s still (say) 50% charge remaining on your device, the Demon has your device show that there’s only 0% charge remaining, switches off the screen and makes it appear _as if_ your phone’s switched off ². When you press the power-on button, since the phone isn’t actually off, the hacker’s software program gives all signs of a phone rebooting without actually doing so.  
    (**b**) you decide to physically extract the battery and restart the device. This is definitely a good approach. Except, it’s not guaranteed to work. When your phone/computer start up (boot up), they run a program called the “bootloader” and, while exceedingly difficult, they have been hacked.  
    Android: as recently as Sep 2017 (3 months ago, as of this post), researchers found vulnerabilities in “[five major chipset vendors](http://www.ehackingnews.com/2017/09/android-bootloaders-vulnerable-to.html)”. In general, if a hacker has root (or administrative) level access to a device or a machine, they can install a “[rootkit](https://en.wikipedia.org/wiki/Rootkit)” from which it’s almost impossible to escape.  
    Among (a) and (b), (b) is better. While it isn’t guaranteed to work, the good news is that _if_ you’re still being attacked, then this person (or entity) has gone through a _lot_ of effort to hack you. You should feel proud that you’re so important that someone would go to such lengths. As Descartes puts it, “so, let \[the Demon\] deceive me as much as he likes”. (I’ve got nothing else. Sorry.)
2.  **Detection  
    **Hook up your device’s battery to an external device which reads how much charge actually remains. An out-of-band verification like this is a good idea, in general. This isn’t guaranteed to work either because while our detector reading the battery might be correct, it’s possible that the _physical connection_ between the battery and the phone is corroded so it’s unable to use the battery correctly. (Descartes didn’t discuss this because his discussion dealt with the unreliability of our senses and there’s no out-of-band validation there.)
3.  **Validation**  
    This actually might work. You physically power off your computer (as in 1b above). Connect the hard disk to an external machine that you trust and have it validate that the operating system is the correct expected version.  
    Finding that external machine that you trust is hard because your own machine was supposed to be one you could trust. Next, it’s possible that your Operating System is fine but the programs installed in it are suspect. This is harder to detect because it’s really hard to see where all your programs are installed. It’s harder to control which ones run at start up. But these steps, which are doable in theory, would work. So, if you can overcome the almost-impossible-to-guarantee problem of acquiring a trustworthy machine, you’re home safe.

What’s the answer, then? In short, there isn’t one. If you’re using a computer, especially in this day and age, you cannot be sure it is what it is. Pondering this question is what led Descartes to formulate his famous _cogito ergo sum_, or _I think, therefore, I am_. Descartes said that the only thing of which he could be certain was his own existence.

> Am I so dependent on my senses and on my body that I cannot exist without them? In persuading myself that there was nothing at all in the world,… did I not also persuade myself that I did not exist? Certainly not, for there can be no doubt that I exist in the very act of persuading myself, or indeed of thinking at all.… But there is no doubt that I exist in being deceived, and so, let him \[the Demon\] deceive me as much as he likes, he can never turn me into nothing so long as I think that I am something. Whence, after due thought and scrupulous reflection, I must conclude that the proposition, _I am, I exist_, is true of necessity every time I state it or conceive it in my mind. _\[my emphasis\] ¹_

These thought experiments led Descartes to formulate two entities: _mind_ and _body_. He concluded that mind surely existed but body, not so much.

In our computer analogy, you, the human, are the _mind_ and the computer is the _body_. As you can see, you certainly exist, but all your interactions with the computer software are suspect and possibly not what they seem.

If you read the Meditations, you’ll see that he discusses pretty much the same steps I outline above.

### Internet security

Okay, presumably, it’s impossible to beat the genius Evil Hacker/Demon. How at all does the Internet function then?

#### Part I

**Secure communications between peers  
**As with most security texts, we’ll consider two parties, Alice and Bob, who wish to securely communicate with one another and Eve, who wishes to listen in on their conversation. Alice and Bob are acquainted with one another and wish, specifically, to communicate with each other and nobody else.

It’s assumed that Eve controls the network on which Alice and Bob communicate. Note: this “network” can be anything. If Alice and Bob communicate by carrier pigeon, Eve could capture the pigeon, copy its message, and send off the pigeon. There’s no guarantee that Eve _won’t_ change messages in-flight (pun intended). If Alice and Bob communicate via snail mail, Eve can intercept the mail, open the envelop, read the contents, put them into a new envelop, and send that over. The standard assumption in modern day cryptography is that Eve can and will intercept and store all of Alice’s communications but Alice is still certain that Bob and only Bob can read Alice’s message. (By way of analogy, suppose you and your peer are sitting on opposite ends of a bus and you can only communicate with one another by shouting. Of course everyone can hear you so you lack privacy. So to secure privacy you speak to each other in [Navajo](https://en.wikipedia.org/wiki/Code_talker#Navajo_code_talkers). ⁴)

The way it works is Alice, on her machine, generates two keys: a _private key_ and a _public key_. Bob does similarly on his machine. These keys relate to one another in a special manner which I’ll discuss presently. In terms of what they can do, the keys are indistinguishable from one another, but the manner in which they’re used is radically different. The public key is publicized and the private key is never exposed. When a message is encoded using a public key, we describe the operation as _encryption_. When the message is encoded using a private key, the operation is called _signing_. If I can decode a message using a private key, the operation is called _decryption_; and if I can decode a message using a public key, the operation is called _verification_.

The specialty of private/public keys is that a message encrypted with a private key can only be decrypted by its public key and nothing else, and conversely, a message encrypted with a public key can only be decrypted by its private key and nothing else. Thus, the ability to decode a message using a key proves that it was encoded by that key’s pair. If I am able to verify a message using Alice’s public key, it proves³ that Alice signed the message and she’s the message’s originator.

Now, when Alice wants to send Bob a message, she composes her message, _encrypts_ it using Bob’s public key, _signs_ it with her private key, and sends it to him.

Bob, upon receiving aforesaid message, verifies that it is indeed from Alice using her public key and then decrypts the message with his private key and reads it.

(An interesting corollary of public key cryptography is that if Alice has encrypted a message to send Bob, after encryption she cannot see what’s in the encrypted message. Only Bob can.)

Back to Descartes, then. I cheated in my description above. While I described perfectly how Alice and Bob can exchange messages, I didn’t discuss how they came to acquire each others’s public keys. I could put up my public key on [https://pgp.mit.edu/](https://pgp.mit.edu/) but when you go there and search for my name, you have no way of knowing if the key listed under my name is really me or — you guessed it — an Evil Hacker posing as me. (Now, I’m perfectly aware that no one on this planet wishes to pose as me — most of the time even I don’t — but these [two](https://pgp.mit.edu/pks/lookup?search=linus+torvalds&op=index) [links](https://pgp.mit.edu/pks/lookup?search=bill+gates&op=index) should make my point clear.) One way security buffs do this is to attend “[key signing parties](https://en.wikipedia.org/wiki/Key_signing_party)” where they print their public keys on paper, meet others, identify themselves using their (presumably authentic) drivers licenses/passports etc, actually sign their public key printout and share them. Later, members lookup that particular public key online and sign them, this time digitally. (As you might expect, this is such a popular event that every year the same three people meet and sign each others’ public keys just as they have for the last twenty years.)

The developers of [Gnu Privacy Guard](https://gnupg.org/) (GPG), the most popular implementation of the consumer public key cryptography, recognize the dangers of Descartes’s Demon. When you attempt to decrypt a file, you see the following warning message:

```
gpg: WARNING: message was not integrity protected
```

According to the GPG developers, this warning is [emitted to remind people](https://lists.gnupg.org/pipermail/gnupg-users/2004-October/023500.html) that their data could, in theory, be modified during the course of encryption.

> That message is on purpose to remind people that they should use the MDC feature.…

> The MDC features solves a problem _when an attacker modifies parts of an encrypted messages_, e.g. by cutting out some parts, and the user did not noticed a couple of garbled characters (he might think this is line noise). _\[my emphasis\]_

And don’t assume from the dates on the above discussion (2004) that security is a solved problem. Far from it. This, below, is from the GPG archives of Aug 2017. When discussing a complicated security attack known as “May the Fourth be With You”, as an aside, mention [this gem](https://lists.gnupg.org/pipermail/gnupg-announce/2017q3/000414.html):

> Allowing other users to run software on a machine with private keys should be considered a full security compromise of that machine, anyway.

Translation: you must have a dedicated machine for encrypting and decrypting messages and it must do nothing but encryption and decryption. The worst part about this warning is that it’s true.

Okay, suppose then you do everything the security experts describe. Are you safe? The unsurprising answer if you’ve come this far is, of course, no. In October 2015, [security researchers Alex Halderman and Nadia Heninger](https://freedom-to-tinker.com/2015/10/14/how-is-nsa-breaking-so-much-crypto/) published a report detailing how the NSA was able to defeat the then recommended, industry-standard encryption algorithm. (See below for my poker metaphor.)

Incidentally, this attack where an attacker places themselves in between two parties is known by the rather boring but descriptive (and slightly sexist) name, “Man-in-the-Middle” (MITM). The problem is easily illustrated with computers but hardly restricted to it. Think of all spy movies where the good guys, to intercept communications between the bad guys, capture the original courier, and send the protagonist instead which, predictably, ends with multiple explosions and car chases. (Hollywood isn’t sufficiently interested in MITM attacks.) To take a more realistic example, consider the [Stingray program](https://www.aclunc.org/blog/aclu-sues-government-information-about-stingray-cell-phone-tracking) which can “mimic a cell tower and obtain information from all wireless devices on the same network in a given area”. So if you’re on, say, Verizon, and your phone shows you as having connected to Verizon, it isn’t necessarily Verizon but possibly a Stingray device acting as a Verizon proxy. Those arbitrary call drops? Those suddenly strong cell signals? Those glitches in the Matrix are possibly just shoddy service or a Stingray and [we’ll never know](https://www.wired.com/2014/03/stingray/).

Descartes laughs in his grave.

#### Part II

**Secure communication with unknown entities aka How do browsers work?**  
Okay, the good news is the Internet mostly works and [while security as a practice is just terrible](https://www.welivesecurity.com/2016/10/24/10-things-know-october-21-iot-ddos-attacks/), and most applications out there are not designed for security, [and](http://www.dailymail.co.uk/news/article-2123854/1-5million-account-numbers-hacked-Visa-Mastercard-card-data-theft.html) [most](https://www.nytimes.com/2016/12/14/technology/yahoo-hack.html) [major](https://www.forbes.com/sites/winniesun/2017/10/02/what-you-should-do-now-after-the-equifax-security-leak/) [websites](https://techcrunch.com/2006/08/06/aol-proudly-releases-massive-amounts-of-user-search-data/) [have](https://www.cnet.com/news/ebay-hacked-requests-all-users-change-passwords/) [been](http://www.zdnet.com/article/amazon-is-resetting-account-passwords-for-some-accounts/) [subject](http://www.theregister.co.uk/2016/05/24/linkedin_password_leak_hack_crack/) [to](http://www.independent.co.uk/life-style/gadgets-and-tech/is-apples-icloud-safe-after-leak-of-jennifer-lawrence-and-other-celebrities-nude-photos-9703142.html) [security](http://fortune.com/2016/11/30/google-android-fraud/) [breaches](http://www.dailymail.co.uk/news/article-2123854/1-5million-account-numbers-hacked-Visa-Mastercard-card-data-theft.html), [some](https://www.huffingtonpost.com/entry/major-security-breaches-found-in-google-and-yahoo-email-services_us_5729f450e4b016f378942950) [multiple](https://www.welivesecurity.com/2015/12/11/microsoft-issues-warning-xbox-live-certificate-inadvertently-leaks/) [times](https://www.washingtonpost.com/world/national-security/chinese-hackers-who-breached-google-gained-access-to-sensitive-data-us-officials-say/2013/05/20/51330428-be34-11e2-89c9-3be8095fe767_story.html)…. Never mind. [Security is in pretty bad shape](https://krebsonsecurity.com/category/latest-warnings/).

Deep Breath. Here I go again. Okay, the good news is it’s not all Descartes’s fault. Because, utopian as it sounds, the non-Decartes-Demon problems described above can be addressed piece by piece.

undefined

Now, let’s consider how browsers function and why you should update your browsers/phones often, especially if they say “security fix”. The simple question is: how do we know that entering “f s f . o r g” in your browser actually takes you to [fsf.org](https://fsf.org) (and not some other)? What does the 🔒 on your address bar signify?

The idea behind browser security is sort of like debunking a conspiracy. Conspiracies are possible but really, really hard to effect and become that much harder as the number of participants increase. The reasoning goes something like this: for you to be hacked, many stars must align; since you’re not that important, you’re probably not hacked. This is not counting technical details behind cryptography. The maths behind cryptography is widely accepted to be unbreakable (aka “computationally intractable”). That’s where the Demon comes in. The best poker strategy is all for naught if your opponent can see your hand.

Browser security works in a very simple and utterly beautiful manner.

For Internet browser security we have the following players: we have providers, (like gnu.org, thisishell.com, aclu.org), and we have people who wish to access the providers and only the providers (i.e. us).

### Footnotes

¹ All references from Descartes are from Descartes, René. _Discourse on Method_. Great Britain, Penguin 1960. Trans. Wollaston, Arthur.

² If you think this is very far fetched, see this 2014 WIRED [article](https://www.wired.com/2014/06/nsa-bug-iphone/) by Andy Greenberg in which he says:

> Like any magic trick, the most plausible method of eavesdropping through a switched-off phone starts with an illusion. Security researchers posit that… software could make the phone _look_ like it’s shutting down — complete with a fake “slide to power off” screen. Instead of powering down, it enters a low-power mode that leaves its baseband chip — which controls communication with the carrier — on. _\[emphasis in original.\]_

³ Strictly speaking, the signature only proves that the message was signed by Alice’s private key, not necessarily by Alice herself for it could be that Alice was hacked and so on.

⁴ I chose Navajo because the Navajo people did exactly this during WWII. The Japanese could intercept all messages sent to American soldiers but because the messages were in Navajo they couldn’t interpret them. See Mark Baker’s _The Atoms of Language_ (2001) for more information and also Mark Baker’s [Code-talker paradox](https://en.wikipedia.org/wiki/Code-talker_paradox).
