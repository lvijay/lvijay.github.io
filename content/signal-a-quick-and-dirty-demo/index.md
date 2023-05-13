---
title: "Signal: A Quick and Dirty demo"
description: "A short code demo of the Signal protocol."
date: "2017-09-19T13:15:42.299Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/signal-a-quick-and-dirty-demo-eca47d76d4f3
redirect_from:
  - /signal-a-quick-and-dirty-demo-eca47d76d4f3
---

I’ve been playing with the Signal codebase and there are either too few examples out there or I’m just poor at Googling. Since I couldn’t find a simple code sample for exchanging messages using the Signal Protocol I went ahead and wrote one.

As is common in cryptography literature, I shall use the famous pair, [Alice and Bob](https://en.wikipedia.org/wiki/Alice_and_Bob), who wish to exchange messages with one another. (More serious discussions in cryptography involve Eve, who wishes to eavesdrop on their conversation but I don’t discuss that here. This is not a cryptography post, merely a code show-and-tell involving a cryptographic library.)

The code is mostly based on the unit test [SessionBuilder::testBasicPreKeyV3](https://github.com/WhisperSystems/libsignal-protocol-java/blob/98e88b749a262055b2fab0b1511c217ea5bde6f6/tests/src/test/java/org/whispersystems/libsignal/SessionBuilderTest.java#L46) in [libsignal-protocol-java v2.3.0](https://github.com/WhisperSystems/libsignal-protocol-java/tree/v2.3.0/).

In all public key cryptography, Alice creates for herself an _identity_, consisting of a paired _private key_ and _public key_. The public key is advertised, the private key remains private. When Alice acquires¹ Bob’s public key she can send him messages. Alice, after encrypting her messages, also _signs_ them. A signed message identifies, to Bob, Alice as the sender. Thus, to extract the encrypted message from a signed message, Bob, too, must acquire¹ Alice’s public key.

This is typical of public key cryptography. The difference with Signal is that these keys change between message exchanges.

The main class, `[Demo](https://github.com/lvijay/DemoSignal/blob/master/src/hacking/signal/Demo.java)`, does the following

1.  Creates two `[Entity](https://github.com/lvijay/DemoSignal/blob/master/src/hacking/signal/Entity.java)` instances representing Alice and Bob
2.  Initiates a `[Session](https://github.com/lvijay/DemoSignal/blob/master/src/hacking/signal/Session.java)` introducing¹ Bob to Alice
3.  Alice sends a few messages to Bob
4.  A session between Bob and Alice is then created so Bob can decrypt the messages received from Alice
5.  Bob sends a few messages to Alice
6.  Bob’s messages reach Alice out of order but he’s nevertheless able to decrypt them.

The class, `Entity`, is a simple placeholder for the various identity requirements of the Signal Protocol. The constructor generates the different keys needed for the exchange.

`Session` is more interesting. If Alice sends Bob a few messages, Bob decrypts them, and then Bob sends Alice some messages _without updating_ the `SessionCipher`, the library throws an `InvalidKeyIdException`. This is part of Signals goals towards maintaining forward-secrecy and their [“three step ratchet”](https://signal.org/blog/advanced-ratcheting/).

Quoting from the Signal documentation:

> If Alice needs to send multiple messages to Bob before he replies, Alice will need to keep using her current key and advertising the same next key.

With that, the code is in [https://github.com/lvijay/DemoSignal](https://github.com/lvijay/DemoSignal). It’s licensed under the [AGPL v3](https://www.gnu.org/licenses/agpl-3.0.html).

#### Footnotes

¹ The question of how Alice and Bob exchange keys in a secure manner is perhaps the hardest problem in all cryptography. I do not touch it at all.
