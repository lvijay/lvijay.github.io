---
title: "Twitter and 280 characters, still unjustified"
description: "In a previous post I wrote how Twitter’s plan to increase the character limit to 280 for tweets in English and other languages was…"
date: "2017-11-12T23:50:07.612Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/twitter-and-280-characters-still-unjustified-8edad9e3b0dd
redirect_from:
  - /twitter-and-280-characters-still-unjustified-8edad9e3b0dd
---

From Twitter’s [Brand Guidelines](https://about.twitter.com/content/dam/about-twitter/company/brand-resources/en_us/Twitter_Brand_Guidelines_V2.0.pdf)

In a [previous post](https://medium.com/@lvijay/twitter-140-characters-25954305960e) I wrote how Twitter’s plan to increase the character limit to 280 for tweets in English and other languages was unjustified. Since then, Twitter have increased the limit to 280 characters for all. They have a new [blog post](https://blog.twitter.com/official/en_us/topics/product/2017/tweetingmadeeasier.html) by the same author, Aliza Rosen, justifying the increase for all. It refers to [a post](https://blog.twitter.com/engineering/en_us/topics/insights/2017/Our-Discovery-of-Cramming.html) by her coauthor from the earlier post, Ikuhiro Ihara, which provides the data analysis behind their decision.

It’s been a week since everyone’s had 280 character tweets. I’m going to argue here that their decision is still unjustified, point out things they don’t appear to have considered, and ponder about the unforeseen consequences of their decision. Additionally, in the week since their increase, I’ve had time to absorb the consequences so I’ve realized some consequences that could’ve been inferred at the time earlier post but weren’t.

The argument’s going to be as follows, first, I consider something Twitter haven’t explained: why are Korean tweets shorter? Next, what they didn’t consider.

In their original post, they justified the need to increase on the basis of two factors (a) many English tweets hit the 140 limit and were subsequently abandoned and (b) the observation that this was not a problem for tweets in Korean.

(Quick note: In this post, any mention of “Korean” should be read as “Korean and/or Japanese and/or Chinese”. I do this for purely for brevity; I do not mean that they _are_ the same. Similarly, English can mostly be read as being English and other languages.)

Nowhere in their original post or later ones have they discussed why it’s the case that Korean and Japanese tweets don’t hit the limit so often. As I see it, there are two possibilities of which I think only the latter is valid.

1.  Languages like Japanese and Korean are genuinely more expressive than others and are hence able to express in fewer words what takes more words in English.
2.  The way we count characters in Korean is fundamentally different from how we count them in English.

I take it as a given that (1) is false. Sixty years of Chomskyan linguistics has taken pains to show that all languages are fundamentally the same, produced by our minds by a Language-Acquisition-Device organ in the brain. Even without discussing into linguistics, the proposition can be shown as false by simple logic: if it were true that Korean were twice (see below) as expressive as English, we would all be Korean speakers; just as, _all else being equal_, a faster computer processor would quickly replace a slower one.

Answering (2) is a little harder and one needs to get into the weeds of character representation to discuss it in detail. The disadvantage for me in this case is that I barely know the Unicode specification (consortium to represent all the world’s scripts in computers) and know absolutely no Korean. But I think we can proceed nevertheless. If anything, I believe it simplifies my analysis by keeping me from getting too detailed.

Computers count things in _byte_s. A byte is a pretty small chunk of memory. As an illustration, consider this: being able to type every key on a standard American Keyboard would take about [half](http://www.asciitable.com/) of what a single byte can represent. This is nowhere near enough for representing every script out there.

Luckily for me, Twitter [explain](https://developer.twitter.com/en/docs/basics/counting-characters) that their goal is to count characters as they appear to “the human eye”. Thus, while it takes more than one byte for a computer to represent “é” — it’s “e” + “´” — Twitter only count the combination as one character.

**Ligatures and Digraphs to the rescue  
**Actually, we can do better than merely counting “café” as four instead of five thanks to ligatures and digraphs in the Unicode spec.

([Ligatures and Digraphs](http://www.unicode.org/faq/ligature_digraph.html#Lig1) are magic sauce used by typesetters thanks to whom some fonts are more readable than others. `Otherwise, all writing would be monospaced like this.`)

Some characters that appear to us as two individual letters are actually only one character. A few examples are “fl” and “ﬂ”, and “fi” and “ﬁ”. In both the former counts as two characters but the latter counts as only one. They look the exact same in Medium’s font, so allow me to repeat them, but this time in monospace — `compare "fl" and "ﬂ", and "fi" and "ﬁ"`. Other, more visceral examples include “ae” and “æ”, and “oe”/“œ”. See the appendix for more interesting examples.

It’s my thesis that this singular counting is what happens in Korean but at a larger scale. I’m happy to get feedback from Korean/Japanese/Chinese speakers — confirming or correcting.

**Non Technical Proof**  
As a non technical proof, consider the image from Twitter’s first blog post (shown below). It shows that while the same sentence in English takes 140 characters, it only takes half as many characters, 67, in Japanese.

undefined

As you can see, visually, they even occupy the same vertical space, you see the same punctuation marks (located differently because both languages use different grammatical ordering).

### What they didn’t consider

#### Hume wags his finger

My problem is that they run into the problem of “deriving ought from is”, as described first by David Hume in his 1757 work, “An Enquiry Concerning Human Understanding”. While it might be true that many English tweeters run into the 140 character limit and some portion of them then abandon the tweet, it has yet to be shown that this is a bad thing. As the comedian, Aparna Nancheria, so [wonderfully put it](https://www.nytimes.com/2017/09/28/opinion/twitter-280-characters.html), “\[b\]ut the reason so many of us loved \[twitter\] was that it was, from its inception, a celebration of something people on the internet generally do very poorly: self-editing.”

The writer Mike Monteiro too, for instance, [attributes to Twitter](https://medium.com/@monteiro/one-persons-history-of-twitter-from-beginning-to-end-5b41abed6c20) his becoming a better writer, going so far as to say that if he “thought a sentence was pretty good \[he\] pasted it into the Twitter text field to make sure it was 140 characters.”

I’m yet to see a single justification for limits as a bad thing. I covered this in my [earlier post](https://medium.com/@lvijay/twitter-140-characters-25954305960e), so I won’t discuss it more.

#### Unforeseen Consequences

In the last week of 280 character tweets, my timeline is flooded with overly long tweets. It’s become so that where I used to read all the tweets in my timeline I now actively skim past the long ones. I don’t believe I’m the only one. Where twitter earlier justified their action on the basis that this would increase engagement, it’s entirely likely the inverse will happen. I’m certainly less engaged.

#### Whither user inputs?

Curiously missing from Twitter’s discussions are inputs from users. There’s extended [discussion](https://blog.twitter.com/engineering/en_us/topics/insights/2017/Experimenting-To-Solve-Cramming.html) of their A/B testing techniques but none discussing inputs from users. Rosen mentions users twice in her post “\[p\]eople in the experiment told us” and that they are increasing the limit “after listening \[to a\] problem our global community was having”.

Two things here, it’s curious that these user inputs don’t deserve their own blog posts and the Henry Ford maxim: “If I had asked people what they wanted, they would have said faster horses.” That some percentage of users felt the need for an increase does not necessarily imply they must be abided by. There’s no discussion of inputs from people who felt the move was unjustified.

#### Usability?

undefined

The vertical space occupied by tweets now has made twitter close to unusable. (On the up side, I spend more time doing other things.) This was evident from the image in their first post (shown on the left) but I never realized it myself. Consider that the image on the left shows four tweets but the one on the right shows only 3. The illustration is slightly artificial because most users probably don’t have Japanese tweets on their timeline and even if they did, most Korean tweets _aren’t_ that long (see their first post). So in the ideal case, we’re talking about a simple phone screen moving from showing 5 tweets to now showing a mere 3. I fail to see how this will drive to the only thing Twitter cares about: **more engagement**.

The funny part is Twitter could’ve easily found this out by asking their Korean users how they felt about tweets that occupied so much space. But, as Molly Rogers’s [insightful article](https://www.washingtonpost.com/blogs/post-partisan/wp/2017/11/09/twitter-verifies-a-neo-nazi-and-blames-everyone-else/) on a different topic points out, user inputs don’t appear to feature high on Twitter’s list of priorities.

#### Equally valid

An equally forceful conclusion that can be drawn from all of Twitter’s studies is had they reduced the character limit of Korean users to 70 characters, the Koreans would exhibit the exact same behavioral patterns as other language users. As far as I can tell, they never once considered this. Given that (a) the fraction of users impacted would be minuscule and (b) most of them probably would not have objected seems to me a simpler approach to first try.

### Conclusion

Where this will take Twitter, I do not know. The platform has more problems than just the character limit.

I miss the days of 140 characters already.

#### Appendix

The following are a short list of ligatures I found in the time I was willing to spend on this post. They’re shown along with their Unicode name.

LATIN SMALL LETTER AA (ꜳ)  
LATIN SMALL LETTER AE (æ)  
LATIN SMALL LETTER AO (ꜵ)  
LATIN SMALL LETTER AV (ꜹ)  
LATIN SMALL LETTER AY (ꜽ)  
LATIN SMALL LETTER LJ (ǉ)  
LATIN SMALL LETTER NJ (ǌ)  
LATIN SMALL LETTER OO (ꝏ)  
LATIN SMALL LETTER UE (ᵫ)  
LATIN SMALL LETTER VY (ꝡ)  
LATIN SMALL LIGATURE FF (ﬀ)  
LATIN SMALL LIGATURE FFI (ﬃ)  
LATIN SMALL LIGATURE FFL (ﬄ)  
LATIN SMALL LIGATURE FI (ﬁ)  
LATIN SMALL LIGATURE FL (ﬂ)  
LATIN SMALL LIGATURE IJ (ĳ)  
LATIN SMALL LIGATURE LONG S T (ﬅ)  
LATIN SMALL LIGATURE OE (œ)  
LATIN SMALL LIGATURE ST (ﬆ)  
LATIN SMALL LETTER DB DIGRAPH (ȸ)  
LATIN SMALL LETTER DZ DIGRAPH (ʣ)  
LATIN SMALL LETTER LS DIGRAPH (ʪ)  
LATIN SMALL LETTER LZ DIGRAPH (ʫ)  
LATIN SMALL LETTER QP DIGRAPH (ȹ)  
LATIN SMALL LETTER TS DIGRAPH (ʦ)

It would be an interesting exercise to rewrite a given word into the best combination of ligatures/digraphs such that the word appears to be the same but uses fewer characters. For instance, it would rewrite “stiffly” as “ﬆiﬄy” (`st + i + ﬄ + y`, saving 3 characters) or “coeffluent” as “cœﬄᵫnt” (`c + œ + ﬄ + ᵫ + nt`, saving 4).

Another avenue for innovation now killed by Twitter.
