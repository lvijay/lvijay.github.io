---
title: "Presto sails on the Ship of Theseus"
description: "The Open Source Software, Presto, presents a real-life case study of the philosophical problem: The Ship of Theseus."
date: "2020-05-13T18:23:26.819Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/theseus-67eba9910d47
redirect_from:
  - /theseus-67eba9910d47
---

In November 2013, Facebook released the software Presto as Free/Open Source. At the time, its three primary developers were (alphabetically): Dain Sundstrom, David Phillips, and Martin Traverso. They were also employees of Facebook.

After its release, the software was hugely successful. It was adopted by several of the bigwigs in the software industry such as Netflix, Twitter, Alibaba, Uber, among others. Amazon offered it as part of its AWS platform. The database company, Teradata, also offered support for Presto.

In January 2019, these three developers launched the Presto Software Foundation (PSF, hereonwards), a non-profit organization that was, according to the press release, “dedicated to the advancement of the Presto open source distributed SQL query engine”. \[[prweb](https://www.prweb.com/releases/presto_software_foundation_launches_to_advance_presto_open_source_community/prweb16070792.htm)\]

They released the software as-is (with minor namespace changes) on a different website and in a new repository too. They named their software… Presto.

As you might expect, their decision has led to some confusion amongst users. For instance, just a month after the PSF was founded, on Mar 2019, there was a rather simple question \[[LIST1](https://groups.google.com/d/msg/presto-users/YtltWEMHgjU/DsTzjQs5BAAJ)\]:

> We have seen a new website with entirely new package and version 314, with url [https://prestosql.io](https://prestosql.io/) and version as 314.  
> And I have been living for the last four years with [prestodb.io](http://prestodb.io/).  
> Can anyone please explain what’s the motive behind changing package name and version number and maintaining a new site ?

> Best,  
> Ron.

This confusion continues to this day. Nine months after the project’s founding, in September 2019, a user posted this on the mailing list: “prestodb vs. prestosql is just too similar and confusing for (prospective) end users. Add onto that the fact that [both](https://prestosql.io/) [projects](http://prestodb.github.io/) use the same logo too!” \[[LIST2](https://groups.google.com/d/msg/presto-users/TRwGWf9Z2_o/NV6Ojq-dBAAJ)\]. A few days ago, came the same question: “What is the difference between [prestodb.io](http://prestodb.io/) and [prestosql.io](http://prestosql.io/) ?” \[[LIST3](https://groups.google.com/d/msg/presto-users/EAkzUNFRQps/dWbhPXPMBAAJ)\]

Facebook had earlier clarified that they would not participate in the PSF \[[FB1](https://groups.google.com/d/msg/presto-users/UZO8Bro575w/TaUDqQghCgAJ)\] and they saw PSF’s Presto as a fork \[[FB2](https://groups.google.com/d/msg/presto-users/nyFBBAbtZAI/tn0IAn8gCgAJ)\]. In the Free Software community, a “fork” is when an existing software is developed in a different location.

The PSF founders reject the characterization as a fork. They argue “the original founders and the major contributors that are still active (who wrote the majority of the codebase) are developing on this \[the PSF\] repository” hence, they argue, their version _is_ Presto, not a fork \[[PSFGH1](https://github.com/prestosql/presto/issues/380)\].

Funnily enough, this is a popular problem in philosophy. We’ll quickly review the philosophical problem and return to the current discussion.

---

### The Ship of Theseus

In his 1976 book _Person and Object_, the philosopher Robert M. Chisolm introduces us to a strange ship¹:

> \[L\]et us imagine a ship — the Ship of Theseus — that was made entirely of wood when it came into being. One day a wooden plank is cast off and replaced by an aluminum one. Since the change is only slight, there is no question as to the survival of the Ship of Theseus. We still have the ship we had before; that is to say, the ship that we have now is identical with the ship we had before. On another day, another wooden plank is cast off and also replaced by an aluminum one. Still the same ship, since, as before, the change is only slight. The changes continue, in a similar way, and finally the Ship of Theseus is made entirely of aluminum. The aluminum ship, one may well argue, is the wooden ship we started with, for the ship we started with survived each particular change, and identity, after all, is transitive.

We start with a ship and we replace one by one its every plank. Done _slowly enough_², we will be happy to say this is still the same ship. This is a simple and straightforward conclusion to make. After all, think about ourselves. We are not made of _any_ of the atoms we consisted of when we were born but we’re still ourselves.³

But wait, continues Chisolm citing the first philosopher to pose this problem, Thomas Hobbes:

> ‘If some man had kept the old planks as they were taken out, and by putting them afterwards together in the same order, had again made a ship of them, this, without doubt, had also been the same numerical ship with that which was at the beginning; and so there would have been two ships numerically the same, which is absurd.’

If you rebuild the ship with the discarded planks “_in the same order”_, do you now have two ships of Theseus? Which, then, is the real Ship?

---

### The tale of two Prestos

#### The argument from origin

The argument from the PSF folks is that _identity_ is conferred on the basis of original authors. They also argue that the top contributing developers (in raw bytes, not necessarily impact), were working on PSF’s software \[[LIST4](https://groups.google.com/d/msg/presto-users/TRwGWf9Z2_o/iA4X6w1SBgAJ)\]. In other words, their argument is that the second ship is the true ship of Theseus and that this holds because it’s made of the first planks that were on the ship and many crew members have also, pardon the pun, jumped ship.

Facebook’s argument is that theirs is Presto as they continue their “development efforts in the original prestodb Github repository” \[[LIST5](https://groups.google.com/d/msg/presto-users/TRwGWf9Z2_o/TAgtb4BWBQAJ)\] and that “Presto was developed at Facebook by a group of its employees. A few months ago, three of them left the company and forked the project” \[[LIST6](https://groups.google.com/d/msg/presto-users/TRwGWf9Z2_o/SAE9t85KBgAJ)\].

Does the majority of original participants confer identity? If so PSF’s is Presto and Facebook’s isn’t (though nobody describes what it is).

#### The argument from purpose

The argument from one of PSF’s Presto is that both softwares can remain with the same name because they soon diverge even in their behavior. Dain Sundstrom, one of Presto’s original authors, and a cofounder of the PSF, took this view in April 2019. He pointed out the two codebases were significantly different in size since PSF was formed and were also architecturally “taking very different approaches to major change\[s\]”. \[[LIST7](https://groups.google.com/d/msg/presto-users/TRwGWf9Z2_o/KdbVoeiaBgAJ)\]

Does divergence in behavior and name confer identity? If one sticks with the original purpose and the other changes what it does, which shall we describe as the Presto?

For instance, the popular chewing gum brand Wrigley’s was originally company that sold soap and baking soda[⁴](https://www.theguardian.com/business/2008/apr/28/fooddrinks1). They ditched the soap and switched to gum. Did the company change during this transition or did it remain the same company?

Which software, then, _is_ Presto?

As rapper Eminem might put it, Will the real Presto please stand up?

### Footnotes

¹ My own reference is from Chapter 21 of the book, _Metaphysics: An Anthology_ (1999), edited by Jaegwon Kim, Ernest Sosa. Blackwell Publishing Ltd.

² I make no attempt to quantify my “slowly enough”.

³ According to this article in the [NPR](https://www.npr.org/templates/story/story.php?storyId=11893583), 98% of the atoms in our body are replaced every year. To put this in perspective, supposing a baby is born with _x_ atoms, after five years, it’ll only have 0.000016% of those original atoms. Given that babies grow, this is vanishingly small. When the child is 16, the fraction of atoms remaining is 6.5536×10⁻²⁸. Perhaps some fraction of atoms are recycled but the point remains.

⁴ Apr 2008 article in the Guardian, “Wrigley’s sold to Warren Buffet”, by Graeme Wearden and Andrew Clark. Available online at [https://www.theguardian.com/business/2008/apr/28/fooddrinks1](https://www.theguardian.com/business/2008/apr/28/fooddrinks1).

### Epilogue

My 2¢? The Facebook Presto is Presto and PSF is a fork. One curiously common assumption everyone who opines on this matter makes is that the Presto maintained by Presto just is Presto. All requests to rename go to PSF’s Presto. The latter organization, have only defended their own rights to use the same name, but have not, to my knowledge, stated that Facebook’s Presto must change its own name which, as I see it, is a tell. Philosophy don’t run on popularity or majority but when close to unanimous populations intuitively feel one is the real Presto and the other the fork, there’s something to observe there.

A ship named Theseus. Source: [Wikimedia](https://commons.wikimedia.org/wiki/File:Theseus_-_IMO_9390159.JPG). License: public domain.
