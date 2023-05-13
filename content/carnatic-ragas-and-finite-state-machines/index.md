---
title: "Carnatic Rāgās and Finite State Machines"
description: "The heart of the Carnatic system are their rāgās. I don’t at all understand them, though. As I see it,  I have at least the following two…"
date: "2023-05-13T11:45:26.040Z"
categories: []
published: false
---

The heart of the Carnatic system are their _rāgās_. I don’t at all understand them, though. As I see it, I have at least the following two problems:

1.  My musical education ranges between 0 and ε and
2.  I haven’t found any good resources that explain it.

Of course, I’m not going to let something as trivial as _ignorance_ keep me from hypothesizing.

Here’s the gist of what I’ve learned about _rāgās_. Any _rāgā_ consists of at least five musical notes and is described in two parts: an ascending scale (called _ārohanam_) and a descending scale (called _avarōhanam_). These scales define (necessary but insufficient) constraints upon how any composition of notes must be ordered for said composition to be of that rāgā.

### Hypothesis

#### All _rāgās_ can be construed as Finite State Automata.

During a song, when a performer is singing/playing a note, she/he has exactly the following three choices:

1.  Sing the note immediately next in the _ārohanam_ or
2.  Sing the note immediately next in the _avarōhanam_ or
3.  Sing the same note again.

The phrase “immediately next” is to be read as the note that’s immediately on the right of a scale when reading the scale. If the note under question is already at the rightmost end, the first note is the “immediate next” one.

#### Example

Suppose a hypothetical _rāgā_, “_aksa”_, has the following _ārohanam_ and _avarōhanam_: _h, i, j, l, m_ and _l, j, k, h_, respectively. (For some notes ‘_h’, ‘i’, ‘j’, ‘k’, ‘l’, ‘m’_.) During some performance, if I find myself singing (or playing) the note _l_, then I have exactly the following choices:

1.  I can go _up_ (on the _ārohanam_) and sing the note _m_
2.  I can go _down_ (on the _avarōhanam_) and sing the note _l_
3.  I can again sing the note _l._

Similarly, for the same _rāgā_, if I’m singing the note _k_, I have exactly the following choices:

1.  I can go down and sing the note _h_
2.  I can again sing the note _k_.

Note that there are only two options here since the note _k_ does not at all feature in the _rāgā_’s _ārohanam_.

If I’m singing the note _m_,

1.  I can go up and sing note _h_
2.  I can go down and sing note _l_
3.  I can again sing note _m_.

### Empirical Evidence

That’s my theory. Whither my evidence, you ask? That’s what the rest of this post will explore. Since this is an initial hypothesis much like Galileo Galilei, the father of the modern scientific revolution, I too shall ignore most of the complexities of Carnatic songs and see how far I can go with this simple thesis.
