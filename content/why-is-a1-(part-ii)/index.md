---
title: "Why is a⁰=1? (Part II)"
description: "In which I attempt to compute the logarithms to greater degrees of accuracy."
date: "2018-06-03T10:56:16.334Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/logarithms-continued-dc8c5dfd7760
redirect_from:
  - /logarithms-continued-dc8c5dfd7760
---

undefined

In an earlier post¹ I discussed a way to understand logarithms by folding paper. I failed to explain how to compute them when the values don’t neatly fold up to integer values. In this post, I do. Unlike the previous post this one has no animated GIFs. Some might see that alone as an improvement.

The solution, as always, is to work backwards. I already know the answer to the question of `log₅250`: it’s approximately `3.43067655807339306`. ² So let’s work towards it. Repeated division in the previous post got us upto 3 but left us stuck with a remainder of 2. (3 steps gives us: 250÷5=50; 50÷5=10; 10÷5=2). Here, we’re going to find a way to get from log₅2 to 0.43067….

What happens if we do 2÷5? Answer: 0.4. This looks curiously close to our expected answer (0.4306…). Promising. How do we get the remaining 0.03067…? Unfortunately, 2÷5 is exactly 0.4 so doesn’t give us fractional problems that we can stress over.

What’s 5⁰˙̇⁴? Answer: 1.9036539387158786. We started with 2 and we’re now at 1.904. Which means our answer’s missing 0.097 (Since 2–1.903 = 0.097.) Dividing this by 5 gives us 0.019. Let’s add the first answer and this one. We have 0.419. We have the glimmers of a procedural method to arrive at logs, let’s follow where it leads.

Repeating the above steps in the programming language, Python:

```
start = 2       ## the value we have
base = 5        ## the logarithm base
result = 0      ## where we'll store the answer
test = 0        ## where we'll see how far off the mark we are
missing = start ## how far off from start is test?
                ## initially, it's off by 2.  we want to make it 0

result  = result + missing / base  ## answer: 0.4
test    = base ** result           ## answer: 1.903653938715878
missing = start - test             ## answer: 0.096346061284121

result  = result + missing / base  ## answer: 0.419269212256824
test    = base ** result           ## answer: 1.963616185080452
missing = start - test             ## answer: 0.036383814919547

result  = result + missing / base  ## answer: 0.426545975240734
test    = base ** result           ## answer: 1.986748263800719
missing = start - test             ## answer: 0.013251736199280

...
```

Continually repeating the last 3 steps gets us closer to the value of log₅2. Here’s what continuing above gives us:

```
result   test     missing
0.000000 0.000000 2.000000
0.400000 1.903654 0.096346
0.419269 1.963616 0.036384
0.426546 1.986748 0.013252
0.429196 1.995241 0.004759
0.430148 1.998300 0.001700
0.430488 1.999394 0.000606
0.430609 1.999784 0.000216
0.430653 1.999923 0.000077
0.430668 1.999973 0.000027
0.430674 1.999990 0.000010
0.430675 1.999997 0.000003
0.430676 1.999999 0.000001
```

Glad that’s settled.

#### Footnotes

¹ “Why is a⁰=1?” published May 13, 2018, available at [https://medium.com/galileo-onwards/why-is-a-raised-to-zero-one-64966392efbe](https://medium.com/galileo-onwards/why-is-a-raised-to-zero-one-64966392efbe).
