---
title: "Solving Minesweeper — Part II"
description: "Software Methodology"
date: "2023-05-13T11:42:51.259Z"
categories: []
published: false
---

This post is [part two](https://medium.com/galileo-onwards/solving-minesweeper-part-2-cff2cd831111) of a [series](https://medium.com/galileo-onwards/minesweeper-d53b4ba60e73) on an Artificial Intelligence powered automated Minesweeper solver.

In this post, I describe my approach to the solver, without a description of the solver itself. As a rule, I work on any side projects only during the weekends, never touching them during the week. Constraining available time ensures I focus only on what’s necessary.

My methodology, which is not original, is described in 3 simple steps:

1.  Make it work
2.  Make it better
3.  Make it faster

In Part 6, the final part, we see some applications of ⑶. Parts 3–5 deal primarily with ⑴ with minor explorations of ⑵.

### The Goal

> The most important single aspect of software development is to be clear about what you are trying to build. — Bjarne Stroustrup

Like the great Stroustrup recommends, my goal here was clear: to write a minesweeper solver that plays on [minesweeper.online.](https://minesweeper.online.)

I used to play the game on my Windows computer from the late nineties through the early noughties. I was quite happy with my exploits in the game—Intermediate finished in 28_s_ and Expert in 83_s_. Anchored to my memories of that Minesweeper, I couldn’t play any Minesweeper clone because it lacked the original’s look-n-feel. Discovering minesweeper.online was a blessing. I loved playing on the site though my more recent results were nowhere near my heyday — Intermediate in 43_s_ and Expert in 126_s_.

Thinking about the implementation, I realized the solver must consist of four parts, the analyzer — which identifies which cells are mines —  the recognizer — which figures out the cells — the effector — which clicks on cells— and the coordinator that puts these four parts together.

When starting the project, I knew the analyzer would be written using the Z3 Theorem Prover in Python. I wasn’t sure how I’d write the _recognizer_ or _effector_. I had multiple options like Selenium WebDriver for both but eventually went with OpenCV-Python and Java respectively.

Let’s look at the project’s approach.

### Planning

Project planning involves breaking it down into multiple components, finalizing the interfaces between components, and determining the order to implement the components in.

A _well_ planned project ensures the fewest messages are exchanged between the multiple components, the implementation of one component does not interfere with another, changes in one do not impact changes in another, and the projects can proceed independently until they must meet. Imagine, for example, constructing a bridge on pillars. If it took 20 people to build a pillar and the road on top of the bridge, then with 200 people you could start constructions of 10 pillars at once. You’d just have to ensure your bridge doesn’t end up like the humorous [bridge alignment joke](https://www.snopes.com/fact-check/misaligned-bridge-photo/).

I’ve attempted to illustrate the planning approach below.

#### Commit History

Below is an illustration of my commit history. I’ve plotted the days I worked on the solver and how many changes went into each file in the project. For simplicity, I’ve only included the code files and skipped the images.

Recall from Part I that the solver’s architecture consists of four parts: the analyzer, the recognizer, the effector, and the coordinator.

When well planned, you’d expect each individual component worked independently of the others. If you have 3 components and 3 devs, each starts work at the same time and they proceed to their individual completion. (Things get complicated when the components are completed at different times. The last thing you want are idle developers. But hey, who said planning was easy.)

In the case of this solver there was only one developer (me) so the entire operation was executed linearly. The X-axis counts days into the project and the Y-axis counts for the total number of changes to a file. Each individual line represents a different file in the project. Luckily, the project has only a few components and files and the mapping between components and files is straightforwardly one-to-one. The only example of _one-component multiple-files_ are the files `ai.py`, `ai1.py`, …, `ai5.py` which were all written in the service of `find_minesweeper_grid.py`. Those files are not actually used by the solver, I wrote them in various iterations to better understand OpenCV. I discuss them in [Part Ⅲ](https://medium.com/galileo-onwards/solving-minesweeper-part-3-6c96e5f389fc).

A plot of days into the project against number of changes on the file. The 

Looking at the graph above, you see it _is_ well executed. Each component worked on independently and all commits, touch only one project. I can attest that I had a clear plan of _how_ things ought to link up with one another before beginning. That helped. Things didn’t go _perfectly_ these are detailed in parts 3–6.

Viewers will notice the _purple_ line above violates the one-component one-day rule. The purple lines tracks the project’s _dependencies_ (for those of you that know Python, it is the file `requirements.txt`) and, as such, cuts across all projects. Hence its long spanning changes are expected.

#### A warning and a conclusion

Let me say that while my method and my associated graph match software development theory, I have not proven my case. See Appendix Ⅱ for examples from other projects. I did not find unequivocal data. I would appreciate any information that supports or disproves the case.

Let’s now turn to actually solving minesweeper. In [Part Ⅲ](https://medium.com/galileo-onwards/solving-minesweeper-part-3-6c96e5f389fc) we’ll see how the cells in minesweeper are organized and how we can _logically_ deduce which cells are and aren’t mines.

See you there.

### Appendix I: Generating the commit graph

The below code, run against the solver repo, generates the graph shown above.

You can run it against any repository. If the repository spans many days, you’re going to get an uninterpretable graph. To run, use the following command

```
/path/to/graph.sh regenerate 2022-12-31
```

The resulting graph will be saved to the file `plot.png`.

### Appendix II: Evidence of Planning Theory

Though I’ve sketched out a theory of good planning and the only evidence I’ve provided is conveniently mine. This is hardly proof. Unfortunately, I do not know of other Free Software (Open Source) projects that _were_ well planned.

This is something to investigate in the future. Let me know if you find evidence in support or contradicting my theory.

I looked at a few open source projects but there was just too much information to be useful. Below are some. 

#### bocker

A shell based Docker clone

Progression on the bocker project. The black line is the README which shows that Peter Wilmott is a better developer than I am. The dark blue line is the project’s main file, bocker. (It goes backwards at one point indicating either later merge of a feature branch into master or history manipulation.). I was unable to make any conclusions from this project.

#### fastapi

A python web application framework

Progression on the fastapi project. I was unable to make any conclusions from this project.
