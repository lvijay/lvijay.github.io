---
title: "The Machine Learning of Simple Things"
description: "Seeking basic examples to show the effectiveness of Machine Learning"
date: "2018-01-05T15:42:12.755Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/the-machine-learning-of-simple-things-e6bca6d5283f
redirect_from:
  - /the-machine-learning-of-simple-things-e6bca6d5283f
---

undefined

Machine Learning is all the rage these days and it’s impossible to not run into something or the other that’s supposedly being done well by Machine Learning. Personally, I’m categorically opposed to it. I discussed this (albeit obliquely) in a previous post. ¹

That said, it is a field whose progress I follow and take an interest in, at least as far as reading about it but not so much in its practice — of which there’s very little.

The most curious aspect that I’ve noticed of Machine Learning is that there are no simple examples.

#### Surveying the landscape (aka Googling)

The tradition in computer programming is typically that the first program written in a new language is one that prints the line “Hello, World!”. This serves as a quick introduction to some aspects of the programming language under study. Similarly, the primary example for Big Data is a program that, given a word corpus, computes the number of occurrences of each word. While more complicated, it succinctly illustrates the Map-Reduce programming model. One can then reason about how it works, convince oneself that it does indeed work, and then see ways to expand its scope, and finally seek out applications for it.

I googled for “Hello World of Machine Learning” and the results were of a scope larger than I expected. For instance, the number two on a Google search for “hello world of machine learning” describes “iris classification”, i.e. identifying varieties of the iris flower as the “classic hello world classification problem”. The website actually says,

> You do not need to understand the problem the tool or the algorithms. Not yet. You are building… familiarity with the tool and what it provides. ²

Reading through this website, the author says “\[t\]he beauty of this _trick_ is that it familiarizes yourself with algorithms \[sic\] and tools” (my emphasis). Nothing on that page discusses the algorithm in a manner that can be described as familiarizing. If all it took to familiarize oneself with the internal workings of (say) a plane were to sit in one, we’d all be airplane mechanics.

