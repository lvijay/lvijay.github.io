---
title: "Catch a spy to enumerate all Rational numbers"
description: "A puzzle helps us understand the mathematical concept of enumerability."
date: "2019-04-17T07:28:51.904Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/catch-a-spy-to-enumerate-all-rational-numbers-c3ceb35e87cb
redirect_from:
  - /catch-a-spy-to-enumerate-all-rational-numbers-c3ceb35e87cb
---

_Spy House_ by Banksy¹

Problems in mathematics are often like the following quote by Sherlock Holmes:

> I am accustomed to have a mystery at one end of my cases, but to have it at both ends is too confusing. — _The Adventure of the Illustrious Client (1924)._

The trick to solving such mysteries is to bring down the mystery to only one end. This article hopes to present a case study in this reduction.

### Enumerating the Natural numbers

The set of Natural numbers is defined as all numbers starting from 1 and adding 1 to each successive value. Hence, `1, 1+1(=2), 2+1(=3), 3+1(=4), ...` and so on. Simple enough.

Writing a computer program that does this is equally easy. Here’s an example in the Python programming language:

```
i = 1
while True:
  print(i)
  i = i + 1
```

The program saves 1 into the variable `i`, prints the value of `i`, increments `i` by 1, and repeats. It never stops so unless the program is explicitly stopped or runs out of memory (or the computer it’s running on dies…) it’ll keep printing the Natural numbers, one per line.

Easy enough.

### Enumerating the Integers

Enumerating the Integers is slightly tricker to express algorithmically. (By “algorithmically” we mean elaborating the problem in steps so simple that a computer can follow them.) While humans can understand the infinite series `..., –3, –2, –1, 0, 1, 2, 3, ...` a computer cannot. While a computer can perform _one_ dot-dot-dot (`...`) it cannot do two. This is the first of our Holmesian mystery-on-both-ends. What’s only confusing for Holmes, though, is impossible for a computer.

The mystery is reduced to only one end by counting the negative numbers along with the natural numbers: `0, 1, -1, 2, -2, 3, -3, 4, -4...`. Here it is, again in Python:

```
print(0)
i = 1
while True:
    print(-i)
    print(i)
    i = i + 1
```

We first print `0` (since it has no negative equivalent), then we print the value of `-i`, followed by its positive equivalent, `+i`, then increment `i` and repeat. As earlier, this continues ad infinitum.

### Enumerating the Rational Numbers

The rational numbers are the set of all _fractions_. You know 1, ½, ⅓, ⅔, ⅓, ⅔, ⅕, ⅖, ⅗, ⅘, ⅙, ⅚, ⅛, ⅜, ⅝, ⅞, ¼, ¾, ..., 2, 2⁄2, 2⁄3, 2⁄4, 2⁄5, 2⁄6, 2⁄7, .... But this is tricky. I don’t even know a good way to represent it for humans let alone computers. (And, if you noticed, I didn’t even include negative numbers in that list.)

We can solve the problem by solving the following puzzle. The connection between the puzzle and the rationals may not be immediately obvious but hopefully it will be by the time we solve the puzzle.

---

### Catch the spy

Below is a puzzle from the excellent book, “Algorithmic Puzzles”, by computer scientists Anany Levitin and Maria Levitin (Oxford University Press, 2011)²:

> In a computer game, a spy is located on a one-dimensional line. At time `0`, the spy is at location `a`. With each time interval, the spy moves `b` units to the right if `b≥0`, and `|b|` units to the left if `b<0`. Both `a` and `b` are fixed integers, but they are unknown to you. Your goal is to identify the spy’s location by asking at each time interval (starting at time 0) whether the spy is currently at some location of your choosing. For example, you can ask whether the spy is currently at location 19, to which you will receive a truthful yes/no answer. If the answer is “yes,” you reach your goal; if the answer is “no,” you can ask the next time whether the spy is at the same or another location of your choice. Devise an algorithm that will find the spy after a finite number of questions.

