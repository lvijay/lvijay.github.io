---
title: "Solving Minesweeper"
description: "Writing a good old fashioned AI Minesweeper solver"
date: "2023-05-13T11:42:30.831Z"
categories: []
published: false
---

If you’ve never played Minesweeper, you’re missing out. If you’ve played Minesweeper before and want a surefire way to _stop_ playing it, write an automated solver. I can no longer play the game after watching it played by an AI. I find my gameplay inefficient, slow, and occasionally buggy. When I remember that my AI solution can be more efficient my feeling of human inadequacy increases.

In this post TK, we’ll go through the solver, the architecture, approach, implementation, testing, running, and results. We go into detail not because the solution is tricky or complicated but the opposite. Because the solution presents itself in a simple manner, we can get into it in detail with the hopes that it’ll be useful to others. The implementation is a few hundred lines of Python plus a few more of Java.

First, a quick demo GIF of the solver in action. Except for opening the game in the browser, everything is entirely computer driven.

The solver in action, sped up 4x. Image produced by the author. License: public domain.

I played the game entirely on the website [minesweeper.online](https://minesweeper.online/). They’ve done an excellent job of recreating the game with the look and feel of the original Windows Minesweeper.

The solver was developed in various phases. These are described in later parts. It’s a testament to planning and designing first that, even though individual components were developed and tested independent of one another, when I finally stitched them together, the solver _Just Worked_. And it surprised me with its speed. It was much faster than I expected.

As a consequence of its speed, the next step was 100% predictable to a neutral observer. I wasn’t neutral and so was surprised when👇:

Blocked by [minesweeper.online](http://minesweeper.online).

Before we discuss the solver’s software architecture, let’s quickly take a look at how the game is played.

All the demos and images in this post were produced by me. Unless stated otherwise, they are released in the public domain.

---

### How to play Minesweeper

Minesweeper is a single-player logic game with an element of luck. The game is also associated with the famous P=NP? computer science problem. See the [description](https://www.claymath.org/sites/default/files/minesweeper.pdf) by the mathematician Ian Stewart. There’s even a million dollar prize associated with it.

Without getting into the rules or mechanics of the game, (see [here](https://minesweepergame.com/strategy/how-to-play-minesweeper.php) for instructions), Minesweeper is played in a repeating loop of mouse clicks:

#### ⒈ Guess open a cell

When you guess open a cell, one of 3 things can happen: ⒜ it reveals a number, ⒝ it opens a mine ⒞ it opens a blank cell. Let’s look at each.

⒜ You open a cell, it reveals a number. This number indicates the number of mines around that cell.

Click on a cell, reveal a number. The number indicates how many mines surround the cell. In this case, there’s one mine around the opened cell, there are 4 mines in the 8 cells around the cell marked 4 and so on.

⒝ You open a mine. This ends the game.

Clicking on a mine ends the game.

⒞ You click open a blank cell. A blank cell is a cell with 0 mines around it. Strictly speaking, this is the same as ⒜. Since a zero-cell has no mines around it, the game opens all the surrounding cells as a convenience to players. If any of those surrounding cells are also zero, then the process is repeated. (Cells, once opened, need not be opened again, hence the process is guaranteed termination.)

Clicking on a 0 opens all the cells around it. If any of the cells around a 0 are themselves 0, the process is repeated.

#### ⒉ Figure out the cells that aren’t mines

Open all the cells that, logically, aren’t mines. This is discussed more later.

Open cells that logically aren’t mines.

#### ⒊ Go to step 1

When you open all cells and only those cells that aren’t mines, you win the game.

Opening all non-mines wins the game. In this game, the last unopened cell is the one in the bottom right corner. Note the smiley face at the top changing too. Note the pause while clicking the bottom row — the first 1 in the sequence 1221.

Now that we’ve seen the loop, take a look at the solver’s software architecture.

---

### The architecture

The flowchart below is the solver in action. It’s pretty simple.

Flowchart of the Minesweeper Solver. Diagram drawn on draw.io. License: public domain

The solver’s architecture follows the steps described above and illustrated in the flowchart. There are four parts to the solver, the **analyzer**, the **recognizer**, the **effector**, and the **coordinator**.

The **_analyzer_** deduces which cells of the board aren’t mines. If no cells can be unambiguously labeled, it recommends a cell to guess open.

The **_recognizer_** visually identifies the board and its individual cells. Given an image it identifies the location of the board in that image, its dimensions, and the value of each cell. Each cell is identified as one of the 12 types — _unopened_, _flagged_, _mine_, or the numerical values, _0_, _1_, …, _8_.

The **_effector_** is the robot body of this solver. It moves the mouse and clicks open cells (the arms) it produces the images that the recognizer uses (the eyes).

The **_coordinator_** stitches together these three parts to produce an automated Minesweeper solver. The coordinator runs the loop described in the section above.

The analyzer, recognizer, and coordinators are written in Python 3.9. The effector is written in Java 17 with no dependencies. It runs an HTTP Server that takes screenshots, moves or clicks the mouse. The **coordinator**, written in Python, interacts with the Java **effector** via HTTP. We look at each in their respective parts.

#### A graphic illustration of the coordinator loop

Close watchers of step 3, the finishing GIF above, will have noticed two things:  
⒜ the mouse clicks an already opened box, a one-cell causing the adjacent two unopened cells to blink and  
⒝ there’s a noticeable pause between that click and the one after it.

This is a consequence of the solver’s loop. Here are the actions that happen in that last GIF:

⑴ **coordinator** → **effector**: take screenshot  
⒜ **coordinator** ← **effector**: here you go

⑵ **coordinator** → **recognizer**: identify board state from this screenshot  
⒝ **coordinator** ← **recognizer**: here you go

⑶ **coordinator** → **analyzer**: identify non-mine cells  
⒞ **coordinator** ← **analyzer**: there are 4 unopened cells. They are  
 ⅰ. penultimate row, last column  
 ⅱ. bottom row, 11th column  
 ⅲ. bottom row, 12th column  
 ⅳ. bottom row, 13th column

⑷ **coordinator** → **effector**: click these cells \[… _from the last step_ …\]  
⒟ **coordinator** ← **effector**: done clicking all 4 cells

⑸ **coordinator** → **effector**: take screenshot  
⒠ **coordinator** ← **effector**: here you go

… remaining steps skipped …

When the **effector** clicks step ⒞ ⅲ. the board opens a zero-cell which opens the adjacent cell. The **effector** does not know this and blindly continues with its instructions to open the cells it was instructed to. It is unaware it is clicking on already-opened-cells. (In fact, the **effector**’s instructions are even more abstract—it is told to go to a position on the screen and click the mouse. It knows nothing about minesweeper.)

Below is an annotated animated GIF of the above description, slowed down 5x. The image was fully generated using the awesome ffmpeg. It wasn’t easy, but exhausting and extremely enjoyable. Watch the bottom half of the image. The timer shows the realtime clock on the solver (now slowed down).

Annotated animation of the solver in action. The black box shows elapsed time slowed down 5x. The first scan (not shown) gives 4 cells to open. The 3rd cell opened is a zero so it opens the fourth cell making redundant the fourth click. The solver doesn’t “know” this and makes a useless click.

---

### The analyzer

Given a board state, how do you identify which cells are and aren’t mines? This question is _the_ most important question to answer when playing Minesweeper. For any cell, after analysis, you will have one of 3 answers: ⒜ it is a mine, ⒝ it is not a mine, ⒞ it is unknown. The last point might seem trivial, after all, isn’t it always true? There are cases in the game where _some cells are unknowable_ and we must guess a solution. We’ll get deeper into these as we explore the analyzer.

We’ll address the content here in two parts. First, we’ll just discuss deducing cell values in minesweeper and then we’ll translate this knowledge into the Z3 framework. Coding is easy when you know what to do.

Let’s consider the following cell arrangement. It’s a 3x3 board with exactly one unopened cell in the bottom left corner. The 3 opened cells around this unopened cell read 1. A number cell tells us how many mines there around that cell. In this case, each 1-cell (for simplicity, we’ll refer to opened cells as 0-cell, 1-cell, and so on where the leading digit is the number on the cell), tells us there’s exactly one mine around them. Since there’s only one unopened cell around, we trivially see that it must be a mine. But trivialities help us gain understanding and we proceed hence.

A 3x3 Minesweeper board arrangement.

Below is the same board as above but labeled A, B, C, …, I. Following the image, we write down the logical case for each cell.

The same 3x3 board arrangement as above with cells labeled A through I.

We know that every cell either has a mine or does not. For every opened, cell we know that the surrounding cells have exactly _k_ cells around that cell where _k_ is the cell’s value. When we combine this information, we arrive at the truth that G is a Mine.

1.  There are 0 mines around the cells A, B, C, F, and I.
2.  There’s exactly 1 mine around the cells, D, E, H.
3.  Considering E, we see that exactly one of E’s neighbors has a mine. This could be A, B, C, D, F, G, H, or I.
4.  Since the cells A, B, C, D, F, G, H, and I are already open, they cannot be mines.
5.  G must be a mine.

Representing this in Python using the Z3 Library, we get

```
from z3 import Ints, Xor, Solver

solver = Solver()
A, B, C, D, E, F, G, H, I = Ints("A B C D E F G H I")

MINE = 1
MINE_NOT = 0

# establish the rules:
# every cell either is or isn't a mine
for cell in (A, B, C, D, E, F, G, H, I):
  solver.add(Xor(cell == MINE, cell == MINE_NOT))

# now add the facts
# 1, opened cells aren't mines
for cell in (A, B, C, D, E, F, H, I): # no G
  solver.add(cell == MINE_NOT)

# next add the neighbor information
solver.add(MINE_NOT == B + D + E)
solver.add(MINE_NOT == A + C + D + E + F)
solver.add(MINE_NOT == B + E + F)
solver.add(MINE     == A + B + E + G + H)
solver.add(MINE     == A + B + C + D + F + G + H + I)
solver.add(MINE_NOT == B + C + E + H + I)
solver.add(MINE     == D + E + F + G + I)
solver.add(MINE_NOT == E + F + H)

# are we in a consistent state?
solver.check() # returns sat
```

The last check, `solver.check()` will return `sat` short for _satisfiable_. Meaning the solver’s state is not in a contradiction. Attempting to maintain contradictory facts will put the solver in an `unsat` state (short for _unsatisfiable_). For instance, if we said `solver.add(X == 1); solver.add(X == 0)` then `solver.check()` will promptly return `unsat` since since `X` can have only one value (given that `X` was created as `X = Int()`).

Note that `solver.check()` gives us a definitive answer _only_ when it says `unsat`. In all other cases, it merely says, there isn’t a contradiction. The trick to solving problems with Z3 then, is to try different values, until we get an `unsat`.

After executing the above code block, we try the following.

```
>>> solver.check(G == MINE)
sat
>>> solver.check(G == MINE_NOT)
unsat
```

With `G == MINE_NOT` we get an `unsat` which tells us `G` _cannot_ be `MINE_NOT`. Since `G` either is or isn’t a mine, then we conclude that `G` _must_ be a mine.

This concludes the analyzer’s section. In the implementation, we create a solver once, at the game start. The cell facts are added with each recognizer loop. After adding facts, we individually check each cell with the mine/no-mine test. If we get a contradiction, we know what it is; otherwise we don’t. We accumulate cells that are not mines to open and send that list back to the coordinator.

---

  

### References

The full source code to the automated solver is on GitHub \[TK\]. Feel free to fork and submit your PRs. I do my best to respond but I reserve my non-work related activity for the weekends (and even then family, work, friends take precedence) so forgive me if I’m slow to respond.

The videos in this post were entirely generated using the amazing ffmpeg. I’ve documented the scripts I wrote to generate them in the following gist: [https://gist.github.com/lvijay/42aa9ea9f9acaf6ad13fe71902a41512](https://gist.github.com/lvijay/42aa9ea9f9acaf6ad13fe71902a41512).

#### The Git Magic Trick


