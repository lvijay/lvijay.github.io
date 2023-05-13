---
title: "The most boring way to solve a logic puzzle"
description: "You can brute force the solution to a puzzle but should you?"
date: "2021-05-11T07:47:55.151Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/boring-logic-5a85da15e748
redirect_from:
  - /boring-logic-5a85da15e748
---

Image taken from Hy Conrad’s Giant Book of Whodunit Puzzles (1999) © publisher. Usage: fair use.

There’s a class of puzzles, called _logic puzzles_, which can be solved by simple programs. For instance, consider the following puzzle titled “Inspector Walker feels the heat”. It is taken from Hy Conrad’s _Giant Book of Whodunit Puzzles_ (1999, pg 115–6).

Rather than copy/pasting the puzzle (not easy when I have a print version), below is a summary. (If you want to read it, you can see the puzzle on Google Books \[[link](https://books.google.co.in/books?id=Dy4FAHkthO4C&pg=PA30&lpg=PA30&dq=%22inspector+walker+feels+the+heat%22&source=bl&ots=7wjsy4z6zu&sig=ACfU3U3muhsYx0S97s9pYZtXwenzpOCO4w&hl=en&sa=X&ved=2ahUKEwjso7D2oL_wAhVszzgGHaBICkkQ6AEwAHoECAIQAw#v=onepage&q=%22inspector%20walker%20feels%20the%20heat%22&f=false)\].) The puzzle is as follows:

A crime has been committed. The police have 5 suspects at least one of whom is guilty. The suspects are Chase, Decker, Ellis, Heath, and Mullaney. The police have acertained the following facts:

1.  if Chase is guilty and Heath is innocent, then Decker is guilty.
2.  if Chase is innocent, then Mullaney is innocent.
3.  if Heath is guilty, then Mullaney is guilty.
4.  Chase and Heath are not both guilty.
5.  Unless Heath is guilty, Decker is innocent.

If you’d like to take a stab at solving the puzzle yourself, pause here. Go ahead, solve it and then come back.

---

Personally, I find _if_ conditions hard to reason about so I got lazy and coded my way out of the puzzle. I translated the above 5 conditions into their equivalent Python code. Each of the participants is represented by their initial (Chase is `c`, Decker is `d` and so on.) They take a boolean value with `_True_` meaning “guilty” and `_False_` meaning “innocent” (i.e. _not_ “guilty”). The translation is as follows

1.  `IF(c **and** **not** h, d)` ⇒ if Chase is guilty and Heath is innocent, then Decker is guilty.
2.  `IF(**not** c, **not** m)` ⇒ if Chase is innocent, then Mullaney is innocent.
3.  `IF(h, m)` ⇒ if Heath is guilty, then Mullaney is guilty.
4.  `**not**(c **and** h)` ⇒ Chase and Heath are not both guilty.
5.  `IF(**not** h, **not** d)` ⇒ Unless Heath is guilty, Decker is innocent.

In the above, the clause “_if_ 𝓅 _then_ 𝓆” is implemented in code as follows:  
`IF=**lambda** p, q: **not** p **or** q`.

I tied them all together into the following function:

```
def dwim(c, d, e, h, m):
  IF=lambda p, q: not p or q
  _0=any([c, d, e, h, m])
  _1=IF(c and not h, d)
  _2=IF(not c, not m)
  _3=IF(h, not m)
  _4=not(c and h)
  _5=not h and not d
  if all([_0, _1, _2, _3, _4, _5]):
    print(f'all true when c={c},d={d},e={e},h={h},m={m}')
```

`_0` captures the base condition: at least one of the suspects is guilty.

Once this prep work was done, the only thing left was to find for what values of c, d, e, h, m the entire expression would be true. With 5 variables, we have a mere 2⁵=32 values to run through. That’s done as follows:

```
[dwim(c,d,e,h,m)
     for c in (True, False)
     for d in (True, False)
     for e in (True, False)
     for h in (True, False)
     for m in (True, False)]
```

Sure enough, the answer is spit out:

```
all true when c=✱✱✱,d=✱✱✱,e=✱✱✱,h=✱✱✱,m=✱✱✱
```

Which tells me ██████ guilty and the others innocent.

(I’ve elided the answers so you may, if you so choose, run the code yourself to get the answer. If, for some reason, you want the answer directly, add a comment and I’ll share it there.)

---

Solving puzzles like this is extremely easy but deeply unsatisfying. For one, I, the human, am reduced to a mere translator of problem statement to computer representation. Next, at the end I do not _know_ if the solution is _correct_ or if I just translated the conditions poorly. I don’t know the _reason_, ie _why_ is this answer _the_ answer? If I myself don’t understand it, I cannot explain or justify it to someone else either — and that’s terrible.

In other words, it’s like Machine Learning.