This problem sounds similar to the children’s game where one is blindfolded and has to find, say, a toy. The blindfolded child is then guided by other players who can only say either “warmer”, indicating the child’s close to the target or, “colder”, indicating the opposite. Except, finding the spy is much harder because you’re only told if you’ve hit or missed. Not whether you’re any _closer_ to or _farther_ from the spy.

Let’s consider an example. Suppose the spy picks `a=12` and `b=5`. The spy’s positions are illustrated in the below table. The first column is time, the second the spy’s location at that time. The animated gif image following the table also illustrates the spy’s movement. (All Python code which generated these images is listed at the bottom of this article.)

```
+------+----------+
| time | location |
+------+----------+
|    0 |       12 |
|    1 |       17 |
|    2 |       22 |
|    3 |       27 |
|    4 |       32 |
|    5 |       37 |
|  ... |      ... |
+------+----------+
```A spy’s movement

The spy starts at position 12, then moves to position 17, followed by 22 and so on.

I don’t know about you but my head spins when I think of ways to solve this puzzle. To see why let’s consider an example solution that doesn’t work. Let’s suppose the game starts with `a=114` and `b=469` but I don’t know this and it’s my task to find out.

1.  `time=0` We have to guess _some_ value for `a`. (`b` doesn’t matter because the spy starts at position `a` and only then moves `b` steps.) Let’s guess `a=10`. We get the answer `false` (because the spy is actually at position `114`) and the clock ticks to `time=1`. What do we do next? All we’ve confirmed is that `a_≠_10` but we have no means to confirm if `a` is (or isn’t) any of the other infinite integer values it could be. Let’s soldier on, nevertheless.
2.  `time=1` Let’s suppose now that `a=15` and `b=2`. With these values, the spy must be at location `15+2*1=17`. We ask. We again get the answer `false`.(spy’s actual location: `114+469*1=583`).
3.  `time=2` Maybe last time we got the value of `_a_` right but `_b_` wrong. Let’s keep `a` fixed at `15` and vary `b`. We’ll try `(a=15, b=12)`. Is spy at: `15+12*2=39`? `false`, (spy location: `1052`).
4.  `time=3` Suppose `(a=15, b=26)` Is spy at: `15+26*3=93`? `false`, (spy location: `1521`).
5.  `time=4` Suppose `(a=15, b=-271)`. Is spy at `15-271*4=1069`? `false`, (spy location: `1990`).

When do we stop guessing values of `b` and start varying values of `a`? This is like the joke about the little girl who said, “I know how to spell ‘banana’ but I don’t know when to stop”. How do we proceed when we don’t even know if we’re on the right track? That clock ticking with every guess makes life really, really hard.

I really don’t know how to compute for `a` _and_ `b` when both can be chosen arbitrarily. Truly, a mystery at both ends.

One strategy that commonly works in these puzzles is to simplify the problem. Since both `a` and `b` can vary, we’ll first try to solve the problem by assuming _one_ of them is fixed. There are two cases, then:

Case 1: `b=0` and  
Case 2: `a=0`.

**Case 1:** suppose `b` is zero.  
What strategy could we devise to solve the problem? Once again, choosing an example problem, let’s suppose `a` is 16. The spy would start at position 16 and at each successive step remain at position 16. In other words, the spy doesn’t move at all. In this case, our problem is reduced to trying out every individual number. A spy at position _x_ would be found after approximately _2x_ steps. We would just try the positions as shown below. Alternate rows, prefixed with “time”, show the time starting from zero and other rows, prefixed with “guess”, show the guessed position.

```
time:    0   1   2   3   4
guess:   0  -1   1  -2   2
time:    5   6   7   8   9
guess:  -3   3  -4   4  -5
time:   10  11  12  13  14
guess:   5  -6   6  -7   7
time:   15  16  17  18  19
guess:  -8   8  -9   9 -10
time:   20  21  22  23  24
guess:  10 -11  11 -12  12
time:   25  26  27  28  29
guess: -13  13 -14  14 -15
time:   30  31  32  33  34
guess:  15 -16  16
                ^^
```

