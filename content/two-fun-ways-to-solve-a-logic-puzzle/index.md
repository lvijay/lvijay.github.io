---
title: "Two fun ways to solve a logic puzzle"
description: "Prolog and the z3 theorem prover are reliable ways to solve a logic puzzle"
date: "2022-05-15T09:42:42.701Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/logic-puzzle-2-74e0166a4176
redirect_from:
  - /logic-puzzle-2-74e0166a4176
---

This post shows you two programmatic ways to solve logic puzzles, one using the Prolog programming language and the other using the z3 Theorem Prover.

In an [earlier post](https://medium.com/galileo-onwards/boring-logic-5a85da15e748), written almost exactly one year ago today, I brute force solved a simple logic puzzle in Python. In it I also pointed out my solution was poor because although it gave _a_ solution, there was no proper way to confirm that it was _the_ _correct_ solution. The only thing worse than _no_ answer is an answer who's correctness is suspect. After looking at the two solutions, we also discuss why the solutions discussed here are fun but last year’s solution — which also gave the same, correct answer — wasn’t.

Before we jump into the solutions, let’s repeat the problem statement from the previous post. The puzzle is taken from is taken from Hy Conrad’s _Giant Book of Whodunit Puzzles_ (1999, pg 115–6). The title of the puzzle is “Inspector Walker feels the heat”.

A crime has been committed. The police have 5 suspects at least one of whom is guilty. The suspects are Chase, Decker, Ellis, Heath, and Mullaney. The police have acertained the following facts:

⒈ At least one of them is guilty  
⒉ if Chase is guilty and Heath is innocent, then Decker is guilty.  
⒊ if Chase is innocent, then Mullaney is innocent.  
⒋ if Heath is guilty, then Mullaney is guilty.  
⒌ Chase and Heath are not both guilty.  
⒍ Unless Heath is guilty, Decker is innocent.

If you’d like to take a stab at solving the puzzle yourself, pause here, solve it, and then come back.

With that, let’s get to the two solutions.

---

### Theorem Prover

A Theorem Prover is a program that attempts to prove a logical theorem. Given a _true_ _proposition_ (a proposition is a statement with variables) is there an assignment to the variables that makes the entire proposition true? We can illustrate it with some examples. Consider the following trivial equation:

```
a ≡ true
```

The symbol `≡` is _identical to_. Read the above equation as _the variable a is true_. The equation evaluates to `true` if (and only if) we assign `a` the value `true`. Another trivial equation is

```
a and not b ≡ true
```

which works when (and only when) `a=true` and `b=false`. Sometimes a solution is impossible, like in the following case

```
a and not a ≡ true
```

There’s no assignment for `a` that can make the above equation return `true`.

There are more complicated equations — the puzzle we solve in this post is an example.

#### Why true statements?

It is important to theorem provers that they only accept _true_ propositions. The philosopher Bertrand Russell famously showed that a false proposition implies any proposition. When challenged, the story goes, he was able to prove that he and the Pope were the same. The story, repeated below, is taken from [ref](http://ceadserv1.nku.edu/longa//classes/mat385_resources/docs/russellpope.html).

> The story goes that Bertrand Russell, in a lecture on logic, mentioned that in the sense of material implication, a false proposition implies any proposition.  
> A student raised his hand and said “In that case, given that 1 = 0, prove that you are the Pope.”  
> Russell immediately replied, “Add 1 to both sides of the equation: then we have 2 = 1. The set containing just me and the Pope has 2 members. But 2 = 1, so it has only 1 member; therefore, I am the Pope.”

#### Impossible

There’s a famous theorem that shows the problem is unsolvable _in general_. This is called Gödel’s Incompleteness Theorem. It shows that for _any_ given logical system where one can build and prove more and more theorems, there will be a statement that is true but cannot be proven true (or false) by the same logical system. We will not go anywhere near it for two reasons: first, this post’s goal is to solve a simple logic problem; second, I don’t understand the theorem well enough to explain it.

#### Hard Problem

In Computer Science there are problems and there are _hard_ problems. They’re so hard, they’ve got a specific name: _NP-Complete Problems_. It’s been shown that the theorem prover problem (called [_SAT_](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem)) is an NP-Complete problem. So any theorem prover has a hard task cut out for it. A brief summary of NP-Completeness is that an NP-Complete problem’s best solutions° grow exponentially so while solving them is easy for small inputs, they become practically impossible for larger inputs. We won’t run into this problem though, we have merely 5 variables. The earlier statement about NP-Complete problems growing exponentially is unproven but generally accepted as true. If you can prove it (or disprove it), you’ll get [$1 million](https://www.claymath.org/millennium-problems/p-vs-np-problem)¹, and everlasting fame. (For some illustrations of exponential growth, see my [Veda Vyasa takes a break](https://medium.com/galileo-onwards/veda-vyasa-takes-a-break-b7d9cdbd795f).)

### Z3 Theorem Prover

Enter the [Z3 Theorem Prover](https://www.microsoft.com/en-us/research/project/z3-3/) by the fine folks at Microsoft Research. We can use it to solve the puzzle and the beauty of it is the code we write looks almost exactly like the problem statement. I’m sure you have more questions like, Why is it called Z3? What else can I use it for? We will not answer these questions.

#### Solving the problem with Z3

We use Z3’s Python bindings. To install it, use `pip install z3-solver`. The following code block solves the problem:

```
import z3

# In the code Guilty is True and
# Innocent is Not Guilty.

(
    Chase,
    Decker,
    Ellis,
    Heath,
    Mullaney,
) = z3.Bools(
    [
        "Chase",
        "Decker",
        "Ellis",
        "Heath",
        "Mullaney",
    ]
)

s = z3.Solver()

# 1. at least one is guilty
s.add(
    (Chase == True)
    or (Decker == True)
    or (Heath == True)
    or (Mullaney == True)
    or (Ellis == True)
)

# 2. if Chase is guilty
#        and Heath is innocent
#    then Decker is guilty
s.add(
    z3.If(
        Chase == True    # condition
        and Heath != True,
        Decker == True,  # then
        True,            # else
    )
)

# 3. if Chase is innocent
#    then Mullaney is innocent
s.add(
    z3.If(
        Chase != True,
        Mullaney != True,
        True,
    )
)

# 4. if Heath is guilty
#    then Mullaney is guilty
s.add(
    z3.If(
        Heath == True,
        Mullaney == True,
        True,
    )
)

# 5. Chase and Heath are not both guilty
s.add(
    z3.Not(
        Chase == True
        and Heath == True
    )
)

# 6. Unless Heath is guilty
#    then Decker is innocent
s.add(
    z3.If(
        Heath == True,
        True,
        Decker != True,
    )
)
```

z3’s `If` accepts 3 arguments, the _condition_ clause, _then_ clause, and _else_ clause. The code above follows the exact pattern. The only noteworthy item above is ⑹ where, because the rule says _unless_, the consequent is placed in the _else_ clause. The Prolog code below follows the same pattern.

As with the last puzzle, we don’t print the answer here. You may paste it into your Python terminal and request the answer from Z3. First run, `s.check()` and assert that it returns `z3.sat` this ensures that the solver is in a _Satisfiable_ state, i.e., it _has_ a solution. Next, and finally, run `s.model()` to get the answer. The following redacted response is what my Python terminal gives me:

```
>>> s.check()
sat
>>> s.model()
[Ellis = ...,
 Mullaney = ...,
 Chase = ...,
 Decker = ...,
 Heath = ...]
```

### Prolog

The Prolog programming language is among the oldest programming languages still in use — it was invented in 1972. The language is super weird to me as I’m used to the more traditional programming languages like Lisp, Python, Java. Let’s look first at the solution. See **Appendix I** for a brief introduction of the language.

```
% Store the contents in the file named inspector.pro
% Content after a % is a comment
guilty :- true.    % guilty is true
innocent :- false. % innocent is false

solve_inspector(
        Chase,   % tokens starting
        Decker,  % with uppercase
        Ellis,   % are variables
        Heath,
        Mullaney) :-
    % each individual is either
    % innocent or guilty
    (Chase = guilty
    ; Chase = innocent), % ; is OR
    (Decker = guilty
    ; Decker = innocent),
    (Ellis = guilty
    ; Ellis = innocent),
    (Heath = guilty
    ; Heath = innocent),
    (Mullaney = guilty
    ; Mullaney = innocent), 
 
    % at least one is guilty
    (Chase      = guilty
     ; Decker   = guilty
     ; Ellis    = guilty
     ; Heath    = guilty
     ; Mullaney = guilty),

    % if Chase is guilty
    %    and Heath is innocent,
    % then Decker is guilty
    ((Chase = guilty,           % condition
              Heath = innocent)
        -> Decker = guilty      % then
        ; true),                % else

    % if Chase is innocent,
    % then Mullaney is innocent
    (Chase = innocent
        -> Mullaney = innocent
        ; true),

    % if Heath is guilty
    % then Mullaney is guilty
    (Heath = guilty
        -> Mullaney = guilty
        ; true),

    % Chase and Heath
    % are not both guilty
    not(Chase = guilty),
    not(Heath = guilty),

    % Unless Heath is guilty
    % Decker is innocent
    (Heath = guilty
        -> true
        ; Decker = innocent),

    true.
```

Don’t be misled by the `=` in the above code. It isn’t _exactly_ an assignment. It’s a declaration that ought to be read as _suppose Chase = innocent, then find the answer._

The `->` is Prolog’s `IF-Then-Else` operator. `a -> b; c`  
is read as if _a_ then _b_ else _c_.

`,` is Prolog’s AND operator. `a, b` is true if and only if both `a` and `b` are true.

`;` is Prolog’s OR operator. `a; b` is true if one or both of `a` and `b` are true.

Because Prolog is cool, we can declare atoms`guilty` and `innocent` to be the same as Prolog’s builtins `true` and `false`. I have kept the code as close as possible to the clue. For example, I say, `not(Heath = guilty)` though it is equivalently `Heath = innocent`.

Save the above in a file named inspector.pro and start your Prolog interpreter. I used [SWI-Prolog](https://www.swi-prolog.org/) for these problems². (See footnote 2 for an easy way to run Prolog on the browser.)

### Fun vs Boring

The biggest issue I had with the original implementation was I couldn’t convince myself it was the correct answer but both both Prolog and Z3 _do_ function on the principles of logic. All I did was make the statements and they figure out the answer based on the given facts. And that makes a huge difference.

Plus, it helps me that the problem statement and its code representation look so similar.

Prolog and Z3 are similar. Both require facts to be stated to the _system_ (new instances of `z3.Solver` in Z3) and they take care of search. Both systems search on the basis of mathematical logic rules. There are technical differences in their _means_ of search — Prolog uses a depth-first search and Z3 a more modern SAT solving technique called SMT.

I look forward to exploring them and finding uses for them.

### Appendix I

#### A Quick and Dirty Intro to Prolog

This is a lightning fast intro to Prolog. Also, note that my knowledge of the language itself has huge gaps. This isn’t meant to be a comprehensive introduction.

Prolog is a weird mix between a database and a programming language. Where traditional programming languages have statements that are executed, in Prolog, you declare true statements and make queries which the language runtime tries to find the answers to. Prolog has search built into it. The true statements are declared in a file and you make the queries to Prolog’s [Read-Eval-Print Loop](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) (REPL for short). Variables start with uppercase and constants (_atoms_ in Prolog) start with lowercase. Consider the simple case of the SWI-Prolog function `atom-string`. Let’s first look at the code on Prolog’s REPL and then discuss it. Prolog comments start with `%` and I’ve used them to highlight the lines. We’ll discuss them in order.

```
?- atom_string(abcd, S). % 1
S = "abcd".

?- atom_string(A, "abcd"). % 2
A = abcd.

?- atom_string(A, S). % 3
ERROR: Arguments are not sufficiently instantiated
ERROR: In:
ERROR:   [10] atom_string(_4678,_4680)
ERROR:    [9] toplevel_call(user:user: ...) at /.../swi-prolog/8.4.2/libexec/lib/swipl/boot/toplevel.pl:1158

?- A=abcd, S="abcd", atom_string(A, S). % 4
A = abcd,
S = "abcd".

?- atom_string(abcd, "efgh"). % 5
false.
```

The Prolog REPL prompts start with `?-` with the responses on the next line. Prolog statements end with a `.`.

In 1, we call `atom_string` with the atom`abcd` and the variable `S`. Prolog returns `S = "abcd"` indicating that it has _found_ the correct value for the variable `S` to make the input statement _true_. This contrast is highlighed in the next example.

In 2, we call `atom_string` with the string `"abcd"` and the variable `A`. Prolog returns `A = abcd` because that makes the statement true. What happens when we call the function with two variables?

In 3, we call `atom_string` with two variables. Prolog throws an exception because it doesn’t know what to do. [Sherlock Holmes](https://medium.com/galileo-onwards/catch-a-spy-to-enumerate-all-rational-numbers-c3ceb35e87cb) once said, “I am accustomed to have a mystery at one end of my cases, but to have it at both ends is too confusing.” This is Prolog’s equivalent.

In 4, we make a _compound, conjunctive_ statement. We’re asking Prolog, how do you make this entire statement true. The `,` is the AND operator in Prolog. The entire statement says given `A` is the atom `abcd`, `S` the string “abcd”, and `atom_string(A, S)`, is there some assignment to make this true? Prolog says, sure, keep `A = abcd` and `S = "abcd"`. That brings us to 5.

In 5, we make a _false_ statement. We say `atom_string(abcd, "efgh")` which, as we know, isn’t true. The string equivalent of `abcd` is `"abcd"` and the atom equivalent of `"efgh"` is `efgh`. Prolog recognizes, this isn’t possible and returns, `false`.

### Footnotes

¹ The Clay Millenium Prize was [first announced](https://www.claymath.org/millennium-problems/millennium-prize-problems) in May 2000. Since then until now, the prize money hasn’t changed at all. Which means, taking inflation into account, the sooner you solve this problem the better off you are. According to [this website](https://www.in2013dollars.com/us/inflation/2000?amount=1), the purchasing power of a dollar in 2000 is merely 57¢ now.

² SWI-Prolog lets you load files and play with them online. I saved the solution documented in this document at [https://swish.swi-prolog.org/p/inspector.pl](https://swish.swi-prolog.org/p/inspector.pl) but I make no guarantees it’ll work. Anyone can edit it.

[**SWISH -- SWI-Prolog for Sharing**  
_The online Prolog interpretor to solve the logic problem_swish.swi-prolog.org](https://swish.swi-prolog.org/p/inspector.pl "https://swish.swi-prolog.org/p/inspector.pl")[](https://swish.swi-prolog.org/p/inspector.pl)

When I run the code on the above website, I get the results as in the image below. I’ve redacted the correct solution.

The Prolog program when run on the SWI-Prolog website.

³ The earlier blog post where I first solved this logic problem is:

[**The most boring way to solve a logic puzzle**  
_You can brute force the solution to a puzzle but should you?_medium.com](https://medium.com/galileo-onwards/boring-logic-5a85da15e748 "https://medium.com/galileo-onwards/boring-logic-5a85da15e748")[](https://medium.com/galileo-onwards/boring-logic-5a85da15e748)

⁴ The Sherlock Holmes reference to a problem with a mystery at two ends was used and illustrated in:

[**Catch a spy to enumerate all Rational numbers**  
_A puzzle helps us understand the mathematical concept of enumerability._medium.com](https://medium.com/galileo-onwards/catch-a-spy-to-enumerate-all-rational-numbers-c3ceb35e87cb "https://medium.com/galileo-onwards/catch-a-spy-to-enumerate-all-rational-numbers-c3ceb35e87cb")[](https://medium.com/galileo-onwards/catch-a-spy-to-enumerate-all-rational-numbers-c3ceb35e87cb)

⁵ To see some illustrations of exponential growth, see my [Veda Vyasa takes a break](https://medium.com/galileo-onwards/veda-vyasa-takes-a-break-b7d9cdbd795f#7b4a). Specifically, the [animated gif](https://miro.medium.com/max/1400/1*Vx31tNi6VFeWsTg3hti4qA.gif).

[**Veda Vyasa takes a break**  
_Philosopher Jerry Fodor explains how Veda Vyasa, the Mahabharata’s author, bought time from its scribe, the god…_medium.com](https://medium.com/galileo-onwards/veda-vyasa-takes-a-break-b7d9cdbd795f "https://medium.com/galileo-onwards/veda-vyasa-takes-a-break-b7d9cdbd795f")[](https://medium.com/galileo-onwards/veda-vyasa-takes-a-break-b7d9cdbd795f)

⁶ This post’s code, conveniently included in a GitHub Gist is included below.
