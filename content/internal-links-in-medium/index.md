---
title: "Internal links in Medium"
description: "Medium doesn’t allow readers to link to sections within articles. Can I hack it?"
date: "2019-08-24T16:42:11.033Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/linking-to-medium-post-sub-sections-b64215da04e5
redirect_from:
  - /linking-to-medium-post-sub-sections-b64215da04e5
---

[Medium](https://medium.com/u/504c7870fdb6) doesn’t allow readers to link to sections _within_ articles. As an occasional writer, I find this restriction annoying to me and this article then becomes an exploration (a _hack_¹, if you will) of ways to circumvent the website’s constraints.

**Quick note:** this post assumes the reader knows HTML. Unlike most of my other posts, there will be no explication.

#### tl;dr

The long and short summary, as best as I can tell, is that you can link to sections and subsections (even paragraphs) within a single post but not to another medium post itself.

### How

Every paragraph in a Medium post is has an `id` attribute. Using this we can reference any specific paragraph by suffixing the URL with a `#` followed by the `id` attribute.

Consider an example, below is a screenshot from a post I wrote supporting [Dean Baker](https://medium.com/u/278449ec382a)’s calls to bring Free Trade laws for doctors and dentists. In today’s America, American Software Engineers are subject to competition from foreign software engineers; but doctors and dentists are protected by a cartel² (literally, see footnote). In my post, drew parallels between his theory and the rise of India’s Software Engineers. In India’s case, the government introduced several software engineering colleges _for_ the explicit purpose of exporting them to the US and setup service companies. The consequence of the Indian government’s actions in the 90s is today’s software industry. The upshot is that both the American and Indian government have benefitted from Free Markets.

I digress. Here’s the screenshot.

A screenshot of a paragraph (highlighted in blue with a red box around it) and an arrow pointing to its id attribute. The id is 1ba0. Copying the following url and pasting it in your browser will take you straight to the highlighted paragraph. Clicking on it won’t work for reasons discussed below. https://medium.com/galileo-onwards/deans-doctors-47bb7c1d8f65#1ba0.

Copy/pasting the link https://medium.com/galileo-onwards/deans-doctors-47bb7c1d8f65#1ba0 into your favorite browser will take you to the highlighted paragraph. Clicking on the link itself won’t work because Medium removes the trailing `#1ba0` from the href. (See footnote 3 for an explanation of why.)

Links to sections within a post will work though. Just find the `id` under question and mark the href as just, literally, `#` followed by the id. Example, (naturally), in this article, the Footnotes section has `id` equal to `05f2`. Using this, I can link to the Footnotes with the link as [#05f2](#05f2).

During the course of editing, the id is instead listed under the `name` attribute. I don’t know why.

Happy hacking.

### Footnotes

¹ I use the word _hacker_ in its original sense, not in the sense of people who break into software systems. As Richard Stallman, founder of the [Free Software Foundation](https://stallman.org/articles/on-hacking.html), puts it: “Playfully doing something difficult, whether useful or not, that is hacking.” He has a good post that describes the meaning of hacking and several examples. See [https://stallman.org/articles/on-hacking.html](https://stallman.org/articles/on-hacking.html).

² A link to Dean Baker’s 2017 article in [Politico](https://www.politico.com/agenda/story/2017/10/25/doctors-salaries-pay-disparities-000557): [https://www.politico.com/agenda/story/2017/10/25/doctors-salaries-pay-disparities-000557](https://www.politico.com/agenda/story/2017/10/25/doctors-salaries-pay-disparities-000557).

³ Medium include something called a _canonical link_ in all their posts. They do this so the posts of medium authors are better ranked by Search Engines (like Google, Bing). For details see [https://help.medium.com/hc/en-us/articles/217991468-About-SEO-and-duplicate-content](https://help.medium.com/hc/en-us/articles/217991468-About-SEO-and-duplicate-content).
