---
title: "The Jokes on Machine Learning"
description: "Humor helps uncover our innate knowledge"
date: "2023-05-13T11:44:42.570Z"
categories: []
published: false
---

In a previous post, [_Which is newer?_](https://medium.com/galileo-onwards/newer-5068491938ec), we discussed how much of our knowledge is already in place. Specifically, we discussed an adjective (_newer_), a few nouns (_book_, _house_), and a transitive verb (_paint_). Here we go farther still, this time with jokes.

I present to you two different jokes that each have _causality_ at the core of their punchline. Once you _get_ the joke, reflect on what you already know for it to _be_ funny.

Our first joke follows. It’s of the “overheard” variety. Picture one person saying this to another.

> I drank whisky with water and I woke up hung over; another time, I drank vodka with water and woke up hung over; last night, I drank rum with water and again woke up hung over. I’m _never_ drinking water again. \[source unknown, cited from memory\]

Now, I know explaining a joke is like dissecting a frog: you can do it but the frog tends to die in the process (ha, ha); I am nevertheless going to spend a few words discussing both jokes.

Clearly the play here is that speaker has made a hilariously wrong inference. It’s the alcohol in the whisky/vodka/rum that’s causing them to throw up, not the water. However, this isn’t such a straightforward inference. An ML/AI system which didn’t already know this would make the same inference as the speaker—that it’s the water that’s causing their sickness. Humans already know (and have learnt) this fact. We are so good at this, in fact, that even if the joke had an additional clause, say, “I drank _sarayam_ with water and threw up”, people would still get the joke _and_ infer that “_sarayam_” was some kind of liquor. (It’s a Tamil word for alcoholic beverage.)

Current ML techniques don’t bother with adding innate knowledge to their systems. Rather, they are configured to entirely form their “models” of the world based on large datasets. (See also Gary Marcus’s experiment with binary numbers in his 2001 book, [_The Algebraic Mind_](https://mitpress.mit.edu/books/algebraic-mind). I briefly discuss it in my [_Machine Learning of Simple Things_](https://medium.com/galileo-onwards/the-machine-learning-of-simple-things-e6bca6d5283f).)

Here’s the second joke. In this one too the hilarity is because of the protagonist’s poor inference.

> There was this biologist who was doing some experiments with frogs. He was measuring just how far frogs could jump. So he puts a frog on a line and says “Jump frog, jump!”. The frog jumps 2 feet. He writes in his lab book: ‘Frog with 4 legs — jumps 2 feet’.  
> Next he chops off one of the legs and repeats the experiment. “Jump frog jump!” he says. The frog manages to jump 1.5 feet. So he writes in his lab book: ‘Frog with 3 legs — jumps 1.5 feet’.  
> He chops off another and the frog only jumps 1 foot. He writes in his book: ‘Frog with 2 legs jumps 1 foot’.  
> He continues and removes yet another leg. “ Jump frog jump!” and the frog somehow jumps a half of a foot. So he writes in his lab book again: ‘Frog with one leg — jumps 0.5 feet’.  
> Finally he chops off the last leg. He puts the frog on the line and teels it to jump. “Jump frog, jump!”. The frog doesn’t move. “Jump frog, jump!!!”. Again the frog stays on the line. “Come on frog, jump!”. But to no avail.

> The biologist finally writes in his book: ‘Frog with no legs — goes deaf’ \[[source](https://jcdverha.home.xs4all.nl/scijokes/4.html)\]

Now, imagine you were training a Machine Learning system with examples such as these. What kinds of conclusions will it arrive at? (_Spoiler_: nothing good :-)
