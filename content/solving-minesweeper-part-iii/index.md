---
title: "Solving Minesweeper - Part III"
description: "Board analysis and solutions"
date: "2023-05-13T11:42:33.073Z"
categories: []
published: false
---

This post is [part three](https://medium.com/galileo-onwards/solving-minesweeper-part-3-6c96e5f389fc) of a [series](https://medium.com/galileo-onwards/minesweeper-d53b4ba60e73) on an Artificial Intelligence powered automated Minesweeper solver.

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
from z3 import Ints, Or, Solver

solver = Solver()
A, B, C, D, E, F, G, H, I = Ints("A B C D E F G H I")

MINE = 1

# note the rules:
# every cell either is or isn't a mine
for cell in (A, B, C, D, E, F, G, H, I):
  solver.add(Or(cell == MINE, cell != MINE))

# now add the facts

# first, note that opened cells aren't mines
for cell in (A, B, C, D, E, F, H, I): # no G
  solver.add(cell == 0)

# next add the neighbor information
solver.add(0 == B + D + E)
solver.add(0 == A + C + D + E + F)
solver.add(0 == B + E + F)
solver.add(1 == A + B + E + G + H)
solver.add(1 == A + B + C + D + F + G + H + I)
solver.add(0 == B + C + E + H + I)
solver.add(1 == D + E + F + G + I)
solver.add(0 == E + F + H)

# are we in a consistent state?
solver.check() # returns sat
```
