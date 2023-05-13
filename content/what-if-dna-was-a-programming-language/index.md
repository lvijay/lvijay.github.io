---
title: "What if DNA was a programming language?"
description: "Let’s see how far we can take the analogy of programming and DNA."
date: "2020-12-31T17:09:59.631Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/dna-programming-f9ce6193431d
redirect_from:
  - /dna-programming-f9ce6193431d
---

DNA Conformations. Source: [Wikimedia](https://commons.wikimedia.org/wiki/File:Dnaconformations.png), License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.en).

Let’s start with a slightly off-color joke.

> Mom: I think it’s time to have the _birds and bees_ talk with our son.  
> Dad: are you sure?  
> Mom: yes, can you do it?  
> Dad: oh, all right.  
> Father goes to his son.  
> Dad: do you remember what we did with those prostitutes?  
> Son: yes….  
> Dad: well, it’s the same for the birds and bees.  
>  — (Source unknown.)

I start with this joke because, in many ways, it reflects this post.

Suppose you have a software system that executes on demand. Your code resides on the disk and every time it needs to be executed, the code is copied into memory and executed there. (This system isn’t as imaginary as it might sound. Systems like this already exist and are quite popular. Many software Cloud vendors provide this as “serverless compute” services. Some notable examples are [AWS Lambda](https://aws.amazon.com/lambda/), [Google Cloud Functions](https://cloud.google.com/functions/), [Azure Functions](https://azure.microsoft.com/en-in/services/functions/), [Alibaba Cloud Function Compute](https://www.alibabacloud.com/product/function-compute), and [openstack Qinling](https://wiki.openstack.org/wiki/Faas).)

Now, there’s a chance of an error every time the code is copied from disk to memory and _if_ there’s a copying error, do we expect that the program will (a) still run and if it runs (b) give the correct output?

Most of us with any experience in computer programming will expect that the answers to both questions are: it is improbable the program will (a) still run successfully and if it did run (b) it is unlikely to give the correct output. So the natural question is: why bother discussing something so trivial? The answer, like with the birds and the bees above, is that _it’s the same in biology_. However, in biology this expectation is considered controversial.

With that context, our agenda in detail. First, a super brief look at the _Neutral Theory of Molecular Evolution_, followed by programming simulations illustrating the theory. Then, we look at some corollaries of our findings and their equivalents in biology. In this way, we start at a theory of biology, explore it with programming and, using those findings, search for supporting evidence in biology.

(In research, you can find anything if you know what you’re looking for. Conversely, if you look for something without theory, you find either nothing or too much—neither of which is good. The philosopher Immanuel Kant described this beautifully: “concepts without percepts are empty; percepts without concepts are blind”, _The Critique of Pure Reason_ (1781). This post will, I hope, also illustrate Kant’s point.)

### _Neutral Theory of Molecular Evolution_

The _Neutral Theory of Molecular Evolution_ was first published by Motoo Kimura in 1968 in the journal _Nature_[¹](https://authors.library.caltech.edu/5456/1/hrst.mit.edu/hrs/evolution/public/papers/kimura1968/kimura1968.pdf). Kimura (1924-1994) was a researcher at Japan’s National Institute of Genetics. In it he says, “many of the mutations involved \[in molecular biology\] must be neutral ones”. In other words, they must have a net zero effect to the organism. Kimura’s article was a mere 3 pages with two conclusions: (1) the rate of mutation in mammals was quite high. Since most mutations are harmful to an organism a high mutation rate must mean (2) most mutations are irrelevant (“neutral”) with regard to the organism’s fitness. In Kimura’s more technical words, “the very high rate of nucleotide substitution which I have calculated can only be reconciled with the limit set by the substitutional load by assuming that most mutations produced by nucleotide replacement are almost neutral in natural selection”.

We will use Kimura’s insights as the frame for this post. We will analogize the operations of DNA and a cell with a programming language and runtime interpreter respectively. Mutations are errors that have crept into the code.

Let’s begin.

### Random changes to code

Let’s look at a simple program, like the one below. It’s in Python 3. We’ll test Kimura’s theory with simulations. We’ll keep the mathematics to a minimum and rely mostly on simulations.

The code sample we’ll use for all illustrations in this post. The code used to create other aspects of this post is available at [https://gist.github.com/lvijay/649b315918c33da6c68f05e02808e1d0](https://gist.github.com/lvijay/649b315918c33da6c68f05e02808e1d0). Author: self, License: Public Domain.

The code above is 126 characters long and uses 17 unique characters. According to Kimura’s theory, mutations occur and most of them are neutral. We’ll simulate his theory using the above code.

Code with 126 characters implies 126 possible locations where copying errors might occur. For simplicity, let’s make the following assumptions:

⒈ copying errors are equally likely at any place in the code  
⒉ all copying errors result in _adding_ a character in the codebase. For eg, copying “𝓍” can result in “𝓍𝓎” for some characters 𝓍 and 𝓎 part of the corpus.  
⒊ the corpus consists of the following 17 characters: the letters `s`, `p`, `l`, `i`, `n`, `t`, `e`, `r`, `d`, `f`; the whitespace characters RETURN and SPACE `↲`, `▢` respectively; and the special characters `"`, `#`, `:`, `(`, `)`.  
⒋ the system starts by first invoking the method `din`. It is the equivalent of a main method. The code that invokes `din` isn’t shown.

The probability of some event is number of possible ways that event can occur divided by the total number of possibilities. Our code is 126 characters long and there are 17 possible choices for each copy error. This means the total number of possibilities is `126 * 17 = 2142`. (Note: we are counting the number of cases _when_ there’s exactly one copying error. We are not considering the probability of exactly one error. A different and harder problem to solve.) Programmers will expect most programs that take such a random copy error will fail and I agree. But ay, there’s the rub; For in those programs that succeed, what dreams may come?

#### **What is an error?**

Let’s also define what we mean by an error. An error is any time the program results in an Exception and does not run to completion. Some programs will run but print a different output. We’ll ignore them for now though we’ll come back to them.

With these assumptions, let’s count the number of places in the code where _a_ random copy error will and won’t cause program failure and use that to calculate the probability of an error.

Rather than manually compute the successes/errors, generating all variants of copy-error-programs would be 2142 times 2 (= 4284), one program each for the two values the `if` clause on line 2. Four thousand programs is a lot so I reduced the 17 characters into the following 7 groups:

⒈ alphabet — any of `s`, `p`, `l`, `i`, `n`, `t`, `e`, `r`, `d`, `f`  
⒉ colon — `:`  
⒊ double quote — `"`  
⒋ hash — `#`  
⒌ newline — the character `\n`, represented here by the Unicode character, DOWNWARDS ARROW WITH TIP LEFTWARDS `↲`.  
⒍ parentheses — any of `(`, `)`  
⒎ space — the character with ASCII code 32, represented here by the Unicode character, WHITE SQUARE WITH ROUNDED CORNERS `▢`.

This brings us to 126×7×2=1764 programs. Less than half the earlier estimate. I generated and ran these 1764 Python programs and tabulated their results.

#### Results

Let’s look at the failures and successes. Of our total of 1764 possible programs, we have 667 successes and 1,097 failures. However, adjusting for the 10 distinct alphabets and 2 distinct parentheses, we have 2,693 failures and 1,591 successes. This accords with our initial instinct that most copy errors (aka “_mutations_”) will lead to errors — 63% to 37% in this case.

The below image tabulates the failures and successes on a per category basis. It shows how many failures/successes we had after inserting a character for the given category into each of the 126 locations in the code. For instance, following is a failure: inserting a `(` on position 2 in the code, `de(f din(n):` and the following is a success: inserting a `(` on position 50, `## re(set`. In the former case the program fails with error `SyntaxError: unmatched ')'`, in the latter case, the program runs to completion based on the value of `n`.

Table showing the number of failures and successes when a character from a category was inserted in one of the 126 locations in the code. For instance, the following will be an error and the next a success: if an open parenthesis was inserted in location 2 resulting in \`de(f din\` that would be counted as a failure. Whereas the following is a success: an open parenthesis inserted on a line after #, like \`## res)et\` the program will still run.

There aren’t too many surprises here. As one might expect, parentheses, double quotes, and alphabets are the _least_ forgiving towards copy errors — (87%, 76%, and 62% respectively). Adding a stray open or close parenthesis is a guaranteed way to completely screw up your parser. It’s why most editors highlight them in color. I was initially surprised by the high error rate of newlines (63%) but it is expected given that we’ve chosen Python.

Spaces are the most copy-error-resilient. Failing only 33% of the time. If there’s one category that _did_ surprise me, it’s the _Colon_ character. See the §Appendix I for details.

Because just data and tables are boring, I’ve illustrated the problem below using animated gifs and discuss a few categories in more detail. The first example is in the _Alphabet_ category. We discuss it along with the _Space_ and _Hash_ categories. For animated images of the other categories, see §Appendix I.

---

The result when one character is added to the code — categorized into error or non-error. The left side shows the execution result when din is called with n=0 and the right side with n=1. Due to Python’s interpreted nature, changing the function name has an impact only when that fork is invoked. The color indicates whether the program succeeded. It is green when the program ran to completion without an error, red otherwise. pos is the position in the overall program where the “copy error” occurred. Source: [https://github.com/lvijay/neutral-programming](https://github.com/lvijay/neutral-programming). Image license: Public Domain.

𝓐**lphabetic errors** frequently cause failures (62% of the time). Any changes to a Python keyword naturally result in errors, so changing `def`, `if`, `else` always fails. Similarly, errors that cause tokenizing problems like `(a n` also cause problems.

There are only 3 cases where errors do not occur, namely:  
⒈ The change is on a _comment_ line like line 7.  
⒉ The change is within a string as on lines 9, 11, and 13.  
⒊ The change modifies a token which is never executed because it is not part of the execution fork. Thus, when `n` _is-not_ (technically speaking) and causes the _else_ fork to execute, changes are allowed. For instance, look at line 3: when `n=0` any part of the function `rest` can be modified (e.g., `**_f_**rest`) or accept a fake argument (e.g., `rest(**_i_**)`) with no _immediate_ consequences. We’ll revisit this later.

𝓢**paces as a copy error**

The result when one character is added to the code — categorized into error or non-error. The left side shows the execution result when din is called with n=0 and the right side with n=1. Due to Python’s interpreted nature, changing the function name has an impact only when that fork is invoked. The color indicates whether the program succeeded. It is green when the program ran to completion without an error, red otherwise. pos is the position in the overall program where the “copy error” occurred. Source: [https://github.com/lvijay/neutral-programming](https://github.com/lvijay/neutral-programming). Image license: Public Domain.

Adding spaces doesn’t cause many errors to the program. In fact, it is the most forgiving in our sample (only 33% of the programs fail).

Spaces are forgiving in the following cases. (In another language it might even be more forgiving.)  
⒈ In between any two distinct tokens and _not_ affecting Python’s indentation rules.  
⒉ At the end of any line, as its last token.  
⒉⒈ On an empty line  
⒊ Within a string  
⒋ On a comment line like line 7.

𝓗**ash copy errors**  
We’ll look at _one_ more category, the _hash_ character, `#`, and then do some philosophizing, i.e., make some predictions.

The result when one character is added to the code — categorized into error or non-error. The left side shows the execution result when din is called with n=0 and the right side with n=1. Due to Python’s interpreted nature, changing the function name has an impact only when that fork is invoked. The color indicates whether the program succeeded. It is green when the program ran to completion without an error, red otherwise. pos is the position in the overall program where the “copy error” occurred. Source: [https://github.com/lvijay/neutral-programming](https://github.com/lvijay/neutral-programming). Image license: Public Domain.

The hash in Python indicates the start of a comment. The Python interpreter ignores everything start at the hash upto the end of the line. Thus, as one would expect, it will also have fewer errors and this is bourne out by the data (46% or 47% depending on _n_).

Hash copy-errors are forgiving in the following cases:  
⒈ As the last token on any line, i.e., end of line  
⒈⒈ On an empty line  
⒉ On a comment line  
⒊ Within a string  
⒋ Similar to Alphabet-error-3 (above), non-executing forks can be changed with no immediate consequences. (Similar but not exact. See image to note the differences.)

---

### Corollaries

Recall that we’ve analogized the code with DNA and the Python interpreter then becomes the _cell_. The success of failure of programs then becomes Natural Selection. The thing about Natural Selection is that it’s an extreme case of _survivorship bias_. Who survives succeeds. (Though, certainly in our example, and [perhaps in evolution too](https://us.macmillan.com/books/9780312680664), there’s [nothing particularly special](https://xkcd.com/1827/) about the survivors.)

#### Corollary 1: Neutral Theory confirmed

First, we’ll look only at the survivors. After all, as the cliche goes, dead men tell no tales. We’ll stick to the 7 categories and one sample from each.

645 of the programs run with _some_ output. Of these 645 programs, 288 print `tridnt` with input `n=1` and 287 print `lensed` with input `n=0`. 70 lines have an output different from the norm. I’m including outputs with leading or trailing spaces as different from the norm, for example, `"lensed "` and `" tridnt"`. Recall that we had 667 successful programs. 22 programs had no output at all.

Of 667 successful programs, a grand total of 575 programs gave the same output as the original program even with one copy error. This is 86%.

Repeating Kimura’s words, “most mutations produced by nucleotide replacement are almost neutral”.

#### Corollary 2: There must be parts of the DNA that undergo more mutations than others

This will require slight elaboration. Let’s look at the errors on a _line by line_ basis. I’ve tabulated these statistics below. The table shows the number of failures encountered on the line. For simplicity, I summed up the failures and successes across both values of `n`.

Observing the tables, we can see that _comment lines_ are most resilient to copy-errors. In the current code, over 7 categories, 9 characters, and 2 values (total 126) the hash line is 86% successful (108 successes to 18 failures).

Thus, we can reasonably surmise, any line that gets a _comment_ character and survives, will become a resilient locus for future random changes. Remember, we care only about the survivors.

undefinedundefinedLine by line success and failure count for various categories in the code. Line 7, the comment line, is the most robust line towards copy errors. Over 7 categories, 9 available positions, and 2 possible values, (total 126) it is successful 86% of the time (108 successes to 18 failures). Source: [https://github.com/lvijay/neutral-programming](https://github.com/lvijay/neutral-programming). Image License: Public Domain.

**Evidence**  
I googled for the following term “some parts of dna have more mutations”, and google took me to a 2004 paper. It turns out to be a commentary on a technical paper that appeared in the technical journal **PLoS Biology**. The article says, “\[c\]orrelating gene mutation rates with their location in the genome, \[researchers\] Jeffrey Chuang and Hao Li… confirm that regional mutation rates indeed exist”. The article is available at [https://www.ncbi.nlm.nih.gov/pmc/articles/PMC340953/](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC340953/).

#### Corollary 3: Most of DNA must do nothing

Following corollary 2, if changes accumulate in _comment_ lines it must follow that those portions of DNA do nothing. And since changes at those loci will accumulate, there will be large portions of DNA that do nothing.

**Evidence**  
I googled for “do most dna do nothing” and link one was a 2015 article in the NYT written by ace science journalist, Carl Zimmer. The article is titled, aptly enough, “Is Most of Our DNA Garbage?”. In it Zimmer says, “a vast majority of its DNA is — to put it bluntly — junk.” The article is available at [https://www.nytimes.com/2015/03/08/magazine/is-most-of-our-dna-garbage.html](https://www.nytimes.com/2015/03/08/magazine/is-most-of-our-dna-garbage.html).

**Note**: The science, it seems, is nowhere near settled. The above article is discusses the issues in some detail. For what it’s worth, I hold to the junk DNA side.

#### Corollary 4: Sections of DNA will be unmodified

This is the flip side to corollary 3. From the experiments, we see there are portions of the code that _allow no changes_, regardless of the value of `𝓃`. For example, `def`, `if`, and `else` are inviolable.

**Evidence**  
Luckily for me, I didn’t have to google this one. The previous two references were sufficient. They said, respectively:

1.  “Cold-region genes… tend to be highly conserved, changing very little since they first evolved.” and
2.  “Over millions of years, essential genes haven’t changed very much, while junk DNA has picked up many harmless mutations.”

#### Corollary 5: New phenotypes arise when non-coding sections become coding sections

This is slightly out-there and highly speculative. (Maybe I shouldn’t call it a _corollary…_.) Let me elaborate.

undefined

Suppose our code is in the following state. We’ve elided most of the code because it isn’t relevant to our current discussion.

undefined

The part we care about is that comment section. Almost all changes that occur there will be neutral.

undefined

Now, suppose a series of mutations occur at this neutral site. The path to that eventuality doesn’t matter, we’re mostly concerned with the end state, which, in our example finally reads `print("instill") #"de f)t:)`.

At this point, suppose there’s, [Columbo style](https://en.wikipedia.org/wiki/Columbo), _just one more_ mutation, this one inserts a newline just after the first `#`. That’ll put the code in the following state:

undefined

And just like that, we have a `print` statement on a new line providing new behavior.

**Evidence**  
I have none and I didn’t google either. When they announce some team winning the Nobel for this, I’ll be staking my rightful claim.

It does seem in the realm of _possibility_ though even finding evidence along these lines would be hard. And, even if evolution did progress by my theory, the following are our unknowns: what is the probability of such changes? it’s entirely possible that _even_ with changes accumulating along these lines, the organism doesn’t make it because of a fatal mutation in some other coding site. (It’s the classic story, “I am walking along the Champs Elysées one day and I see an old friend across the street. There is no traffic nearby and I’m not otherwise engaged, so, being rational, I start to cross the street. Meanwhile, at 33,000 feet, a cargo door falls off a passing airliner,2 and before I make it to the other side of the street I am flattened.” ²)

---

I’ll stop the analogies after one more example. We started by saying we’ll copy code every time we need to execute our program. This is certainly true for DNA. Let’s consider two questions that follow from this fact: ⑴ just how many times is the code copied anyway? and ⑵ are there consequences of copy errors?

#### ⒈ How many executions?

“During an average human life span, the cells inside the body cumulatively pass through approximately 10¹⁶ growth-and-division cycles” ⁴ says a textbook. 10¹⁶ is a staggeringly large number. Imagine all the grains of sand in the world today. That’s only a [hundred times](https://www.npr.org/sections/krulwich/2012/09/17/161096233/which-is-greater-the-number-of-sand-grains-on-earth-or-stars-in-the-sky) more than the number of cell divisions we’ll go through in our lifetime. Over a 75 year lifespan, that translates to 4000 copies per second.

#### ⒉ Copy error consequences

“random errors occurring during DNA replication in normal stem cells are a major contributing factor in cancer development” say two researchers, Cristian Tomasetti and Bert Vogelstein, in the premier research journal, _Science_⁵. Their article is available at [https://science.sciencemag.org/content/347/6217/78](https://science.sciencemag.org/content/347/6217/78).

---

Let’s now consider some aspects that haven’t been discussed, some places where I’m possibly wrong, some parts where the programming language analogy doesn’t really fit.

### Unconsidered aspects

While this discussion has, in my opinion, gone quite far in representing evolution as it actually happens, it lacks in some aspects. Those are the areas we discuss here. First is that our analysis is purely syntactic, not semantic. Second is we’ve only considered changes to the DNA and not the _cell_ mechanism itself. Of the two, the first is, I think, impossible to predict even in biology but I get ahead of myself.

#### Syntactic not semantic

Our analysis, has been a purely _syntactic_ one—we don’t discuss _what_ anything means, just how they interact with each other and what they do. For example, what are these programs computing anyway? what does it mean that a program which earlier printed `dissent` now prints `dissent↲instill`? what does `n`, the argument to the main function, actually represent? what is its true frequency of occurrence? These are the truly interesting questions because, certainly for an organism, it is these successful mutants that go on to form new variants and build upon that process we call _evolution_.

#### Triple Helix

In his 2002 [book](https://www.hup.harvard.edu/catalog.php?isbn=9780674006775) with the same title, molecular biologist, Richard Lewontin points out it’s absurd to talk exclusively about DNA and genes because the molecule by itself can tell you nothing. The DNA molecule acts in concert with the _cell_. Together they form the organism. (Some day, perhaps biotech will come to a stage where DNA can be fixed in some form and we’ll have different cells that interpret them differently.)

In this post, I’ve kept _to_ code and DNA. But who knows what changes can (perhaps already have) come about because of changes in the cell itself. In Robert Louis Stevenson’s great science fiction novella, _The Strange Case of Dr Jekyll and Mr Hyde_ (1886)³, Dr. Jekyll makes a “draught” potion that turns him into Mr. Hyde. He is unable to later recreate this potion because, it turns out, his _initial_ ingredients contained some “unknown impurity which lent efficacy to the draught”. In a like manner, who knows if some trait of a species evolved because an otherwise ordinary strand of DNA was just poorly interpreted by a cell.

𝒯_his_ is a good place to stop. I could continue and ideas are heading my way but one mustn’t get high on one’s own supply.

### Appendix I: Animations of all categories

undefinedundefined

undefinedThe result when one character is added to the code — categorized into error or non-error. The left side shows the execution result when din is called with n=0 and the right side with n=1. Due to Python’s interpreted nature, changing the function name has an impact only when that fork is invoked. The color indicates whether the program succeeded. It is green when the program ran to completion without an error, red otherwise. pos is the position in the overall program where the “copy error” occurred. Source: [https://github.com/lvijay/neutral-programming](https://github.com/lvijay/neutral-programming). Image license: Public Domain.

### Footnotes

¹ Motoo Kimura, “Evolutionary Rate at the Molecular Level”, accessed at [https://authors.library.caltech.edu/5456/1/hrst.mit.edu/hrs/evolution/public/papers/kimura1968/kimura1968.pdf](https://authors.library.caltech.edu/5456/1/hrst.mit.edu/hrs/evolution/public/papers/kimura1968/kimura1968.pdf).

² This brilliant joke is from the premier Artificial Intelligence textbook, “Artificial Intelligence: A Modern Approach” 2nd edition (2003), by Stuart Russel and Peter Norvig. Their book is currently in its Fourth Edition. The book’s website is [http://aima.cs.berkeley.edu/](http://aima.cs.berkeley.edu/). Their joke has a footnote reference to the following _Washington Post_ article: “New Door Latches Urged For Boeing 747 Jumbo Jets”, written by Nell Henderson on Aug 24, 1989. The article is available at [https://www.washingtonpost.com/archive/politics/1989/08/24/new-door-latches-urged-for-boeing-747-jumbo-jets/4ea406f5-dfa5-4b66-83e6-54555e850ef9/](https://www.washingtonpost.com/archive/politics/1989/08/24/new-door-latches-urged-for-boeing-747-jumbo-jets/4ea406f5-dfa5-4b66-83e6-54555e850ef9/).

³ Robert Louis Stevenson’s _The Strange Case of Dr. Jekyll and Mr. Hyde_ is available at [https://www.gutenberg.org/files/43/43-h/43-h.htm](https://www.gutenberg.org/files/43/43-h/43-h.htm).

⁴ “Number of cell divisions in an average human lifespan” [https://bionumbers.hms.harvard.edu/bionumber.aspx?s=n&v=10&id=100379](https://bionumbers.hms.harvard.edu/bionumber.aspx?s=n&v=10&id=100379). The link cites the book by R. Weinberg, _The Biology of Cancer_, 2nd edition, 2014.

⁵ “Variation in cancer risk among tissues can be explained by the number of stem cell divisions” by Cristian Tomasetti and Bert Vogelstein available at [https://science.sciencemag.org/content/347/6217/78](https://science.sciencemag.org/content/347/6217/78). Published in _Science_ on Jan 2, 2015.