As you see above, we encounter the spy at position **16** at time 32, or, after 33 steps (counting 1 for the guess made at time 0).

**Case 2:** suppose `a` is zero.   
When `a` is zero, the spy starts at position 0 followed by `b` and then `b+b`, `2b+b`, and so on. Since the spy always start at position 0 we are guaranteed to guess the spy’s location immediately thus reducing the problem to a triviality. But since we aren’t interested in trivialities let’s assume time starts at 1.

Two illustrations are shown below. Our guessing starts at time=1. We’ll guess all and each of the integers starting 0 (since `b` could be zero). Our guesses are as shown in the two tables below. The values are initialized with `b=8` for the table on the left and `b=-9` for the table on the right. The line at which guesses catch up with the spy are marked with `<<` and `>>` respectively.

```
+------+-----+-------+      +------+-------+
| time | spy | guess |      | spy  | guess |
|      | b=8 |       |      | b=-9 |       |
+------+-----+-------+      +------+-------+
|    1 |   8 |     0 |      |   -9 |     0 |
|    2 |  16 |    -2 |      |  -18 |    -2 |
|    3 |  24 |     3 |      |  -27 |     3 |
|    4 |  32 |    -8 |      |  -36 |    -8 |
|    5 |  40 |    10 |      |  -45 |    10 |
|    6 |  48 |   -18 |      |  -54 |   -18 |
|    7 |  56 |    21 |      |  -63 |    21 |
|    8 |  64 |   -32 |      |  -72 |   -32 |
|    9 |  72 |    36 |      |  -81 |    36 |
|   10 |  80 |   -50 |      |  -90 |   -50 |
|   11 |  88 |    55 |      |  -99 |    55 |
|   12 |  96 |   -72 |      | -108 |   -72 |
|   13 | 104 |    78 |      | -117 |    78 |
|   14 | 112 |   -98 |      | -126 |   -98 |
|   15 | 120 |   105 |      | -135 |   105 |
|   16 | 128 |  -128 |      | -144 |  -128 |
|   17 | 136 |   136 |<<    | -153 |   136 |
|   18 | 144 |       |    >>| -162 |  -162 |
|   19 | 152 |       |      |      |       |
|   20 | 160 |       |      |      |       |
+------+-----+-------+      +------+-------+
```

Observant readers would have noticed that in both cases our _guesses_ remain the same. As with Case 1, we find the spy in approximately `2|b|` _steps_ (the absolute value of b).

Below is an animated gif of capturing a spy with `a=0` and `b=8`. The green line is the spy’s movement and the blue line our guesses. They meet at the same time at position 136.

Catch a spy with a=0, b=8

Similarly, the below gif shows capturing a spy with `a=0` and `b=-9`. The colors are the same as the previous example. Here, the guesses catches up with the spy at position –162.

Catch a spy with a=0, b=–9

#### Solving the puzzle in entirety

Considering the two cases has helped simplify understanding of the problem. One thing that’s now evident over the two cases is that solving for just one variable (either `a` _or_ `b`) is the equivalent of enumerating the natural numbers. We need to come up with a way to enumerate all _pairs_ of numbers in an _algorithmic_ manner so we can guess the spy’s position. Because, if we list every pair `(a, b)`, we just guess that as the spy’s location at the current time and eventually catch that spy. (This realization also shows us the equivalence between the puzzle and enumerating the Rationals.)

Just as we enumerated the negative numbers in pairs, as negative and positive numbers, we must concurrently enumerate values of `a` and `b`. Below’s an illustration of what I mean:

