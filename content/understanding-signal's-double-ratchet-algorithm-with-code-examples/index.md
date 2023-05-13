---
title: "Understanding Signal’s Double Ratchet algorithm with code examples"
description: "Signal’s Double Ratchet algorithm is what powers the world’s most popular messaging systems—WhatsApp and Facebook Messenger (both owned by…"
date: "2023-05-13T11:45:03.435Z"
categories: []
published: false
---

Signal’s Double Ratchet algorithm is what powers the world’s most popular messaging systems—WhatsApp and Facebook Messenger (both owned by Facebook). WhisperSystems, the 501c3 non-profit behind the protocol itself has a messaging software, Signal, which implements the same.

An explanation of the protocol is available on Signal’s website at [https://signal.org/docs/specifications/doubleratchet/](https://signal.org/docs/specifications/doubleratchet/). This post uses the illustrations in that website along with code examples from their GitHub page ([https://github.com/signalapp/libsignal-protocol-java](https://github.com/signalapp/libsignal-protocol-java)). I’ll be using code examples from one of my older posts, “Signal: A Quick and Dirty demo”.

This post is an annotated version of my “Signal: A Quick and Dirty demo”. It shows that code along with images from Signal’s Double Ratchet page.

Signal put their documentation in [the public domain](https://signal.org/docs/specifications/doubleratchet/#ipr) so I’m not, afaik, violating any copyrights.

Here’s the scenario. Alice and Bob wish to exchange messages with one another. As pointed out in the footnote to my earlier article, the “question of how Alice and Bob exchange keys in a secure manner is perhaps the hardest problem in all cryptography. I do not touch it at all.” But, let’s assume that the public key Alice gets really is Bob’s, not some attacker’s.

Going by Signal’s documentation (hereafter referred to simply as “the documentation”), we have the below image.

Alice and Bob wish to exchange messages with one another

The [class](https://github.com/lvijay/DemoSignal/blob/master/src/hacking/signal/Entity.java) `[Entity](https://github.com/lvijay/DemoSignal/blob/master/src/hacking/signal/Entity.java)` represents either Alice or Bob. It is briefly shown below.

```
public class Entity {
    private static final int DEVICE_ID = 1;

private final SignalProtocolStore store;
    private final PreKeyBundle preKey;
    private final SignalProtocolAddress address;

public Entity(int preKeyId, int signedPreKeyId, String address)
            throws InvalidKeyException
    {
        this.address = new SignalProtocolAddress(address, DEVICE_ID);
        this.store = new InMemorySignalProtocolStore(
                KeyHelper.generateIdentityKeyPair(),
                KeyHelper.generateRegistrationId(false));
        IdentityKeyPair identityKeyPair = store.getIdentityKeyPair();
        int registrationId = store.getLocalRegistrationId();

ECKeyPair preKeyPair = Curve.generateKeyPair();
        ECKeyPair signedPreKeyPair = Curve.generateKeyPair();
        long timestamp = System.currentTimeMillis();

byte[] signedPreKeySignature = Curve.calculateSignature(
                identityKeyPair.getPrivateKey(),
                signedPreKeyPair.getPublicKey().serialize());

IdentityKey identityKey = identityKeyPair.getPublicKey();
        ECPublicKey preKeyPublic = preKeyPair.getPublicKey();
        ECPublicKey signedPreKeyPublic = signedPreKeyPair.getPublicKey();

this.preKey = new PreKeyBundle(
                registrationId,
                DEVICE_ID,
                preKeyId,
                preKeyPublic,
                signedPreKeyId,
                signedPreKeyPublic,
                signedPreKeySignature,
                identityKey);

PreKeyRecord preKeyRecord = new PreKeyRecord(preKey.getPreKeyId(), preKeyPair);
        SignedPreKeyRecord signedPreKeyRecord = new SignedPreKeyRecord(
                signedPreKeyId, timestamp, signedPreKeyPair, signedPreKeySignature);

store.storePreKey(preKeyId, preKeyRecord);
        store.storeSignedPreKey(signedPreKeyId, signedPreKeyRecord);
    }
```
