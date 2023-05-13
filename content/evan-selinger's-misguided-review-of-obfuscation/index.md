---
title: "Evan Selinger’s misguided review of “Obfuscation”"
description: "Evan Selinger ponders “the ethical question of whether it’s really okay for us to defend ourselves by polluting corporations data pools”."
date: "2017-09-20T12:52:04.517Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/evan-selingers-misguided-review-of-obfuscation-38a812cb1952
redirect_from:
  - /evan-selingers-misguided-review-of-obfuscation-38a812cb1952
---

> Half the money I spend on advertising is wasted; the trouble is I don’t know which half. — John Wanamaker (attributed)

Evan Selinger, [professor of philosophy at Rochester Institute of Technology](https://lareviewofbooks.org/contributor/evan-selinger), in his [critical review](https://lareviewofbooks.org/article/internet-privacy-stepping-up-our-self-defense-game/) of “[Obfuscation: A User’s Guide for Privacy and Protest](https://mitpress.mit.edu/books/obfuscation)” by Helen Nissenbaum, Finn Brunton (N&B, henceforth) misses much of the point and proposes some pretty bad “solutions”.

Selinger starts his review by diminishing the value of privacy. I offer no defenses of privacy in this post and keep myself to his review and proposals.

Selinger accurately describes “Obfuscation \[as\] _the deliberate addition of ambiguous, confusing, or misleading information to interfere with surveillance and data collection_.” (italics in original).

N&B’s obfuscation goals, as I see them, are to make it harder for companies to differentiate between what we’re actually searching for ([TrackMeNot](https://cs.nyu.edu/trackmenot/)) and hit the advertising companies where it hurts by transparently clicking on _all_ served ads ([AdNauseum](https://dhowe.github.io/AdNauseam/)). As John Lancaster [points out](https://www.lrb.co.uk/v39/n16/john-lanchester/you-are-the-product), in “the internet-age dictum that if the product is free, you are the product” and its “customers aren’t the people who are on the site: its customers are the advertisers who use \[the\] network and who relish \[the\] ability to direct ads to receptive audiences”. If the costs of incessant tracking can be increased to an extent where companies are forced to (a) expend more resources to counter these obfuscation measures or (b) find a different business model then the approach can be described as a success.

Selinger’s biggest objection to this approach appears to be “the ethical question of whether it’s really okay for us to defend ourselves by polluting corporate data pools”. Again, like the privacy argument, I won’t defend the ethics (which seem perfectly legitimate to me) except to point out that, at this time, the two companies under question — Google and Facebook — have a combined market cap of $1 trillion and a combined market share of 90% of all online advertising.

N&B, by concentrating on Obfuscation primarily are in pretty good company. Linus Torvalds, maintainer of the Linux kernel — which runs on most computer servers and all Android phones — is fully supportive of “security through obscurity” as a legitimate [approach to security](https://marc.info/?l=linux-kernel&m=110559199830771&w=2) (though not the _only_ approach, of course). His comments were made in context of computer security but I don’t see N&B’s goals as fundamentally different — they’re arguing for ordinary people to defend themselves from the privacy invasions of mega-corporations.

The next objection Selinger has is that obfuscation “isn’t the only way to enhance privacy” and “our collective concern about proprietary platforms” must extend further. With this I agree but I don’t see why N&B can’t focus on a tiny domain while also working on a larger goal.

Finally, Selinger cites his [own work](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2439866) with Woodrow Hartzog, [Professor of Law and Computer Science](http://https//www.northeastern.edu/law/faculty/directory/hartzog.html) and where the bulk of my objections begin.

His suggestions are:

> sharing ideas on platforms that are invisible to search engines \[1\]; using privacy settings and other access controls \[2\]; withholding your real name and speaking anonymously or identifying yourself with a pseudonym \[3\]; disclosing information in coded ways that only a limited audience will grasp \[4\]; or transmitting content that is encrypted or temporarily accessible through an ephemeral conduit \[5\] \[My labelling.\]

Each of these is either poor advice or impractical or irrelevant. While all the tips address (to a poor degree, imo, details below) social networking they don’t touch upon avoiding tracking while _searching_. Ostensibly, tips \[2\] and \[3\] do but their practicality in 2017 is limited.

> sharing ideas on platforms that are invisible to search engines

These might have been relevant once upon a time but in the era of Facebook this cannot work. Any and all social groups are on Facebook. While Facebook serves as an effective walled-garden from Google, it too is a big surveillance player. (In fact, [Lancaster](https://www.lrb.co.uk/v39/n16/john-lanchester/you-are-the-product) describes Facebook as “the biggest surveillance-based enterprise in the history of mankind”.)

> using privacy settings and other access controls

Another great idea on paper but practically impossible. Most websites make extensive use of JavaScript loaded from other websites, use 3rd party Cookies. Additionally, most websites ignore browser Do Not Track [settings](https://en.wikipedia.org/wiki/Do_Not_Track#Effectiveness).

> disclosing information in coded ways that only a limited audience will grasp

Of all the ideas suggested, this is the most impractical. Establishing secrets is a ridiculously difficult problem. It’s the reason cryptographic committees and standards exist. The best an ad hoc, untrained group can do is to perhaps replace some words with others, say, using “p45” when they mean “Donald Trump” or coming to an understanding to use “ladle” when they mean “gun”. For the most part, it’s hard to communicate and the cognitive burden of remembering the terms becomes computationally intractable as both groups grow and the number of words increase.

For an in-group network to reliably form associations that cannot be broken, they must know each other well in person and it must be a tiny group.

Neither of these approaches are practical for large scale social networking where the goal is merely to do the most banal things of life.

> withholding your real name and speaking anonymously or identifying yourself with a pseudonym

Both Google and Facebook purchase information about us from private data brokers (see Lancaster, above). It was recently revealed that [Google tracks even our offline purchases](http://www.slate.com/blogs/future_tense/2017/08/01/google_tracks_people_offline_to_see_if_online_ads_work.html). For a long time Facebook did not allow users to join it unless [they used](https://www.wired.com/2015/06/facebook-real-name-policy-problems/) their [real name](https://www.theguardian.com/us-news/2015/dec/15/facebook-change-controversial-real-name-policy). The policy has been [slightly amended](https://www.facebook.com/help/112146705538576) but in a limited manner and only much after Facebook has gathered a lot of data about most people.

**Google powers an enormous part of the Internet**. Leaving aside search, GMail, Maps, or YouTube; for any website you open the chances are that you’re downloading some content from Google — via cookies or some web resource hosted through [Google’s CDN](https://cloud.google.com/cdn/). Google provides web hosting and sells domain names. Opening a website? If Google provided the domain, it’s probably going to know. Google provides [Google DNS](https://dns.google.com/) for “free”. Anyone that uses it now lets Google know all websites they’re requesting. Then there’s [Google Cloud](https://cloud.google.com/). Note that this doesn’t include the ever present Google Ads.

> transmitting content that is encrypted or temporarily accessible through an ephemeral conduit

These are the problems that Messaging apps such as [WhatsApp](https://whatsapp.com/), [Signal](https://signal.org/), and [Telegram](https://telegram.org/), among others aim to solve. But they have no utility beyond communication. The purpose of Google Search is to find things. There’s no better software than the Google search bar to find information across the most general domains. N&B’s book is a means to counter what they (and many others, myself included) see as illegitimate tracking that occurs in return for the service of providing search results.
