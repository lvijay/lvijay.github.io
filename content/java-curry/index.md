---
title: "Java Curry"
description: "A demonstration of currying in the Java Programming Language."
date: "2019-07-30T01:18:19.428Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/java-curry-997fb357b47e
redirect_from:
  - /java-curry-997fb357b47e
---

Another commercial variant of Java Curry manufactured by the Japanese corporation, House Foods. Image taken from their [website](https://housefoods-group.com/products/en/catalog/java/hot.html).

A curried function is a function that accepts _n_ arguments of which up to _n–1_ arguments have already been filled in. Think of it as preparing some curried rice. A single curry does not a meal make but it’s most of one. You add the remaining ingredients and lo, presto, you have a whole meal. With such a great analogy, you’d think that’s the origin of the term but no, it’s named after the mathematician and logician, Haskell Curry. Curry himself credited the mathematician and logician, Moses Schönfinkel, as the first person (in 1923) to use the concept and that he only independently discovered it.

Back to currying, then. Let’s consider an example. We want to measure the time it takes for a stone to drop from various heights. For simplicity, we’re going to ignore the effects of air resistance. Let’s suppose the stone’s height is represented by the variable `_s_` and acceleration due to gravity is represented by the variable `_g_`. The time taken is simply `+√2√s/√g`. In words, it is the positive square root of the distance divided by the positive square root of the acceleration due to gravity.

Below is a simple code sample in Python 3.

```
def time_taken(s, g):
    return (2 * s / g) ** 0.5
```

We define a function named `time_taken` which accepts two parameters, `s` and `g`. The function divides `s` by `g` and returns their square root. Simple enough, what’s the problem?

Suppose that you now want to provide a function that measures how long it would take to drop from a _fixed_ height on different astronomical bodies. You’d like an easy way to measure the time it would take to drop a hundred meters on earth, Mars, Venus, the sun, the moon, Jupiter’s moons Ganymede, Io, and so on. And, being a programmer, you don’t want to pass the value _100_ to the function each time because that’s repetitive and boring. You’d like to have a function named (perhaps poorly), `_time_taken_100_`. Below is an easy way to achieve this:

```
def time_taken_100(g):
    return time_taken(100.0, g)
```

Congrats, you’ve just _curry_’d the `_time_taken_` function. It doesn’t have to stop here, of course. You could just as easily write a function, `time_taken_earth` which, given a distance, computes the time taken for an object to fall on earth. It would be as simple as:

```
def time_taken_earth(s):
    return time_taken(s, 9.8)
```

It’s easy to imagine how useful such a capability is. Languages like Haskell partially offer this feature for free. (Yes, the language _is_ named after Haskell Curry.)

#### What would it take to do this in the Java programming language?

Below is a simple program which demonstrates currying in Java. Note that, for illustrative purposes, I’ve added line numbers to each line. While this is great for explanatory purposes, it makes copying the code a chore. To run this code (strongly encouraged) all the code shown in this article is available as a [gist](https://gist.github.com/lvijay/f3c95f1944b895df1b9f30c682b95b2c).¹

```
 1 import java.util.function.Function;
 2 
 3 public class Currier0 {
 4   public static String concat(String s, Integer i, Integer j) {
 5     return s + i + j;
 6   }
 7 
 8   public static
 9       Function<String,
10           Function<Integer,
11               Function<Integer, String>>> curry() {
12     return s -> (i -> (j -> concat(s, i, j)));
13   }
14 
15   public static void main(String[] args) {
16     String direct = concat("hello", 12345, 67890);
17     System.out.println(direct); // prints hello1234567890
18 
19     String curried = curry()
20         .apply("hello")
21         .apply(12345)
22         .apply(67890);
23     System.out.println(curried); // prints hello1234567890
24   }
25 }
```

Apart from the `main` method, it defines two methods, `concat` and `curry`, defined on lines 4 and 11 respectively. The `concat` method accepts three arguments, a `String` and two `Integer`s. It concatenates them and, (thanks to Java’s automatic type conversion), returns a `String` object. An example invocation of `_concat_` is shown on line 16 where the result is stored in the variable `direct`. Its result is printed to the console on line 17 and is also shown in the comment. It prints `hello1234567890`.

The `curry` function’s body is almost as terse as the `concat` method itself. It delegates to the `concat` method for actual processing too. If anything, `_curry_`’s return type is what’s complicated. It returns (hold your breath) a function which accepts a string and returns a function which accepts an integer and returns a function which accepts an integer and returns a string. If you understood that on first pass, give yourself a pat on the back. You probably don’t need this post. To readers familiar with typed functional programming languages like Haskell, ML, OCaml, the Java syntax will appear familiar. In fact, the method body in `curry` —`s -> (i -> (j -> ...))`—looks exactly like in those languages except there the parentheses would be superfluous because functions are naturally right associative. In Java the explicit grouping is mandatory for syntactic reasons.

To better understand what curry does, it might help to break it down. Try running the following variations:

```
... elided ...
public static void main(String[] args) {
  Function<String,
    Function<Integer,
      Function<Integer, String>>> curried = curry();
  System.out.println(curried);
  System.out.println(curried.apply("e"));
  System.out.println(curried.apply("e").apply(27));
  System.out.println(curried.apply("e").apply(27).apply(18));
}
```

Depending on your jdk, your output will look something like below. Note that the last output should always be the same.

```
Currier0$$Lambda$1/0x0000000800060840@64b8f8f4
Currier0$$Lambda$2/0x0000000800062840@1996cd68
Currier0$$Lambda$3/0x0000000800062c40@555590
e2718
```

Above is an output from openjdk11. Notice that the first 3 lines are all Java _lambdas_. What’s happening is that each invocation of the variable `curried` returns another lambda until finally, when it has all the variables it needs, it delegates to the original method, (`concat`, in this case) and returns the result (`e2718`, in this case).

#### Curry next step: a programmatic skeleton

Hopefully, the steps so far are clear. While Currier0.java does the trick and is straightforward it’s also unsatisfying. It’s easy to write `a -> b -> c -> ... -> m -> doIt(a, b, c, ..., m)` when we already know the `a, b, ..., m` what we’d really like is to programmatically generate the curry.

Let’s start slowly. Early abstraction, like premature optimizations, is a root of much evil. Presented below is Currier1.java. Its currying function is named `curry1`(line 17). It accepts a `java.lang.reflect.Method` from which it programmatically generates a curried function. We’ll discuss the details after the code block below.

```
 1 import java.lang.reflect.InvocationTargetException;
 2 import java.lang.reflect.Method;
 3 import java.util.function.Function;
 4 
 5 public class Currier1 {
 6   public static final class Distance {
 7     public double distance(double t, double v, double u) {
 8       return v * t + 0.5 * u * t * t;
 9     }
10   }
11 
12   public static String concat(String s, int i, int j) {
13     return s + i + j;
14   }
15 
16   @SuppressWarnings("rawtypes")
17   static Function curry1(Method method) {
18     return (Function) (Object s) -> {
19       Object self = s;
20       Object[] args = new Object[3];
21       return (Function) (Object i) -> {
22         args[0] = i;
23         return (Function) (Object j) -> {
24           args[1] = j;
25           return (Function) (Object k) -> {
26             args[2] = k;
27             try {
28               return method.invoke(self, args);
29             } catch (IllegalAccessException e) {
30               throw new RuntimeException(e);
31             } catch (InvocationTargetException e) {
32               throw new RuntimeException(e.getCause());
33             }
34           };
35         };
36       };
37     };
38   }
39 
40   public static void main(String[] args) throws Exception {
41     Method concatM = Currier1.class.getMethod(
42         "concat", String.class, int.class, int.class);
43     @SuppressWarnings("unchecked")
44     Function<Void,
45         Function<String,
46             Function<Integer,
47                 Function<Integer, String>>>> curry1 = curry1(concatM);
48     String curried1static = curry1
49         .apply(null) // static methods take no instance
50         .apply("hello")
51         .apply(12345)
52         .apply(67890);
53 
54     System.out.println(curried1static); // prints hello1234567890
55 
56     Method distM = Distance.class.getMethod(
57         "distance", double.class, double.class, double.class);
58     @SuppressWarnings("unchecked")
59     Function<Distance,
60         Function<Double,
61             Function<Double,
62                 Function<Double, Double>>>> instanceCurry = curry1(distM);
63     Distance cm = new Distance();
64     Double distance = instanceCurry
65         .apply(cm)
66         .apply(1.0d)  // t
67         .apply(2.0d)  // v
68         .apply(10.0d); // u
69     System.out.println(distance); // prints 7.0
70   }
71 }
```

The `curry1` method takes a Java reflection class, `Method`, and from it generates a `Function`. A quick word about how Method works. It represents the _method_ whose behavior we wish to dynamically execute. Any Java method is typically invoked as `instance.dwim(arg1, arg2, arg3, .., argN)` where `instance` is the object that invokes the method `dwim` (shorthand for [do-what-i-mean](https://en.wikipedia.org/wiki/DWIM)²) with its arguments. For Method to function (no pun intended), it inverts this order slightly. The _Method_ class has a _method_ named `invoke` with the following signature

`public Object invoke​(Object obj, Object… args)` [³](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/reflect/Method.html#invoke%28java.lang.Object,java.lang.Object...%29)

Where,  
`obj`\- the object the underlying method is invoked from; and  
`args`\- the arguments used for the method call.

Thus, instead of `obj.dwim(arg1, arg2, ..., argN)`, given a Method, `m`, you’d say, `m.invoke(obj, new Object[] { arg1, arg2, ..., argN })`. ⁴

Back to the `_curry1_` function then. The first invocation to `curry1` (strictly speaking, the invocation on the _first function_ returned by `curry1` but I’ll use the more colloquial terms in the rest of this text), is “the object the underlying method is invoked from”. We save it into a variable named `self`. All subsequent calls are stored into an `Object` array. For simplicity, in this iteration (Currier1) we use a fixed array of size 3.

Below, I’ve repeated `curry1`, line numbers and everything, with added annotations. At each stage—lines 18, 21, 23, 25, and 28—we return a Java lambda Function representing each curried state. `Method::invoke` throws a few checked exceptions so we have code to handle those too

```
17   static Function curry1(Method method) {
18     return (Function) (Object s) -> {
19       Object self = s;
20       Object[] args = new Object[3];
21       return (Function) (Object i) -> {
22         args[0] = i; // save first argument
23         return (Function) (Object j) -> {
24           args[1] = j; // save second argument
25           return (Function) (Object k) -> {
26             args[2] = k; // save third argument
27             try {
28               return method.invoke(self, args); // invoke!
29             } catch (IllegalAccessException e) {
30               throw new RuntimeException(e);
31             } catch (InvocationTargetException e) {
32               throw new RuntimeException(e.getCause());
33             }
34           }; // these close braces look like lisp code
35         };
36       };
37     };
38   }
```

To show that `curry1` is generic enough for all methods that accept 3 arguments we have two samples in our code (repeated below). One is the method `concat`(line 12), copied from Currier0 and the other is the method `distance` from the custom class `Distance`(line 6). These two examples show that we can curry both static methods and instance methods (methods that require an object to work). We’ll look at how they are curried and invoked after the below code box.

```
 6   public static final class Distance {
 7     public double distance(double t, double v, double u) {
 8       return v * t + 0.5 * u * t * t;
 9     }
10   }
11 
12   public static String concat(String s, int i, int j) {
13     return s + i + j;
14   }
```

Below is the class’s _main_ method. We first look at the same example as Currier0, `concat`. At line 41, we reflectively retrieve the method. In line 47 we capture the curried instance in a variable named `curry1`. Note that thanks to Java’s automatic type inference we capture the return type. (Note also that since Java lacks reified generics, it will happily assign any given type specification to the variable and blow up at runtime if you make a mistake.) From lines 48–52 we invoke the curried method. The method’s arguments should be familiar from Curried0, the difference here is the specification of `obj`. Since `concat` is a static method, we pass `_null_`. (The type specification on line 44 also lists it as `Void`.) We’ll look at invoking the instance method after looking at the entire `_main_` method’s code.

```
40   public static void main(String[] args) throws Exception {
41     Method concatM = Currier1.class.getMethod(
42         "concat", String.class, int.class, int.class);
43     @SuppressWarnings("unchecked")
44     Function<Void,
45         Function<String,
46             Function<Integer,
47                 Function<Integer, String>>>> curry1 = curry1(concatM);
48     String curried1static = curry1
49         .apply(null) // static methods take no instance
50         .apply("hello")
51         .apply(12345)
52         .apply(67890);
53 
54     System.out.println(curried1static); // prints hello1234567890
55 
56     Method distM = Distance.class.getMethod(
57         "distance", double.class, double.class, double.class);
58     @SuppressWarnings("unchecked")
59     Function<Distance,
60         Function<Double,
61             Function<Double,
62                 Function<Double, Double>>>> instanceCurry = curry1(distM);
63     Distance cm = new Distance();
64     Double distance = instanceCurry
65         .apply(cm)
66         .apply(1.0d)   // t
67         .apply(2.0d)   // v
68         .apply(10.0d); // u
69     System.out.println(distance); // prints 7.0
70   }
71 }
```

If you understood the static method, the instance method shouldn’t look too different. In lines 56–57, we retrieve the `distance` method. We capture the curry in lines 59–62 in the variable `instanceCurry`. Unlike the static method, we create an instance of the `_Distance_` class in line 63 and pass this to the curry. Lines 64–68 show the curry invocation. It’s the same as with the static method except with different types and, of course, a different result.

#### Curry 2: a generic solution

Curried1 is a big step over Curried0. It curries over all arbitrary methods that accept exactly 3 arguments. In this next iteration, Curried2, we curry all methods. Below is the full code. In this iteration, I won’t go through `concat` or `main`. They are both sufficiently similar to the previous two versions. What’s interesting here is the `curry2` method. Let’s look at that after the full code snippet.

```
 1 import java.lang.reflect.InvocationTargetException;
 2 import java.lang.reflect.Method;
 3 import java.util.function.Function;
 4 import java.util.function.Supplier;
 5 
 6 public class Currier2 {
 7   public static String concat(String s, Integer i, Integer j) {
 8     return s + ":" + i + ":" + j;
 9   }
10 
11   @SuppressWarnings("unchecked")
12   public static void main(String[] args) throws Exception {
13     Method concatM = Currier2.class.getMethod(
14         "concat", String.class, Integer.class, Integer.class);
15     Function<Currier2,
16         Function<String,
17             Function<Integer,
18                 Function<Integer, String>>>> curry2 = curry2(concatM);
19     String concatted = curry2
20         .apply(null)
21         .apply("hello")
22         .apply(12345)
23         .apply(67890);
24 
25     System.out.println(concatted); // prints hello:12345:67890
26   }
27 
28   @SuppressWarnings("rawtypes")
29   public static Function curry2(Method method) {
30     int parameterCount = method.getParameterCount();
31 
32     Function f = o -> {
33       Object self = o;
34       Object[] args = new Object[parameterCount];
35 
36       Supplier<?> c = () -> {
37         try {
38           return method.invoke(self, args);
39         } catch (IllegalAccessException e) {
40           throw new RuntimeException(e);
41         } catch (InvocationTargetException e) {
42           throw new RuntimeException(e.getCause());
43         }
44       };
45 
46       if (parameterCount == 0) {
47         return c.get();
48       }
49 
50       Function[] fns = new Function[parameterCount];
51 
52       for (int i = 0; i < parameterCount - 1; ++i) {
53         int j = i;
54         fns[i] = v -> {
55           args[j] = v;
56           return fns[j + 1];
57         };
58       }
59 
60       fns[parameterCount - 1] = a -> {
61         args[parameterCount - 1] = a;
62         return c.get();
63       };
64 
65       return fns[0];
66     };
67 
68     return f;
69   }
70 }
```

`curry2` looks different but is largely the same as `curry1`. The difference here is that we can’t beforehand code for how many arguments _method_ expects. It could be anywhere between 0 and 255[⁵](https://docs.oracle.com/javase/specs/jvms/se11/html/jvms-4.html#jvms-4.11). While 255 is a pretty small number and we could just `**_switch/case_**` it in, what’s the fun in that?

First, in line 30, we capture how many parameters the method needs. We save it in the variable `parameterCount`. Next, we prepare the Function `f`. We will return this variable. Like all `java.util.function.Function`’s, it expects a single parameter. This first parameter is always the invoker object. We save that as `Object self` in line 33. Line 34 creates an object array, `args`, representing all arguments the method needs. If `method` expects no arguments, `parameterCount` will be `0` and `args` will be an empty array.

Lines 36–44 look a bit out of place so I’ll spend a little time explaining them. A `_Supplier_` is a functional interface introduced with Java 8. Its abstract method, `get`, takes no arguments and returns a value. It may be invoked multiple times. In our case, the Supplier captures a way of (for lack of a better term) _invoking_ `Method::invoke`. It lexically captures `method`, `self`, and `args`, so it can, on demand, execute `Method::invoke`. Additionally, it also handles the checked exceptions thrown by `Method::invoke`.

The purpose of the Supplier is explained by the `if` clause on line 46. For cases where `method` requires no arguments and `self` is instantiated we should just return the result of the method invocation. And that’s what we do on line 47.

If `method` does require more than one argument, we now create an array of `Function`’s (line 50), each invoking the function next in line⁶—lines 52–58. The last function (line 60–63) invokes `Supplier::get`. The first responsibility of every function’s definition is to capture its parameter and save it in `args`—lines 55, 61. The seemingly useless assignment on line 53, `int j = i;`, is needed because all variables referenced within lambdas must be _effectively final_. That’s a way of saying that the reference must never change during its lifetime though its value might. (In this case, since `i` is a primitive there’s no reference hence it must not change at all.)

With that we have a fully generic currying class. We’re _almost_ done.

### **The 3 stages of currying**

Let’s take a brief stop to generalize what we’ve learnt about currying _implementations_.

All currying implementations have three stages — initial, intermediate, and final.

The first call to the curry method is the _initial stage_. In it, invokers pass to us the information of who is calling the curry. It is `null` for methods and `obj` for instance methods. The _intermediate stages_ involve capturing all the arguments needed for the curried function and the _final stages_ represents actual invocation of the curried function. Typically, the final stage involves both capturing the parameter and making the invocation. (Because otherwise the curry invocation, instead of `curry.apply(1).apply(2).apply(n)`, will look like `curry.apply(1).apply(2).apply(n).**_accept_**()`, and we can’t have that!)

With that, we’re ready for…

#### Curry 3: generic, lazy, shareable, type-inferencing, Executable and thread-safe

Currier2 is great. It works for all practical purposes. What does it miss?

While I stand by my recommendation in the [README](https://gist.github.com/lvijay/f3c95f1944b895df1b9f30c682b95b2c#file-readme-md): “No part of this is actually recommended for use in a production system”, it still would be amiss to write thread-unsafe code. Additionally, observant readers would’ve noticed that there’s no principled reason to exclude constructors from the curry mix (okay, slight pun intended).

Since [Currier3.java](https://gist.github.com/lvijay/f3c95f1944b895df1b9f30c682b95b2c#file-currier3-java) is 156 lines, I don’t print it in entirety. In the spirit of Test Driven Development (TDD), let’s first look at the file’s skeleton, then the `_main_` method (which has the tests), before looking its implementation itself.

Like the earlier curry methods, this one also uses the static factory method. You invoke `curry3` with a `Method` (line 17–19) or with a `Constructor`(line 21–24). Luckily for us, Java 1.8 introduced the abstract class Executable as a parent of both Method and Constructor simplifying our implementation.

The `FunctionE` (Function with _E_nvironment) class implements Java’s `Function` interface. It’s declaration alone is shown on line 26. We’ll look at it in detail presently.

The `_main_` method should look familiar to previous versions. The only difference is currying an object constructor so that alone is shown. Refer the [gist](https://gist.github.com/lvijay/f3c95f1944b895df1b9f30c682b95b2c#file-currier3-java-L101) for details. In line 145, we find the String constructor that accepts `byte[]` and `Charset`. We curry it into variable `c3cons` on lines 147–149 and execute it. For its execution we use some byte encoding magic to read one string in one encoding (ISO-8859–1) and output in another (UTF-8). The output uses Unicode characters that (imo) read “curry”. The encoding is not discussed here but left as exercise.

```
  1 import static java.nio.charset.StandardCharsets.ISO_8859_1;
  2 import static java.nio.charset.StandardCharsets.UTF_8;
    
    ... remaining imports elided ...
    
 16 public final class Currier3 {
 17   public static <T, R> Function<T, R> curry3(Method method) {
 18     return new FunctionE<>(method);
 19   }
 20 
 21   public static <T, R, K extends T> Function<T, R>
 22           curry3(Constructor<K> constructor) {
 23     return new FunctionE<>(constructor);
 24   }
 25 
 26   private static final class FunctionE<T, R> implements Function<T, R> {
      ... described later ...
101   }
102 
103   public static void main(String[] args) throws Exception {
        ...
105     ... other examples elided ...
        ...                       
145     Constructor<String> stringConstructor = String.class.getConstructor(
146         byte[].class, Charset.class);
147     Function<String,
148         Function<byte[],
149             Function<Charset, String>>> c3cons = curry3(stringConstructor);
150     String byteArray = c3cons
151         .apply(null)
152         .apply("ââªâ¡âÒ¯".getBytes(ISO_8859_1))
153         .apply(UTF_8);
154     System.out.println(byteArray); // prints ⊂∪ⓡ╓ү
155   }
156 }
```

This much must appear familiar enough to the earlier versions so hopefully everything’s clear.

Let’s now look at the `FunctionE` class itself. It too will look similar enough to the implementation in Currier2. The differences here are that we explicitly implement the Function interface, maintain state, and mutate nothing. First, the instance variables:

-   `Executable executable` — this captures the method or the constructor objects. We control setting only this via the public constructors (invoked by the factory methods since the class itself is private). The explicit public constructors keep the code future proof. In today’s version of Java the Executable class has only two subclasses—Method and Constructor. We cannot predict that this will forever remain the case and without such a guarantee the two constructors allow us to support only those cases we know about.  
    This field is shared through the chain of `FunctionE`’s created for currying.
-   `int parameterCount` — holds the value of`Executable::getParameterCount()`.  
    This field is shared through the chain of `FunctionE`’s created for currying.
-   `T self` — holds the invoker. `null` for static methods and constructors and the instance itself for instance methods.
-   `int invocationCount` — represents the number of times the curried instance was called. In conjunction with `parameterCount` helps determine the stage of currying.
-   `Object[] env` — holds all the parameters.

The `apply` method implements the actual currying. We’ll look it after the code.

```
 26   private static final class FunctionE<T, R> implements Function<T, R> {
 27     private static final Object[] EMPTY = new Object[0];
 28 
 29     private final Executable executable;
 30     private final int parameterCount;
 31     private final T self;
 32     private final int invocationCount;
 33     private final Object[] env;
 34 
 35     public FunctionE(Method method) {
 36       this(method, null, 0, EMPTY);
 37     }
 38 
 39     public FunctionE(Constructor<? extends T> constructor) {
 40       this(constructor, null, 0, EMPTY);
 41     }
 42 
 43     private FunctionE(
 44         Executable executable,
 45         T self,
 46         int invocationCount,
 47         Object[] env) {
 48       this.executable = executable;
 49       this.parameterCount = executable.getParameterCount();
 50       this.invocationCount = invocationCount;
 51       this.self = self;
 52       this.env = env;
 53     }
 54 
 55     @SuppressWarnings("unchecked")
 56     @Override
 57     public R apply(T t) {
 58       final T newSelf;
 59       final Object[] newEnv;
 60 
 61       if (invocationCount == 0) { // initial stage
 62         newSelf = t;
 63         newEnv = env;
 64       } else {                    // intermediate stage
 65         newSelf = self;
 66         newEnv = Arrays.copyOf(env, invocationCount);
 67 
 68         newEnv[invocationCount - 1] = t;
 69       }
 70 
 71       if (invocationCount == parameterCount) {
 72         return invoke(newSelf, newEnv); // final stage
 73       }
 74 
 75       return (R) new FunctionE<>(
 76           executable,
 77           newSelf,
 78           1 + invocationCount,
 79           newEnv);
 80     }
```

`apply` is simple: based on `invocationCount`, it determines its invocation stage and acts accordingly. Lines 61–63 represent the initial stage, lines 64–68 and 75–79 the intermediate stage. Lines 71–73 represent the final stage where`executable` is invoked. The invocation code is shown below. Note that, on line 66, we create a copy of `env`. This guarantees we mutate nothing across instances guaranteeing thread safety.

The invoke method is shown below. For reasons explained above (see `• Execution execution`), we perform an `instanceof` check, cast⁷, and invoke.

```
        ... continued from above ...
        ...
 82     @SuppressWarnings("unchecked")
 83     private final R invoke(T self, Object[] args) {
 84       try {
 85         if (executable instanceof Method) {
 86           Method m = (Method) executable;
 87           return (R) m.invoke(self, args);
 88         } else if (executable instanceof Constructor) {
 89           Constructor<R> c = (Constructor<R>) executable;
 90           return c.newInstance(args);
 91         } else {
 92           throw new IllegalStateException(
 93                   "Cannot handle type " + executable.getClass());
 94         }
 95       } catch (IllegalAccessException e) {
 96         throw new RuntimeException(e);
 97       } catch (InstantiationException | InvocationTargetException e) {
 98         throw new RuntimeException(e.getCause());
 99       }
100     }
101   }
```

Can we do more? I’m sure we could. But that’s all I’m doing :-)

### Footnotes

¹ The entire code shown above is available as a public gist accessible at [https://gist.github.com/lvijay/f3c95f1944b895df1b9f30c682b95b2c](https://gist.github.com/lvijay/f3c95f1944b895df1b9f30c682b95b2c). I’ve also embedded it below.

² Wikipedia page on DWIM: [https://en.wikipedia.org/wiki/DWIM](https://en.wikipedia.org/wiki/DWIM). Contains an honorary mention of GNU Emacs.

³ The javadocs are available at [https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/reflect/Method.html#invoke(java.lang.Object,java.lang.Object...)](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/reflect/Method.html#invoke%28java.lang.Object,java.lang.Object...%29).

⁴ Technically, `m.invoke(obj, arg1, arg2, ..., argN)` is also valid but to be as general as possible you would put all the args into an `Object[]` and pass that to `_invoke_`.

⁵ See _§4.11. Limitations of the Java Virtual Machine_ at [https://docs.oracle.com/javase/specs/jvms/se11/html/jvms-4.html#jvms-4.11](https://docs.oracle.com/javase/specs/jvms/se11/html/jvms-4.html#jvms-4.11).

⁶ For the design pattern aficionados, this is the Chain-of-Responsibility pattern.

⁷ Hopefully, future versions of Java will simplify the instanceof/cast ceremony. See jep305 ([http://openjdk.java.net/jeps/305](http://openjdk.java.net/jeps/305)) and [https://cr.openjdk.java.net/~briangoetz/amber/pattern-match.html](https://cr.openjdk.java.net/~briangoetz/amber/pattern-match.html).
