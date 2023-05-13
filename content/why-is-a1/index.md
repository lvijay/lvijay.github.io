---
title: "Why is a⁰=1?"
description: "Folding paper helps explain logarithms and why any number raised to the zeroth power is one."
date: "2018-05-13T03:45:13.338Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/why-is-a-raised-to-zero-one-64966392efbe
redirect_from:
  - /why-is-a-raised-to-zero-one-64966392efbe
---

undefined

By “any number”, I mean any _positive_ number. I do not consider zero or negative numbers.

Also, do not try this game with real paper. As an article in Gizmodo points out, folding a paper in half just 7 times is approximately as thick as a 128 page notebook. ¹

#### The Game

In the game, we pick two numbers, _a_ and _b_. We take a strip of paper that’s exactly _a_ units long. Then we fold this strip into _b_ equal sized portions. We continue until the strip is exactly 1 unit long. The goal of our game is to find out how many times we must fold the strip to bring it down to exactly 1 unit.

The nice thing about our paper is that it folds perfectly, has zero width, and a consequence of having zero width is that how many ever times you fold it, it remains at zero width.

**Example 1  
**For our first example, we’ll pick two small numbers: 4, 2. More complicated examples follow.

We take our paper that’s 4 units long as shown below.

undefined

We divide it into 2 equal parts as below.

undefined

We fold the 2 parts to 1 section and measure how many units we have left. (Note: since I lack the artistic skills to animate a strip being folded, you’ll have to settle for the strip being grayed out.) If you _are_ doing this with real paper, you could also tear out the divided portion. The results will be the same.

undefined

We are left with a strip that now is 2 units long. We divide by two what remains.

undefined

We again fade what remains.

undefined

And we are left with a strip exactly one segment long.

We ran this operation twice so our answer’s 2.

**Example 2**  
Let’s pick something slightly more elaborate but still relatively simple. Let’s take 27 and 3. This time, I show the entire animation in a single image.

undefined

As you can see, we divided and faded the strip 3 times so the answer is 3.

#### What’s going on?

The answer we get playing this game is the same as the logarithm of a number. Given any two numbers, _b_ and _x_, the game gives us the answer to _logₓb_ (read as log b to the base x). Logarithms can also be defined thusly:

If _logₓb=a_ then _xª=b_.

Looking again at the above examples gives us:

_log₂4=2_ and _2²=4_;  
_log₃27=3_ and _3³=27_.

This works consistently. For example, _15¹=15_, and dividing a 15 unit long paper into 15 units and bringing them down to 1 unit will take us exactly 1 step.

undefined

**Why is a⁰=1?  
**At this point it should be obvious that if you start with a piece of paper that’s exactly _1_ unit long, it’ll take you exactly _0_ steps to reach 1.

For example, below we start with an image that’s 1 segment long:

undefined

We start with 1 intending to reach 1 and, hey, it’s exactly what we wanted so we declare victory. Case closed.

#### There are more numbers than just integers

Of course, even with perfect paper, things don’t always divide perfectly.

Let’s again look at two examples below.

**_log₂12_**

undefined

As you can see, we made 3 folds, went down to _almost_ 1 but there’s a remainder (of 0.5 units).

Clearly, _log₂12_ is at least _3_. But how much is it? We started with 12. Came down to 6. Then went to 3, then 1.5 and stopped. How do we bring 1.5 down to 1 by only folding in halves?

**_log₇21_**

undefined

log₇21 is approximately 1. We make one fold and we have 3 units left. But we have no means to divide the remainder into seven equal parts to reach 1 because the individual segments will themselves be less than 1. How do we bring 3 down to 1 by only folding in sevens?

Like the mathematician who dropped his keys but searched elsewhere — under a lamppost — because “that’s where the light is” ², I, not knowing how to bring 1.5 to 1, too shall change the problem to one that can be easily solved.

#### Numbers less than 1

Suppose we somehow come across a strip of our paper that’s 0.5 units long and we wish to make this strip 1 unit long. We choose the base of our logarithms as 2. Since, we cannot further fold this strip to arrive at 1, we pull the classic mathematician’s trick: we’ll do the inverse and call it a negative number: we’ll _un_fold the paper by our log base (2, in this case), until we reach 1. And we’ll count backwards for each unfolding step we take. In this case, the answer is –_1_. I don’t show the image because prettier examples follow.

#### **log_₂_0.015625**

Here’s another example, this time with graphical representation. We start with a strip that’s _0.015625_ units long which we wish to keep unfolding until we reach 1. In the below animation, we start with a red strip and each unfolding shows us a green strip. The number of different greens is also our answer. As a guide, the unit values are also drawn.

undefined

Six different greens gives us the answer as _–6_.

#### log₅0.008 = –3

undefined

#### log₃0.012345679 = –4

undefined

The reason the above 3 examples work is easily expressed via fractions. The first one, _0.015625_, is 1/64 which is 1/2⁶. The second, 0.008, is 1/125, i.e. 1/5³, and the last is 1/3⁴.

#### log0 = –∞

This unfolding technique also explains why _log_0 is _\-∞_. The thinner the strip with which we begin, the more _un_folds we must perform to reach 1. With 0 we’d have to fold it infinite times to reach 1 and, since we’re counting backwards, the answer follows naturally.

It’s also for the same reason that negative numbers do not have a logarithm. No amount of folding or unfolding will take them to 1.

(Of course, there’s the matter of taking logarithms of negative numbers using negative bases but I don’t want to go there.)

#### log₂0.012345679 = –6.??

Of course, unfolding isn’t perfect either. We can unfold _log₂0.012345679_ _6_ times which takes us all the way to _0.79…_ but we cannot account for the remaining _0.21…_.

undefined

As earlier, I don’t have a simple means to explain why _log_₂ of the above number is _–6.33985_.

I’ll end here.

#### Footnotes

¹ Link to article: [https://sploid.gizmodo.com/if-you-fold-a-paper-in-half-103-times-it-will-be-as-thi-1607632639](https://sploid.gizmodo.com/if-you-fold-a-paper-in-half-103-times-it-will-be-as-thi-1607632639). The numbers are not a coincidence, of course. Folding a paper in half seven times is the same as having 128 pages since 2⁷=128. (In reality it’ll actually be thicker still because the paper won’t fold perfectly.)

² The full joke runs as follows:

> One night, a mathematician parks his car, locks it with his key and walks away. After walking about 50 yards the mathematician realizes that he has dropped his key somewhere along the way. He walks to the other end of the parking lot where there is better light and looks for his key there.

**Featured Image source**: [https://commons.wikimedia.org/wiki/File:Fortuneteller\_mgx.svg](https://commons.wikimedia.org/wiki/File:Fortuneteller_mgx.svg). Public Domain.

The code used to generate these GIF animations is available at: [https://gist.github.com/lvijay/7039c3db5cd237eb6a01971813661a5b](https://gist.github.com/lvijay/7039c3db5cd237eb6a01971813661a5b).