```
(0,0)
(1,0) (1,1)                   ;; (0,1)
(2,0) (2,1) (2,2)             ;; (0,2) (1,2)
(3,0) (3,1) (3,2) (3,3)       ;; (0,3) (1,3) (2,3)
(4,0) (4,1) (4,2) (4,3) (4,4) ;; (0,4) (1,4) (4,2) (3,4)
```

Any pair`(a,b)` is shown grouped together in parentheses, like `(2,3)`. We start at zero, count `b` from zero upwards until `a`, then invert our order: keep `b` at 0, count `a` up from `0`. Then we run the same procedure with `a=1`, `a=2`, and so on. In the examples above, we show fixed `a`’s with increasing `b`’s on the left of the double semicolons (`;;`); and fixed `b`’s with increasing `a`’s on the right of the double semicolons.

For simplicity, this only covers positive pairs but including negative numbers will be straightforward enough. The below animation shows show how we could systematically cover all the numbers. First, just the positive numbers:

Enumerating all positive pairs of (a, b)

We start at `(0, 0)`, move to `(1, 0)`, then `(0, 1)`, and `(1, 1)`. Then we increase `a` to 2 and carry out the rest of the computations. This, as with other computations, continues infinitely.

And the following animation shows what covering _all_ the number pairs entails:

Plotting all integer pairs of (a, b)

We start at `(0, 0)`, thus completing the zeroes. Next, we run through all the ones, starting at `(-1, 1)`, moves eastwards through `(0, 1), (1, 1)` and then moving southwards `(1, 0), (1, -1)`, before moving westwards `(0, -1), (-1, -1)` turn northwards and finish at`(-1, 0)`. We similarly run through the twos, threes and so on forever.

I’m tempted to stop here because it’s like the following joke about the mathematician dousing a fire:

> The Engineer walks in her office and finds her trash can on fire. She gets the fire extinguisher and puts out the fire.  
> The Mathematician walks in his office and finds his trash can on fire. He gets the fire extinguisher and puts out the fire.

> The following day:  
> The Engineer walks in her office and finds the trash can on fire on top of her desk. She gets the fire extinguisher and puts out the fire.  
> The Mathematician walks in his office and finds the trash can on fire on top of his desk. He takes the trash can and puts it on the floor. He has reduced the problem to a previously solved state. To solve it again would be redundant. ³

Like the mathematician, I’ve proved that catching the spy is the same as enumerating all pairs of integers, which is the same as enumerating the Rationals. I _could_ declare Mission Accomplished and stop. But I’ll continue because I’m an engineer discussing mathematics, not a real mathematician.

Let’s now address the puzzle full on. We know the number pairs to consider and the order in which to address them. Below is an example problem solved with `a=2`, `b=3`. It takes 39 steps to find the spy. The table is followed by an animated gif capturing the spy. The animation shows the chosen values for `a` and `b`.

```
+------+-----+-------+
| time | spy | guess |
+------+-----+-------+
|    0 |   2 |     0 |
|    1 |   5 |     1 |
|    2 |   8 |    -2 |
|    3 |  11 |    -3 |
|    4 |  14 |     1 |
|    5 |  17 |    -1 |
|    6 |  20 |     7 |
|    7 |  23 |    -6 |
|    8 |  26 |     7 |
|    9 |  29 |    18 |
|   10 |  32 |   -20 |
|   11 |  35 |   -22 |
|   12 |  38 |     2 |
|   13 |  41 |    -2 |
|   14 |  44 |    29 |
|   15 |  47 |   -29 |
|   16 |  50 |    31 |
|   17 |  53 |   -35 |
|   18 |  56 |    20 |
|   19 |  59 |   -17 |
|   20 |  62 |    18 |
|   21 |  65 |   -23 |
|   22 |  68 |    46 |
|   23 |  71 |   -44 |
|   24 |  74 |    46 |
|   25 |  77 |    75 |
|   26 |  80 |   -78 |
|   27 |  83 |   -81 |
|   28 |  86 |     3 |
|   29 |  89 |    -3 |
|   30 |  92 |    91 |
|   31 |  95 |   -92 |
|   32 |  98 |    95 |
|   33 | 101 |  -100 |
|   34 | 104 |    37 |
|   35 | 107 |   -32 |
|   36 | 110 |    33 |
|   37 | 113 |   -40 |
|   38 | 116 |   116 |<<<
+------+-----+-------+
```Catch the spy with a=2, b=3

