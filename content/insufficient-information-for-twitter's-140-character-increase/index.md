---
title: "Insufficient information for Twitter’s 140 character increase"
description: "Twitter’s proposal to double their character limits for many languages isn’t sufficiently justified."
date: "2017-09-30T20:34:16.771Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/twitter-140-characters-25954305960e
redirect_from:
  - /twitter-140-characters-25954305960e
---

Twitter [recently announced](https://blog.twitter.com/official/en_us/topics/product/2017/Giving-you-more-characters-to-express-yourself.html) that they were “going to try out a longer limit, 280 characters, in \[all\] languages… (except Japanese, Chinese, and Korean).”

In this post I question Twitter’s reasoning on methodological and philosophical grounds. I conclude with what, in my opinion, ought to have been their focus.

#### Philosophical Grounds

Justifying their rationale, Product Manager, Aliza Rosen, says they looked at data of people using Twitter around the world and came to the conclusion that “the character limit is a major cause of frustration for people Tweeting in English, but it is not for those Tweeting in Japanese” \[my emphasis\]. Her following sentence indicates — in my opinion — Twitter’s true intent that there are more tweets “when people… have some \[characters\] to spare”.

There a few things at play here. What does Twitter mean by frustration and how do they infer “the character limit is a major cause of frustration”.

As far as frustration goes, we must keep in mind Twitter isn’t a neutral party and they have a vested interest in people staying on their platform. For instance, if Twitter found its users were more frustrated than the remaining populace but this frustration tended to keep them on Twitter it’s unlikely Twitter would describe it as a bad thing. \[[1](https://www.forbes.com/sites/amitchowdhry/2016/04/30/study-links-heavy-facebook-and-social-media-usage-to-depression/#51da47334b53)\] Hence, Twitter must define “frustration” as people who decide to leave Twitter, not what people actually feel.

Regarding how they know about people ceasing to tweet, my guess is that the Twitter website and mobile apps track when people cancel a tweet or fail to send a tweet and noticed that this is highly correlated with times when the number of characters reach 140. They see this as bad only because of their narrow construal of “frustration” as abandoning the platform. Many places impose strong constraints on what people may submit — no porn (Facebook, Instagram), relevance (NYT comments). These constraints force one to rethink or rephrase and thus they shouldn’t be rejected solely on the basis of _engagement._

#### Methodological Grounds

In justifying Twitter’s decision, Rosen and Ihara share a [graph](https://blog.twitter.com/content/dam/blog-twitter/official/en_us/products/2017/giving-you-more-characters-to-express-yourself/more-chars-1.png) which shows that while most tweets in Japanese have 15 characters, the corresponding number for English is 34. But this ignores cultural differences entirely. Unless we know how Twitter is used by Japanese tweeters raw numbers are not a fair comparison.

Also, why an increase of a 140 characters? Again, going by their graph, only 9% of all tweets exceed 140. To double the tweet character limit because 9% of users reached the limit seems… excessive.

Are the numbers right? The graph’s Y-axis isn’t labeled so we don’t (a) know how many tweets were actually made and if (b) the graph uses different Y-axes for English vs Japanese tweets. From the graph, I calculated the number of tweets — the area under the curve — and it gave almost the same number. I don’t have access to the numbers but I very seriously doubt that the number of tweets in English versus Japanese are the same. \[2\]

#### What could they have instead done?

Given that only 9% of all tweets are running into the limit, they could have increased the limit by a proportional amount. 160… perhaps. My own suspicion is that the problem isn’t the character limit. At this time, experienced users write well composed threads. All Twitter needed to do was to improve the interface to threading and make composing threads easier while also maintaining that 140 character limit.

#### My conspiracy theory

A possible factor behind their character limit that, as far as I know, hasn’t been discussed elsewhere is the emergence of gab.ai, a similar social network \[[3](https://www.wired.com/2016/09/gab-alt-rights-twitter-ultimate-filter-bubble/)\]. Gab offers a character limit of 300 and is growing fast according to [Wikipedia](https://en.wikipedia.org/wiki/Gab_%28social_network%29).

#### References

\[1\] See Amit Chowdhry, Forbes, Apr 30, 2016; [https://www.forbes.com/sites/amitchowdhry/2016/04/30/study-links-heavy-facebook-and-social-media-usage-to-depression/#51da47334b53](https://www.forbes.com/sites/amitchowdhry/2016/04/30/study-links-heavy-facebook-and-social-media-usage-to-depression/#51da47334b53)  
\[2\] I colored the graph from the blog (shown below) and counted the number of pixels in a particular color. The code to count colors is in: [https://gist.github.com/lvijay/0cdd7d7ee04e244b908fe0728299256e](https://gist.github.com/lvijay/0cdd7d7ee04e244b908fe0728299256e). The results were English: 161384 blue pixels and Japanese: 159948 red pixels. A ratio of 1.009.

undefinedEnglish on the left and Japanese on the right

\[3\] Emma Grey Ellis, WIRED, Sep 14, 2016; [https://www.wired.com/2016/09/gab-alt-rights-twitter-ultimate-filter-bubble/](https://www.wired.com/2016/09/gab-alt-rights-twitter-ultimate-filter-bubble/)
