---
title: "The Jokes on Machine Learning v1"
description: "Humor helps uncover our innate knowledge"
date: "2023-05-13T11:44:50.165Z"
categories: []
published: false
---

### The Jokes on Machine Learning v1

#### Humor helps uncover our innate knowledge

In a previous post, [_Which is newer?_](https://medium.com/galileo-onwards/newer-5068491938ec), we discussed how much of our knowledge is already in place. Specifically, we discussed an adjective (_newer_), a few nouns (_book_, _house_), and a transitive verb (_paint_). Here we go farther still, this time with jokes.

I present to you two different jokes that each have _causality_ at the core of their punchline. Once you _get_ the joke, reflect on what you already know for it to _be_ funny.

Our first joke follows. It’s of the “overheard” variety. Picture one person saying this to another.

> I drank whisky with water and I woke up hung over; another time, I drank vodka with water and woke up hung over; last night, I drank rum with water and again woke up hung over. I’m _never_ drinking water again. \[source unknown, cited from memory\]

Now, I know explaining a joke is like dissecting a frog, you can do it but the frog tends to die in the process, I am nevertheless going to spend a few words discussing both jokes.

Clearly the play here is that speaker has made a hilariously wrong inference. It’s the alcohol in the whisky/vodka/rum that’s causing them to throw up, not the water. However, this isn’t such a straightforward inference. An ML/AI system which didn’t already know this would make the same inference as the speaker — that it’s the water that’s causing their sickness. Humans already know (and have learnt) this fact. We are so good at this, in fact, that even if the joke had an additional clause, say, “I drank _sarayam_ with water and threw up”, people would still get the joke _and_ infer that “_sarayam_” was some kind of liquor. (It’s a Tamil word for alcoholic beverage.)

Current ML techniques don’t bother with adding innate knowledge to their systems. Rather, they are configured to entirely form their “models” of the world based on large datasets. (See also Gary Marcus’s experiment with binary numbers in his 2001 book, [_The Algebraic Mind_](https://mitpress.mit.edu/books/algebraic-mind). I briefly discuss it in my [_Machine Learning of Simple Things_](https://medium.com/galileo-onwards/the-machine-learning-of-simple-things-e6bca6d5283f).)

Here’s the second joke. In this one too the hilarity is because of the protagonist’s poor inference.

> There was this biologist who was doing some experiments with frogs. He was measuring just how far frogs could jump. So he puts a frog on a line and says “Jump frog, jump!”. The frog jumps 2 feet. He writes in his lab book: ‘Frog with 4 legs — jumps 2 feet’.  
> Next he chops off one of the legs and repeats the experiment. “Jump frog jump!” he says. The frog manages to jump 1.5 feet. So he writes in his lab book: ‘Frog with 3 legs — jumps 1.5 feet’.  
> He chops off another and the frog only jumps 1 foot. He writes in his book: ‘Frog with 2 legs jumps 1 foot’.  
> He continues and removes yet another leg. “ Jump frog jump!” and the frog somehow jumps a half of a foot. So he writes in his lab book again: ‘Frog with one leg — jumps 0.5 feet’.  
> Finally he chops off the last leg. He puts the frog on the line and teels it to jump. “Jump frog, jump!”. The frog doesn’t move. “Jump frog, jump!!!”. Again the frog stays on the line. “Come on frog, jump!”. But to no avail.

> The biologist finally writes in his book: ‘Frog with no legs — goes deaf’ \[[source](https://jcdverha.home.xs4all.nl/scijokes/4.html)\]

The humor in both jokes is akin to what linguists call _garden-path sentences_. Stephen Pinker discusses them as an experiment to determine the order in which humans (instinctively) parse sentences (_The Language Instinct_, 1994). According to [Wikipedia](https://en.wikipedia.org/wiki/Garden-path_sentence), “a _garden-path sentence_ is a grammatically correct sentence that starts in such a way that a reader’s most likely interpretation will be incorrect”.

A few examples will help:  
⒈ The horse raced past the barn fell.  
⒉ The prime number few.  
⒊ The old man the boat.  
⒋ The complex houses married and single soldiers and their families.  
⒌ Fat people eat accumulates.  
⒍ Buffalo buffalo Buffalo buffalo buffalo buffalo Buffalo buffalo — this has its own [Wikipedia page](https://en.wikipedia.org/wiki/Buffalo_buffalo_Buffalo_buffalo_buffalo_buffalo_Buffalo_buffalo).

I’ll leave you to parse them (or look at wikipedia :-). Either way though, note the following

1.  it’s not trivial to get a computer to understand these sentences (though parsing them might be easier)
2.  sentences of this sort are probably found only in linguistics texts (and probably their eponymous wikipedia page) so the odds that an ML system was trained on them is approximately zero.

#### What steps are ML researchers taking towards understanding?

Unfortunately for us this isn’t a goal of ML. Here’s a recent example: Uber AI have updated their systems to prevent the kind of gaffes that most ML language bots are by now famous for ([link](https://www.technologyreview.com/s/614961/ai-language-gpt-2-tame-controllable-uber/)). The article quite unabashedly admits that its “model still doesn’t understand meaning”.

It’s for the same reason that researchers within the field are admitting they’re on the wrong track.

Geoffrey Hinton, who coauthored the 1986 paper which, it is claimed, “is central to the explosion of artificial intelligence” said as much in 2017. “My view is throw it all away and start again”, he said to Axios. He also said that the ML techniques are not “how the brain works”.

x [https://www.axios.com/artificial-intelligence-pioneer-says-we-need-to-start-over-1513305524-f619efbd-9db0-4947-a9b2-7a4c310a28fe.html](https://www.axios.com/artificial-intelligence-pioneer-says-we-need-to-start-over-1513305524-f619efbd-9db0-4947-a9b2-7a4c310a28fe.html)

x [https://www.technologyreview.com/s/614961/ai-language-gpt-2-tame-controllable-uber/](https://www.technologyreview.com/s/614961/ai-language-gpt-2-tame-controllable-uber/)