The next graph is the über graph—the graph to catch all spies. It plots time on the horizontal axis and the spy’s position at that time on the vertical axis.

The graph to catch every spy

#### When will it finish?

Recall the _last_ sentence from the puzzle:

> Devise an algorithm that will find the spy after a finite number of questions.

It isn’t an algorithm unless it terminates in finite time. The question then, is, in how much time is our system guaranteed to find the spy? Our enumeration series goes as shown below. Each row has an increasing number of pairs which go as shown below.

```
0: ( 0, 0)

1: (-1, 1), ( 0, 1), ( 1, 1), ( 1, 0),
   ( 1,-1), ( 0,-1), (-1,-1), (-1, 0)

2: (-2, 2), (-1, 2), ( 0, 2), ( 1, 2),  
   ( 2, 2), ( 2, 1), ( 2, 0), ( 2,-1),
   ( 2,-2), ( 1,-2), ( 0,-2), (-1,-2),
   (-2,-2), (-2,-1), (-2, 0), (-2, 1)

3: (-3, 3), (-2, 3), (-1, 3), ( 0, 3),
   ( 1, 3), ( 2, 3), ( 3, 3), ( 3, 2),
   ( 3, 1), ( 3, 0), ( 3,-1), ( 3,-2),
   ( 3,-3), ( 2,-3), ( 1,-3), ( 0,-3),
   (-1,-3), (-2,-3), (-3,-3), (-3,-2),
   (-3,-1), (-3, 0), (-3, 1), (-3, 2)

4: (-4, 4), (-3, 4), (-2, 4), (-1, 4),
   ( 0, 4), ( 1, 4), ( 2, 4), ( 3, 4),
   ( 4, 4), ( 4, 3), ( 4, 2), ( 4, 1),
   ( 4, 0), ( 4,-1), ( 4,-2), ( 4,-3),
   ( 4,-4), ( 3,-4), ( 2,-4), ( 1,-4),
   ( 0,-4), (-1,-4), (-2,-4), (-3,-4),
   (-4,-4), (-4,-3), (-4,-2), (-4,-1),
   (-4, 0), (-4, 1), (-4, 2), (-4, 3)

5: (-5, 5), (-4, 5), (-3, 5), (-2, 5),
   (-1, 5), ( 0, 5), ( 1, 5), ( 2, 5),
   ( 3, 5), ( 4, 5), ( 5, 5), ( 5, 4),
   ( 5, 3), ( 5, 2), ( 5, 1), ( 5, 0),
   ( 5,-1), ( 5,-2), ( 5,-3), ( 5,-4),
   ( 5,-5), ( 4,-5), ( 3,-5), ( 2,-5),
   ( 1,-5), ( 0,-5), (-1,-5), (-2,-5),
   (-3,-5), (-4,-5), (-5,-5), (-5,-4),
   (-5,-3), (-5,-2), (-5,-1), (-5, 0),
   (-5, 1), (-5, 2), (-5, 3), (-5, 4)

6: (-6, 6), (-5, 6), (-4, 6), (-3, 6),
   (-2, 6), (-1, 6), ( 0, 6), ( 1, 6),
   ( 2, 6), ( 3, 6), ( 4, 6), ( 5, 6),
   ( 6, 6), ( 6, 5), ( 6, 4), ( 6, 3),
   ( 6, 2), ( 6, 1), ( 6, 0), ( 6,-1),
   ( 6,-2), ( 6,-3), ( 6,-4), ( 6,-5),
   ( 6,-6), ( 5,-6), ( 4,-6), ( 3,-6),
   ( 2,-6), ( 1,-6), ( 0,-6), (-1,-6),
   (-2,-6), (-3,-6), (-4,-6), (-5,-6),
   (-6,-6), (-6,-5), (-6,-4), (-6,-3),
   (-6,-2), (-6,-1), (-6, 0), (-6, 1),
   (-6, 2), (-6, 3), (-6, 4), (-6, 5)
```

