---
title: "Google and the failures of ‘Enormous Data’"
description: "Wired has an article describing the failures of Google’s ‘Enormous Data’ [2]. Though it isn’t described as a failure, that’s how it should…"
date: "2017-07-17T22:22:57.589Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/google-and-the-failures-of-enormous-data-85cc89e0f18a
redirect_from:
  - /google-and-the-failures-of-enormous-data-85cc89e0f18a
---

Here’s a gorilla, not a black person \[1\]

Wired has an [article](https://www.wired.com/story/ai-and-enormous-data-could-make-tech-giants-harder-to-topple/) describing the failures of Google’s ‘Enormous Data’ \[2\]. Though it isn’t described as a failure, that’s how it should be.

Google, in an “expensive collaboration with Carnegie Mellon University” ran its image recognition Machine Learning algorithms on

> 50 powerful graphics processors for two solid months, and used an unprecedentedly huge collection of 300 million **_labeled_** images… to test whether it’s possible to get more accurate image recognition _not by tweaking_… existing algorithms but just by feeding them much, much more data. \[my emphasis\]

The answer to their test was: no. WIRED claims the answer was yes but reading through the article, it says

> Crunching Google’s giant dataset of 300 million images **_didn’t produce a huge benefit_** — jumping from 1 million to 300 million images increased the object detection score achieved by **_just 3 percentage points_**. \[emphases mine\]

I elaborate more about these 3pp numbers below but first, a look at some costs.

---

### The Numbars game: How much did this cost?

Let’s assume that each analyzed images was 300kb. The space requirements for 300M images then becomes 83 _peta_bytes (1 Petabyte is 1024 Gb).

Using a 2013 estimate by Dutta et al. \[3\], the cost per byte at a datacenter is 71K picocents, i.e. Google’s “experiment” cost $6.5M. This was 4 years ago and these costs keep falling.

Running a similar estimate against Amazon’s [AWS Calculator](http://calculator.s3.amazonaws.com/index.html) \[4\], gives a monthly estimate of $2.25M \[5\]. Since it’s lower, let’s go with this. The cost for 2 months comes to $4.5M. As Google owns the cluster, let’s assume it cost Google **four million dollars**. (See references section for details.) Note also that Google intends to run these tests often and this is the cost each time they run a test. If they use more data, it’ll be more expensive.

Remember, the cost involved with this “experiment” was more than just the hardware costs. Google pays the salaries of several data scientists and engineers for this task. Since it was done in collaboration with CMU, we can assume they worked with at least one tenured professor and several minimum wage slaves (aka grad students). I leave it to the reader to speculate what Google pays expert Data Scientists and Computer programmers. (Google it ;-)

Furthermore, recall that Google used “300 million **_labeled_** images” in its analysis. That labeling was done by humans. There’s a cost involved there too though I doubt it was one Google paid for. For instance, the [Google Image Labeler](https://googlesystem.blogspot.in/2006/09/google-image-labeler.html) was a means to “help Google improve Google Image Search by tagging images” and, because they had our best interests at heart, they “transformed this boring activity into a nice interactive game”. The original game was online from 2006–2011 and was relaunched in 2016. This is one of the dirty secrets of all Machine Learning systems — much of the data is acquired and inputted by humans. \[7\]

Instead of these complicated “algorithmic” solutions, what would happen if Google just hired workers to label images and paid them $15/hour? According to \[7\], the cost to a company for paying someone $15/hour comes to $62,000/year. Which means that instead of blowing $4,000,000 on this single “experiment,” Google could have just hired 60 employees to identify their images. Their image identifying system would not be Real-Time but it would certainly function with an accuracy close to 90% (definitely higher than present). And you certainly won’t have humans identified as gorillas \[1\]. If you’re a consultant you could sell this as a product to companies, charge them top dollar, boast a high accuracy; run a decent shop behind the scenes and you’ll still beat the richest software company ever. (Remember, that $4 million figure does not include untold millions in salaries Google pays its engineers, their managers, and _their_ managers…. Factoring that in means you even have money to give yourself a big bonus.)

---

### What could a 3pp improvement mean?

Holding to the assumption that any group that wishes to advertise will use the number that projects it in a positive light, we can try to reverse engineer what a 3 percentage point improvement means.

For instance, if the original accuracy percentage were 1% and it improved to 4%, the results would have been touted as a 300% improvement in performance. Given that that wasn’t how it was advertised, we can safely assume this isn’t what happened. Supposing it went from 50% to 53%, that’s a 6% performance improvement.

One can continue this and speculate what the actual numbers were but this hopefully gives a flavor.

### Conclusion

At what point will Google see that their Image Recognition is useless and throw it all away? Does it even make sense to run such an expensive operation?

I’ll leave that to the shareholders.

### A quick note about the gorilla image

Medium insisted that I have an image when sharing this post. Given that this post is about Google’s image recognition, I thought it apropos to have a picture of a gorilla, because, back in 2015, [Google Photos](http://www.telegraph.co.uk/technology/google/11710136/Google-Photos-assigns-gorilla-tag-to-photos-of-black-people.html) famously identified black people as gorillas. \[1\]

### References

\[1\] Sophie Curtis, “Google Photos labels black people as ‘gorillas’”, Telegraph, Jul 01 2015, accessed at [http://www.telegraph.co.uk/technology/google/11710136/Google-Photos-assigns-gorilla-tag-to-photos-of-black-people.html](http://www.telegraph.co.uk/technology/google/11710136/Google-Photos-assigns-gorilla-tag-to-photos-of-black-people.html). The Gorilla photo was taken from Wikipedia, a photo by Brocken Inaglory, accessed at [https://commons.wikimedia.org/wiki/File:Male\_gorilla\_in\_SF\_zoo.jpg](https://commons.wikimedia.org/wiki/File:Male_gorilla_in_SF_zoo.jpg)  
\[2\] “AI and ‘Enormous Data’ Could Make Tech Giants Harder to Topple”, by Tom Simonite, Jul 13, 2017, [https://www.wired.com/story/ai-and-enormous-data-could-make-tech-giants-harder-to-topple/](https://www.wired.com/story/ai-and-enormous-data-could-make-tech-giants-harder-to-topple/)  
\[3\] “How Much Does Storage Really Cost?” — Amit Kumar Dutta and Ragib Hasan, accessed at [https://www.bja.gov/bwc/pdfs/dutta-2013-full-cost-accounting-gecon.pdf](https://www.bja.gov/bwc/pdfs/dutta-2013-full-cost-accounting-gecon.pdf)  
\[4\] AWS Simple Monthly Calculator, [http://calculator.s3.amazonaws.com/index.html](http://calculator.s3.amazonaws.com/index.html)  
\[5\] I’m no AWS Expert but here are the parameters I put in. Estimates are on top of the image.

50 of their best computers with 90Pb storageline item specification of costs

\[6\] Info on the Google Image Labeler from the unofficial Google News blog, [https://googlesystem.blogspot.in/2006/09/google-image-labeler.html](https://googlesystem.blogspot.in/2006/09/google-image-labeler.html) and for adding tags to a Google Photos image, see, for eg, [https://productforums.google.com/forum/#!topic/photos/KyzzpfxYHoc](https://productforums.google.com/forum/#!topic/photos/KyzzpfxYHoc). As of 2016, the Google Image Labeler has a new home at [http://crowdsource.google.com/imagelabeler](http://crowdsource.google.com/imagelabeler).  
\[7\] Real Cost of an Employee at [https://www.toptal.com/freelance/don-t-be-fooled-the-real-cost-of-employees-and-consultants](https://www.toptal.com/freelance/don-t-be-fooled-the-real-cost-of-employees-and-consultants) I found this with quick search for “Cost of an employee”. I have no idea how reliable it is but I’m betting it can’t be off by more than 2x.

undefined
