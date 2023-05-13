---
title: "A pure Java Builder"
description: "In a previous post titled, “Java Curry”, we saw ways to curry ordinary Java methods and constructors. Here, we’ll continue with the same…"
date: "2023-05-13T11:44:38.029Z"
categories: []
published: false
---

In a previous post titled, “[Java Curry](https://medium.com/galileo-onwards/java-curry-997fb357b47e)”, we saw ways to _curry_ ordinary Java methods and constructors. Here, we’ll continue with the same theme but this time in a manner that’s familiar to Java programmers—via the Builder Pattern. In the process we’ll show that the Builder Pattern _just is_ currying but one that abides by the norms of the Java Programming Language.

Now, showing that the Builder Pattern is currying is simple enough so we won’t stop there. Instead, we’ll continue beyond the simple Builder and consider a _pure Builder_. Spoiler: the number of types needed to achieve said purity will be impractical. After considering purity we’ll take a strong stance in favor of side-effects and against purity. But that conclusion will be reached only after much code and discussion.

(I use the word “pure” in its technical sense. A pure function is one whose execution has no side-effects, it doesn’t change the arguments passed to it. A simple example is the `_add_` function which adds two integers. It sums up its arguments and returns their value. In the process, none of the arguments are changed by the function. TK footnote on some concurrent process modifying the arguments.)

So as not to leave you in suspense, we’ll go from a simple Builder all the way to a dynamically-bytecode-generated Builder class. It’ll be fun, I promise.

As with the Java Curry post, all code shown here is meant to be run. The code is always shown with line numbers because Medium doesn’t provide a good code sharing plugin but you should be able to follow along by copy/pasting from the gist at TK.

#### The Builder Pattern: not a tutorial

This post isn’t intended as a tutorial on when and how to use the Builder Pattern in Java. There are vastly other resources which discuss this. A simple internet search (aka google) will give you better resources than I could.

The rest of this post will presume knowledge of the Builder Pattern. It isn’t necessary to know _when_ to use it, just sufficient to know what it is.

Since there are slight variants on how Builders are used, let’s quickly standardize our usage for the rest of this post. (Think of this as determining code style. It really doesn’t matter if you put your Java braces on the same line or the next; except that if you pick one, you use it consistently in your project.)

In our case, we’ll always want to create instances of some class, `C`. Its Builder class will always be created by invoking `C.newBuilder()`, each of the states in `C` will be set by invoking a _setter_ method `builder.setState1(state1);`, `builder.setState2(state2);` and so on. Finally, we’ll actually create an instance of `C` by invoking the `build` method in the Builder class. The general pattern will look something like below:

```
 1 public class C {
 2     public static final class Builder {
 3         private State1 state1;
 4         private State2 state2;
 5         ...
 6         private StateN staten; // not the island
 7 
 8         public Builder setState1(State1 state1) { ... }
 9         public Builder setState2(State2 state2) { ... }
10         ...
11         public Builder setStateN(StateN staten) { ... }
12 
13         // the build method
14         public C build() {
15             ...
16         }
17     }
18     ... // C's internal details and
19         // business logic methods
20 }
```

We won’t care much about `_C_` itself since it’s the Builder we’re interested in. This is akin to the Curry article we didn’t care _what_ the curry was computing—we were only interested in _how_ we could delay, defer, and encapsulate its computation. In this manner, we are no different from most technologies. Sorting algorithms don’t care _what’s_ being sorted, only _how_ to sort them; and if the sort procedure is followed, the results are sorted—[with a few exceptions](https://www.youtube.com/watch?v=Enwbh6wpnYs) TK footnote to [https://www.youtube.com/watch?v=Enwbh6wpnYs](https://www.youtube.com/watch?v=Enwbh6wpnYs). Hashing algorithm discussions don’t care _what_ is hashed, only _how_ its input ought to be hashed. You get the picture.

#### Builders and currying

In both currying and Builders, there’s a final state whose results may not be computed until all necessary components have been added. And in both cases, keeping ourselves to Java, if you attempt to violate this you’ll get a `RuntimeException`. (There are ways to prevent this with Builders about which more later.)

Consider the below code comparing Builders on the left and currying on the right. The currying illustrated is as described in the previous article.

```
 1 class UseBuilder {       | class UseCurry {
 2   public void dwim() {   |   public void dwim() {
 3                          |     Constructor<C> cc = C.class
 4                          |         .getConstructor(
 5                          |             State1.class,
 6                          |             State2.class,
 7                          |             ...,
 8                          |             StateN.class);
 9                          |     Function<State1,
10                          |       Function<State2,
11                          |         ...
12                          |           Function<StateN,
13                          |             Supplier<C>>...> curry
14                          |                 = curry(cc);
15     C c = C.newBuilder() |     C c = curry2.apply(null)
16         .setState1(...)  |         .apply(...)
17         .setState2(...)  |         .apply(...)
18         ...              |         ...
19         .setStateN(...)  |         .apply(...)
20         .build();        |         .get();
21   }                      |   }
22 }                        | }
```

On the left we have the class using a Builder and on the right we have the curry. Except for the extra lines to get `C`’s constructor and curry it (but see next paragraph), the lines to create an instance of `C` are almost exactly the same—lines 15–20.

The curry appears to have 12 extra lines (lines 3–14) getting the constructor from the class `C` which is boilerplate-y but the comparison is unfair because we don’t show the Builder class’s code. Now, as in the Java Curry post, I would never recommend using the curry solution in production (or even in jest) but will recommend using a Builder where applicable.

The above illustration should suffice to show that the curry and the builder are the exact same. It doesn’t matter to us that the builder is typically used to create a new instance of a class whereas the curry is used to defer final computation. Both can be modeled in the same manner and be put to the exact same use which proves our case.

Now, onward to more radical uses of the Builder.

#### Safe Builder?

The simplest incarnation of the Builder is prone to `RuntimeException`s. Justifiably so. Consider the below Builder implementation, especially line 9.

```
 1 public class C {
 2     public static final class Builder {
 3         private State1 state1;
 4         ...
 5         public Builder setState1(State1 state1) { ... }
 6         ...
 7         // the build method
 8         public C build() {
 9             requireNonNull(state1, "state1 was null");
10             ...
11             ... // call C's constructor
12         }
13     }
14     ...
```

If `state1` is `null` the `build()` method throws a `NullPointerException`. This can happen for two reasons only one of which is acceptable. Either, ⒜ the method `setState1` was invoked with a `null` value or ⒝ `setState1` was never invoked at all. In the case of ⒜ we might say that the use of `null` is _understandable_ (though not necessarily justified). Perhaps the library user called `builder.setState1(state1)` and unknown to them, `state1` was `null`.

On the other hand, ⒝ is something we’d like to avoid because it’s something you wouldn’t see happen with a constructor. It isn’t possible to invoke a constructor _without_ passing it an argument (overridden constructors are not considered here).

I’m consciously avoiding discussions of Builders that permit non-invocation of one of the setter methods. That’s a legitimate—in fact, the most common—use of Builders because Builders allow for reasonable defaults. However, this is an exploration of _Pure Builders_, all purity comes from Functional Programming and, quoting from Philip Wadler’s monads [paper](https://homepages.inf.ed.ac.uk/wadler/papers/marktoberdorf/baastad.pdf) (TK), “Pure functional languages have this advantage: all flow of data is made explicit. And this disadvantage: sometimes it is painfully explicit.”

In the functional programming spirit, we will be painfully explicit all the way.

#### Safe Builder I

The best way to prevent early calls to the `build` method is to make it unavailable unless all setters have been invoked. The way to prevent that is to add more types. (This will be a recurring theme through this post. When we run into an issue, we’ll add more types. It’s sort of a mantra.)

Our Builder must not have a `build` method unless all its setters have been invoked. We can model this with the following state machine.

The state machine for a safe builder. This builder uses several intermediate classes each with only one setter method. The setter returns a new object of a different type in a cascading chain. Source: by author. License: public domain.

The Builder itself maintains a cascading series of classes. We have one class per type. In code, that’s…