The number of pairs in each row goes 1, 8, 16, 24, 32, 40,…. In other words, multiples of 8. This is an _arithmetic progression_ whose sum evaluates to `1+n×(n+1)÷2`.

An interesting thing to note here is that the time it takes us to catch a spy with `a=314, b=271` is approximately the same as catching a spy with `a=271, b=314` which is the same as catching a spy with `a=-271, b=314` and so on. In all cases, it depends on the _higher_ of the _absolute_ values of `a` and `b`.

To pick an example, if the spy started with the values `a=4`, `b=-8`, we take the higher value in absolute terms (i.e. we disregard the negative sign), which is 8. We’ll first run through all the pairs upto 7. That’ll take us 225 steps (since `225 = 1+224 = 1+(7*8/2*8)`and then take a maximum of 64 steps to catch the spy. Simplifying for the worst case, we have our formula as shown in Python below:

```
def num_steps(a, b):
  bigger = max(abs(a), abs(b))
  round_up = bigger + 1
  step_count = 8 * round_up * (1 + round_up) / 2
  return step_count
```

The Python function `abs` returns the absolute value of its argument (thus, `abs(9) = abs(-9) = 9`). We calculate `bigger` which stores the bigger of the two arguments `a`, `b`. So, given `a=-19`, `b=18`, `bigger` will contain `+19`. Since we’re considering the worst case, we save one plus bigger in the variable `round_up` (iow, we _round up_ bigger). Then the number of steps is calculated as shown.

With the original examples a=314, b=271, it’ll take us 398160 steps to capture the spy. That’s a lot of steps but we’re guaranteed to capture the spy.

In technical terms, the time of complexity of this algorithm is `Θ(n²+3n)` where `n` is the maximum of the absolute values of `a`, `b`.

---

#### The Rational Numbers Redux

At first glance it might not be obvious how the spy puzzle is related to the rational numbers but the confusion is quickly resolved if we make the following two changes the pairs `a` and `b`.

1.  we remove pairs that have `b=0` and
2.  we replace the commas with slashes thereby making the pairs to fractions:`(a, b) → a/b`. For example,  
    • (1,2) → ½  
    • (0,3) → ↉  
    • (3,8) → ⅜.

We get the below fractions by enumerating all fractions until 4. Note, they are not normalized but just shown as is. Normalizations come after.

```
0: 0/1, 0/-1
1: 1/1, 1/-1, -1/1
2: 0/2, 0/-2, 1/2, 1/-2, -1/2, 2/1, 2/-1, -2/1, -2/-1, 2/2, 2/-2, -2/2
3: 0/3, 0/-3, 1/3, 1/-3, -1/3, 3/1, 3/-1, -3/1, -3/-1, 2/3, 2/-3, -2/3, 3/2, 3/-2, -3/2, -3/-2, 3/3, 3/-3, -3/3
4: 0/4, 0/-4, 1/4, 1/-4, -1/4, 4/1, 4/-1, -4/1, -4/-1, 2/4, 2/-4, -2/4, 4/2, 4/-2, -4/2, -4/-2, 3/4, 3/-4, -3/4, 4/3, 4/-3, -4/3, -4/-3, 4/4, 4/-4, -4/4
```

When normalized—sorted, deduplicated, negatives resolved—we see that Step Zero remains zero; Step One includes 1, –1; Step Two gives us half steps from –2 all the way to +2; Step Three gives all steps from negative three to three; and so on. The normalized values are again shown below as a not-to-scale triangle.

```
0:                              0
1:            -1                0             1
2:    -2      -1      -1/2      0     1/2     1     2
3:   -3 -3/2  -1  -2/3 -1/3     0   1/3 2/3   1  3/2 3
4: -4 -2 -4/3 -1 -3/4 -1/2 -1/4 0 1/4 1/2 3/4 1 4/3 2 4
```

While level 2 did not contain the intermediary between –2 and –1, we can see it was filled in level 3. Similarly all gaps will be filled with progressive increases in values. This is illustrated by the two animations below.

The rationals in the range -17 to +17Closer view of the rationals in the same range as above

The first image shows all the rationals computed in the range –17 to +17. The second image shows the same rationals but focuses on only the values between –2 and +2.

Because the lines are so messy, here’s the same graph but it plots each iteration separately. This goes from the range –20 to +20.

All Rationals

Again, showing the entire set but focusing on the range –2, 2:

The rational numbers in the range -2 to +2 with a high resolution. We plot all rationals from -20 to +20 but only focus on a smaller area.

While the smaller numbers fill up first, note that all ranges get filled albeit later. Here’s the above graph but focusing on the range –4, –2.

The rational numbers in the range -4 to -2. We plot rationals from -80 to +80 but focus on a smaller area. Note the asymmetry between the left and right sides of the image. The dots on the right side converge quicker than the dots on the left.

Note the asymmetry between the left and right sides of the image. The dots on the right side converge quicker than the dots on the left, i.e. the dots on the right side are closer to one another than the dots on the left side. They too will get filled with the rational numbers.

With larger and larger ranges, more and more of the number line will get filled. But will it fill _all_ of the number line?

#### Irrational numbers

Though the Rational numbers will cover many (_infinite_) values, there will still be gaps. Numbers such as `√2, √3, ∜5, ∛7` will be absent. As will numbers like π, e, δ, and Ω. The _ir_rational numbers are defined as numbers which cannot be represented as a fraction of natural numbers.

Can we cover these too using the above techniques? The answer is no. While the former set of numbers (the roots) are, _I think_, enumerable, enumeration of the latter category of numbers is impossible. I don’t use the word lightly but in its true technical sense.

In 1874, the mathematician Georg Cantor proved there are infinities and there are _infinities_. He showed that while the _count_ of natural numbers is the same as the count of integers which is the same as the count of the rationals, there are _more_ irrational numbers than there are _enumerable_ numbers. Cantor loved his finding so much he proved this same truth multiple times each time using different techniques.

The proof of that I leave for another day.

#### Mystery tied up

In _The Adventure of the Illustrious Client_ the client’s identity is never revealed to Sherlock Holmes but, being Sherlock Holmes, both solves client’s mystery and deduces his identity. Here, we’ve solved our own mystery-on-two-ends by considering them as one mystery at a time and then, with the learnings from each, unified them into a solution. The master detective would’ve been impressed.

### Footnotes

¹ Cover image: _Spy House_ by Banksy. Picture taken from [https://uncrate.com/banksy-house/](https://uncrate.com/banksy-house/).

² “Algorithmic Puzzles” by Anany Levitin and Maria Levitin, published 2011 Oxford University Press. [https://global.oup.com/academic/product/algorithmic-puzzles-9780199740444](https://global.oup.com/academic/product/algorithmic-puzzles-9780199740444?cc=us&lang=en&).

³ “Science humor collected by Joachim Verhagen”, §6.2 Fire [https://jcdverha.home.xs4all.nl/scijokes/6\_2.html](https://jcdverha.home.xs4all.nl/scijokes/6_2.html). Slightly modified.

⁴ The files which generated the above animated GIFs are available at the following GitHub Gist. As a warning, please note that in addition to the common NO WARRANTY clauses of all Free Software projects, I will add that these files aren’t even guaranteed to work. This is because I edited the files, opened the generated GIF in my browser, eyeballed the image, and then added it to this article.