Other resources are just as bad. This project on [GitHub](https://github.com/machine-learning-projects/machine-learning-recipes) says it is all about “Machine Learning Recipes”. Again, nil explication. ³

In general, from what I’ve seen, introduction to ML texts treat ML systems as closed systems. You’re presented with a beautiful box into which you may not peer. You’re encouraged to tweak various _parameters_ of the algorithms but the algorithms themselves belong to the high priests.

This is sharply different from my experience learning other subjects where the strategy always begins with a simple example that one can reason about. The starting example will typically illustrate the problem that you can then work out on paper. As far as I know, this is how all topics are learnt and you’re encouraged to consider them from first principles.

Like ML, Blockchain and encryption are also heavily mathematical. However, it’s possible to understand the latter two without getting into their technical details. Any introduction to the RSA encryption algorithm begins with two single-digit numbers and showing how it works and why breaking it is computationally intractable. This has been my (admittedly, anecdotal) experience but it holds and applies for all complicated topics.

For instance, Ken Shirriff literally walks us through “[Mining Bitcoin With Pencil and Paper](https://gizmodo.com/mining-bitcoin-with-pencil-and-paper-1640353309)”⁴. There’s much speculation about whether bitcoin is a bubble but the protocol itself is remarkably simple and elegant. Almost all introductory articles discuss bitcoin’s architecture and very few its uses.

With ML, I’m yet to come across a simple example that illustrates why it produces the results that it does. While immediately beginning with complex image processing that recognizes cats does have a wow-factor, I haven’t seen anyone take off the covers and explain _how_ the magic happens. My suspicion is that even the experts don’t know and this leads to the dark but open secret of ML: we don’t know what we don’t know. It’s why the silliest things break an ML down. For instance, in a paper by Jiawei Su et al, describe how they were able to fool a “deep neural network” by altering _a single pixel_. In a series of images they changed one pixel which made the system recognize, among other examples, an airplane as a dog, a horse as a cat, or dog as a cat. Imagine an automated car that’s fooled so easily. ⁵

Consider the consequences of this. When an image recognition algorithm is trained only on data but with no principles underlying it, we don’t know how it does what it does. A famous example is an ML system which was trained to differentiate between dogs and wolves. The system was trained with images of wolves labeled WOLF and images of dogs labeled DOG. It actually performed well on different inputs but when the researchers looked under the hood, they discovered that all the system did was: if the image has “snow”, it’s a WOLF; otherwise it’s a DOG. The story of Clever Hans comes to mind. ⁶ (In my earlier post¹, I featured a mistake made by Google Photos which categorized African Americans as gorillas. These things happen too often with ML and I think it’s a tell that ML experts don’t understand ML.)

Again, compare the above with cryptographic discussions around SHA-1 vs SHA-256. The limitations around the algorithm were known and understood even when implemented. Implementations went ahead with this knowledge because breaking it was considered computationally too hard for the time. And they were correct. ⁷

I guess my biggest problem with ML is philosophical. While the topics which interest me explain _how_ something works leaving aside _what_ can be done with it; ML describes _what_ can be done with it ignoring, almost entirely, the _how_. And in my opinion, _science_ and understanding are in the business of the former.

In my pursuit of simple examples of ML the only pursuits of simplicity have been by the critics.

Gary Marcus, psychologist at NYU, in his 2001 book _The Algebraic Mind_ ⁸ experimented with ML with a simpler function. He trained an ML system to produce the binary notation of any positive integer. Below is a sample of his training data.

```
+----+-------+
|  X |  f(X) |
+----+-------+
|  2 |    10 |
|  4 |   100 |
|  6 |   110 |
|  8 |  1000 |
| 10 |  1010 |
| 12 |  1100 |
| 16 | 10000 |
+----+-------+
```

`X` is a number and `f(X)` is the number’s _binary notation_. Marcus did two interesting things. (1), he fed the ML its data and, interestingly, (2) he gave the ML _only_ even numbers as its input. The crucial thing about ML systems is that they have no understanding of what’s happening and no inferences either. A consequence of binary notation is that even numbers will _always_ have the last digit be `0`. Given an even integer _p_, it is guaranteed that the binary notation of _p_ will end with `0`. Equally, it’s guaranteed that the binary notation of _p+1_ will end with `1`.

Marcus’s ML system worked correctly for even numbers. When given an even number it hadn’t previously encountered, it managed to give the number’s binary notation but when given an odd number, a number it had never encountered in its training, it failed completely. It instead gave the binary notation of the even number.

In Marcus’s case, he knew what he was doing. He knew because he simplified and tested a specific case. Had his ML responded correctly it wouldn’t have proven anything, of course. A positive could be a false positive. However, his experiment proved a negative and that’s always significant. Coming back to ML, ML systems are trained on large, uncurated datasets. How do the researchers know they’ve covered all cases? How can they _show_ that their inputs are sufficient? If they _can_, why aren’t they searching for the _minimal set_ which would prove the case? That’s what scientists do. Kepler collected a large amount of astronomical data. He didn’t collate that data into a corpus but came up with his _Laws_. It’s because he was able to reduce his data to conclusions that we know of him and respect him. Not because he amassed data and fit it to a curve. ⁹

A large aspect of the problem is a lack of recognition of the issue that the psychologist Steven Pinker raised in his book, _The Language Instinct_. ¹⁰

> The main lesson of thirty-five years of AI research is that the hard problems are easy and the easy problems are hard. The mental abilities of a four-year-old that we take for granted — recognizing a face, lifting a pencil, walking across a room, answering a question — in fact solve some of the hardest engineering problems ever conceived.

#### Footnotes

¹ “Google and the Failures of Enormous Data” [https://medium.com/galileo-onwards/google-and-the-failures-of-enormous-data-85cc89e0f18a](https://medium.com/galileo-onwards/google-and-the-failures-of-enormous-data-85cc89e0f18a).

² Full website, [https://machinelearningmastery.com/hello-world-of-applied-machine-learning/](https://machinelearningmastery.com/hello-world-of-applied-machine-learning/). The iris classification dataset may be found at [http://archive.ics.uci.edu/ml/datasets/Iris](http://archive.ics.uci.edu/ml/datasets/Iris). The iris classification problem is a program that’s trained on aforesaid dataset which then can categorize arbitrary images as (a) this is an iris of type _X_ or (b) this is not an iris.

³ GitHub project is available at [https://github.com/machine-learning-projects/machine-learning-recipes](https://github.com/machine-learning-projects/machine-learning-recipes).

⁴ Full url: [https://gizmodo.com/mining-bitcoin-with-pencil-and-paper-1640353309](https://gizmodo.com/mining-bitcoin-with-pencil-and-paper-1640353309).

⁵ “One pixel attack for fooling deep neural networks” by Jiawei Su, Danilo Vasconcellos Vargas, Sakurai Kouichi, Nov 16 2017, available at [https://arxiv.org/abs/1710.08864](https://arxiv.org/abs/1710.08864).

⁶ For examples about ML failures see [https://medium.com/veon-careers/dogs-wolves-data-science-and-why-machines-must-learn-like-humans-do-213b08036a10](https://medium.com/veon-careers/dogs-wolves-data-science-and-why-machines-must-learn-like-humans-do-213b08036a10). Clever Hans was a horse which could count. Upon investigation, they discovered that the horse gave its answers by picking up subtle clues from its questioners. Wikipedia [https://en.wikipedia.org/wiki/Clever\_Hans](https://en.wikipedia.org/wiki/Clever_Hans). It turns out I’m not the first person to critique ML using Clever Hans either. Ian Goodfellow, Senior Researcher at Google, apparently made the same comparison at a talk referred to at [https://tatourian.blog/2017/08/28/artificial-intelligence-versus-clever-hans-the-horse-that-could-count/#1](https://tatourian.blog/2017/08/28/artificial-intelligence-versus-clever-hans-the-horse-that-could-count/#1). See also Carl Sagan’s 1995 book, _The Demon-Haunted World._

⁷ For details on breaking the SHA-1 algorithm, see [https://shattered.io/](https://shattered.io/). The website itself says that “theoretical attacks have been known since 2005, and SHA-1 was officially deprecated by NIST in 2011”. The paper was published in early 2017.

⁸ Description of Gary Marcus’s book at the publisher’s website: [https://mitpress.mit.edu/books/algebraic-mind](https://mitpress.mit.edu/books/algebraic-mind).

⁹ Kepler’s Laws can be found on Wikipedia at [https://en.wikipedia.org/wiki/Kepler%27s\_laws\_of\_planetary\_motion](https://en.wikipedia.org/wiki/Kepler%27s_laws_of_planetary_motion)

¹⁰ For a description of _The Language Instinct_ (1994), visit the author’s page at [https://stevenpinker.com/publications/language-instinct](https://stevenpinker.com/publications/language-instinct). I strongly recommend this book. In my opinion, it’s the best popular science book and the best introductory book to Chomskyan linguistics.

¹¹ About the image: It was generated using the software program, Graphviz. The script which generated it is available at [https://gist.github.com/lvijay/1acbf225242532ac557594a5d8288a8e](https://gist.github.com/lvijay/1acbf225242532ac557594a5d8288a8e). For details about Graphviz, see [http://graphviz.org/](http://graphviz.org/).
