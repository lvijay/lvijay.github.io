---
title: "git-magic — predicting a git sha"
description: "Where I perform magic and predict a git commit-id before git commit"
date: "2020-08-15T20:07:55.498Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/git-magic-predicting-a-git-sha-c50d4095d2cf
redirect_from:
  - /git-magic-predicting-a-git-sha-c50d4095d2cf
---

undefined

Below is a three minute video[¹](https://youtu.be/esILqJRuvN4) where I predict a git commit id before actually doing the git commit. Before getting into the video itself, I’ll briefly explain why this is such a big deal, then demonstrate the video, and finally, I discuss the magic.

### Why is this a big deal?

Git’s security model is based on it being impossible to replicate or predict the commit ids beforehand. This is a strong preventive mechanism. Because if someone _could_ actually generate a commit id that matches an existing commit, they could easily insert malicious code into the system. It is not an exaggeration to say this will change the internet forever and it will be a catastrophe of larger proportions than Heartbleed[²](https://heartbleed.com/), Spectre[³](https://en.wikipedia.org/wiki/Spectre_%28security_vulnerability%29), and Meltdown[⁴](https://meltdownattack.com/).

Luckily, I haven’t done that.

### The video

The video is presented below. It’s a little more than 3 minutes. It might better if watched at 1.5x speed because the typing is a little slow.

<Embed src="undefined" aspectRatio={undefined} caption="" />

### Philosophers and magic

Talk of magic always reminds me of two quotations by the cognitive philosopher, Daniel Dennett. I cite them below but elide their larger context. Interested readers can follow the references.

In this first one, Dennett cites the writer Lee Seigel’s experiences and adds his comments to it.

> Lee Seigel: “I’m writing a book on magic”, I explain, and I’m asked, “Real magic?” By _real magic_ people mean miracles, thaumaturgical acts, and supernatural powers. “No”, I answer: “Conjuring tricks, not real magic”. _Real magic_, in other words, refers to the magic that is not real, while the magic that is real, that can actually be done is _not real magic_.⁵

This second quote is even better:

> It is rather as if philosophers were to proclaim themselves expert explainers of the methods of a stage magician, and then, when we ask them to explain how the magician does the sawing-the-lady-in-half trick, they explain that it is really quite obvious: the magician doesn’t really saw her in half; he simply makes it appear that he does. “But how does he do that?” we ask. “Not our department”, say the philosophers.⁶

That second quotation reminds me of a quote by Raymond Smullyan. Smullyan was a logician, a philosopher, and an _actual_ magician (in Dennett’s terms: one who performed magic that could actually be done). This appears in Smullyan’s 1983 book _5000 Thousand B.C. and Other Philosophical Fantasies._

> I performed magic most intensively when I was a student at the University of Chicago. I never did much stage magic; I was a closeup magician who entertained small groups at private parties and more often at the tables of various supper clubs. The following recollection is about my funniest.  
> At one table where I was performing, there was a man who was about the most blase character I have ever met. He just sat there smoking his pipe, saying not a word, and **_nothing_** I could do got the slightest rise out of him. I made my tricks more and more startling, all to no avail. After about twenty-five minutes of increasing effort, I finally did my most spectacular effect, at which he took his pipe out of his mouth, slammed the table with his fist, and angrily shouted, “It’s a **_trick_**!” \[emphasis in original\]

And another gem from the same book:

> Because I have been a magician for many years, people have often asked me whether I ever have sawn a woman in half. I reply, “Oh, yes; I’ve sawn over seventy women in half in my lifetime, and I’m learning the second half of the trick now.”

Smullyan died in Feb 2017, aged 97. While making this video, I was thinking of him and the above book. This post is dedicated to his memory.

Raymond Smullyan teaching at Lehman College in the 1970s. Source: [NYT](https://www.nytimes.com/2017/02/11/us/raymond-smullyan-dead-puzzle-creator.html). License: © New York Times.

### The magic explained

The video was a lot of fun to make and was my first foray into the domain of _magic tricks_. It belongs to the category of performance art and is the code equivalent of a magician sawing someone in half. I now have a much greater appreciation for magicians and performance artists. While this exercise hasn’t helped me divine _their_ tricks, I now have a better understanding of the preparation needed for their work. I realize it is unbelievably hard work.

I also now understand their maxim: A magician never reveals his secrets.

#### Footnotes

¹ Thanks to [Shuveb Hussain](https://medium.com/u/266ee5133326), [Arjun Das](https://medium.com/u/60280e22a81a), [Girish Koundinya](https://medium.com/u/7d5a3ade16b3), and [Geeth Alladi](https://github.com/geethalladi) for early feedback.

² From Dennett’s 2003 paper in the _Journal of Cultural and Evolutionary Psychology_ titled “Explaining the “Magic” of Consciousness”. It is available online at [https://ase.tufts.edu/cogstud/dennett/papers/explainingmagic.pdf](https://ase.tufts.edu/cogstud/dennett/papers/explainingmagic.pdf).

³ This appears in Dennett’s essay titled “Cognitive Wheels: The Frame Problem of AI”, published in the 1987 book, _The Robot’s Dilemma: The Frame Problem in Artificial Intelligence_ edited by Zenon Pylyshyn.

⁴ Heartbleed’s official website explaining the exploit in detail: [https://heartbleed.com/](https://heartbleed.com/).

> The Heartbleed Bug is a serious vulnerability in the popular OpenSSL cryptographic software library. This weakness allows stealing the information protected, under normal conditions, by the SSL/TLS encryption used to secure the Internet. SSL/TLS provides communication security and privacy over the Internet for applications such as web, email, instant messaging (IM) and some virtual private networks (VPNs).

⁵ Spectre’s wikipedia page: [https://en.wikipedia.org/wiki/Spectre\_(security\_vulnerability)](https://en.wikipedia.org/wiki/Spectre_%28security_vulnerability%29)

⁶ Spectre and Meltdown’s official website explaining the exploits in detail: [https://meltdownattack.com/](https://meltdownattack.com/).

> Meltdown and Spectre exploit critical vulnerabilities in modern processors. These hardware vulnerabilities allow programs to steal data which is currently processed on the computer. While programs are typically not permitted to read data from other programs, a malicious program can exploit Meltdown and Spectre to get hold of secrets stored in the memory of other running programs. This might include your passwords stored in a password manager or browser, your personal photos, emails, instant messages and even business-critical documents.
