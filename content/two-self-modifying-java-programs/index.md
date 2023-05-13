---
title: "Two self-modifying Java programs"
description: "And the theory behind a potential third and fourth"
date: "2020-05-30T14:24:33.121Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/java-self-modify-ecae04189196
redirect_from:
  - /java-self-modify-ecae04189196
---

“Self-playing Cello”, 4' Brass Mobile, by Matt Brand, Zintaglio Arts, 1994. Source: [http://web.mit.edu/deansgallery/brand/cello.html](http://web.mit.edu/deansgallery/brand/cello.html). License: Matt Brand, Zintaglio Arts, used with permission from the author.

In this post, we’ll look at a two small Java programs with the same flavor: they modify themselves.

I know of no practical use for these programs and I make no excuse for that. A while back the thought struck me to write a program which modified itself and I just followed it through.

#### What is a self-modifying Java program?

Before we begin, let me quickly define what I mean by a self-modifying program.

Trivially, any program that maintains state modifies itself. For instance, the simplest `for` loop, `for (int i = 0; i < n; ++i)`, is a self-modifying program. The variable `i` is a part of the program and is modified; therefore, by definition, this program modifies itself.

I mean something less trivial, though. A self-modifying program is one that modifies its _structure_ not its state. There should be a change in the program’s behavior rather than in its data. Let’s take a more concrete example.

#### General program structure

Both the programs have the structure shown below. We’ll discuss it after the code itself.

The general structure of the self modifying programs. Did you notice that the code itself refers to this blog and vice versa?

We have a _final class_ named `Replacement0` that has a `main` method. This should be the main class we run. The class has a _public final_ method named `dwim` (short for _do-what-i-mean_) that accepts three arguments, each of which is also final. The method simply concatenates their string values and returns a `String`.

In the above, the crucial lines are lines 16 and 21. I’ve highlighted them. Notice that in line 16 the function prints exactly what one would expect from reading the method `dwim` (`3.14159[2, 6, 53]`). However, we get a different output from `dwim` at line 21 (`2.718281828[4, 5]`). In effect, we have modified a `final` method of a `final class` in Java. How? That’s what we explore here.

Goodhart’s Law states “When a measure becomes a target, it ceases to be a good measure”. Later in the article, we’ll look at some ways to achieve the above goal but without actually modifying the program’s behavior.

**Batteries Included**  
Neither of the two solutions I show below require any additional dependencies. They both work with just plain ol’ Java. They were tested on OpenJDK 11 and AWS Corretto JDK 11.

### The two techniques

⒈ Java Debug Interface (JDI) and  
⒉ Java Agents API

[Talk is cheap. Show me the code](https://lkml.org/lkml/2000/8/25/132), you say? Here’s [_Replacement1.java_](https://github.com/lvijay/selfmod/blob/master/finl/Replacement1.java), built using Java JDI API, followed by [_Replacement2.java_](https://github.com/lvijay/selfmod/blob/master/finl/Replacement2.java), built using Java Agents. The actual code would be too much and doesn’t render well so I’ve only shown excerpts. The full code is available on [GitHub](https://github.com/lvijay/selfmod). These programs are best understood by playing with them so I strongly encourage running them.

#### ⒈ Replacement1.java JDI

```
  7 /**
  8  * A Java program that modifies itself using the JDI API.  For details
 17  * <h3>Compilation Instructions</h3>
 19  * javac Replacement1.java
 21  *
 22  * <h3>Run instructions</h3>
 35  * java -agentlib:jdwp=transport=dt_socket,address=2718,server=y,suspend=n      \
 36  *         Replacement1.java
 38  */
 39 public class Replacement1 {
 40   public static void main(String[] args)
 41       throws Exception {
          // ... elided because it is the same
          // ... as Replacement0's main method
 55   }
 56 
 57   private final <T> String dwim(
          // ... elided
 62   }
 63 
 64   private static final void doTheDeed() throws Exception {
 65     var vmm = com.sun.jdi.Bootstrap.virtualMachineManager();
 66
 67     AttachingConnector socketConnector = null;
 68     for (var connector : vmm.attachingConnectors()) {
 69       if (connector.description().contains("socket")) {
 70         socketConnector = connector;
 71         break;
 72       }
 73     }
 74
 75     var defaultArguments = socketConnector.defaultArguments();
 76     defaultArguments.get("port").setValue("2718");
 77
 78     var vm = socketConnector.attach(defaultArguments);
 79     var replacementReferenceType = vm.classesByName(
                "Replacement1").stream()
 80         .findFirst()
 81         .orElseThrow();
 82
 83     vm.redefineClasses(Map.of(
            replacementReferenceType, replacement()));
 84   }
 85
 86   private static final byte[] replacement() {
 87       // byte values elided
158   }
159 }
```

#### ⒉ Replacement2.java Java Agent

```
 18 /**
 19  * A self modifying program which uses the Java Agents API.
     * ... some lines skipped
     *
 24  * Compile Instructions
 25  * <pre>
 26  * javac Replacement2.java
 27  * </pre>
     *
 29  * Run Instructions
 30  * <pre>
 31  * java -Djdk.attach.allowAttachSelf=true Replacement2
 32  * </pre>
 33  */
 34 public class Replacement2 {
 35   public static void main(String[] args)
 36       throws Exception {
          // ... elided because it is the same
          // ... as Replacement0's main method
 50   }
 51 
 52   private final <T> String dwim(
          // ... elided
 57   }
 58 
 59   private static Instrumentation ageinst;
 60 
 61   public static void agentmain(
 62       @SuppressWarnings("unused") String args,
 63       Instrumentation inst) {
 64     ageinst = inst;
 65   }
 66 
 67   private static void doTheDeed() throws Exception {
 68     var manifestRows = List.of(
 69         "Implementation-Title: selfmod",
 70         "Implementation-Version: 0.0.1",
 71         "Agent-Class: Replacement2",
 72         "Can-Redefine-Classes: true",
 73         "Can-Retransform-Classes: true",
 74         "Can-Set-Native-Method-Prefix: false");
 75 
 76     var manifest = new Manifest();
 77     manifest.read(new ByteArrayInputStream(manifestRows.stream()
 78         .collect(joining("\n"))
 79         .getBytes(UTF_8)));
 80 
 81     var jarFile = Paths.get("selfmod.jar");
 82     try (var out = newOutputStream(jarFile, WRITE, CREATE)) {
 83       var jout = new JarOutputStream(out);
 84 
 85       jout.putNextEntry(new ZipEntry("META-INF/MANIFEST.MF"));
 86       jout.write(manifestEntries.stream()
 87           .collect(joining("\n"))
 88           .getBytes(UTF_8));
 89       jout.closeEntry();
 90 
 91       jout.putNextEntry(new ZipEntry("Replacement.class"));
 92       jout.write(replacement());
 93       jout.closeEntry();
 94       jout.finish();
 95     }
 96     jarFile.toFile().deleteOnExit();
 97 
 98     var vm = VirtualMachine.attach(
                "" + ProcessHandle.current().pid());
 99 
100     vm.loadAgent("selfmod.jar");
101 
102     ageinst.redefineClasses(new ClassDefinition(
103         Replacement2.class,
104         replacement()));
105   }
106 
107   private static final byte[] replacement() {
115     return new byte[] {
            // byte values elided
221     };
222   }
223 }
```

#### What’s happening?

As was shown in the first gist, both programs share the same technique. They have some common elements which we’ll go over now. We’ll go through the details when we cover each implementation.

All the magic happens in the method `doTheDeed` which I’ve shown. I’ve removed (_elided_) the import statements and the methods`main` and `dwim`, because they’re the same as shown in _Replacement0.java_. Both implementations have a method named `replacement` which returns a byte array. I’ve elided it too because it’s only a series of bytes. The actual contents of the byte array are crucial to understanding the magic behind this program but actually printing them in this post only hinders understanding. You’ll have to play with it yourself.

Both implementations do the self modification in the method `doTheDeed`. They connect to themselves and redefine their own class. Once the class is redefined, the method `dwim` returns a different value. This value is dutifully printed.

The work done in `doTheDeed` can be divided into three parts: (ⅰ) discovery–necessary setup for connecting to its own process, (ⅱ) connection–actually connect to itself, and (ⅲ) redefinition–change the behavior of the class and method.

`doTheDeed` invokes the method `replacement` which returns a byte array. This byte array actually is the Replacement class’s new behavior. The byte array’s values are in Java byte-code. There are two aspects to it: its contents and its provenance. I leave both as exercises to the reader.

#### ⒈ _Replacement1.java_ JDI – Java Debug Interface

_Replacement1.java_ solves the problem of discovery and connecty by using the Java Debug Interface. According to Oracle’s official [documentation](https://docs.oracle.com/javase/8/docs/technotes/guides/jpda/jpda.html)¹, JDI “provides a pure Java programming language interface for debugging Java programming language applications” and it “defines a high-level Java language interface which tool developers can easily use to write remote debugger applications” ¹. It is one of the three components of Java’s JPDA—Java Platform Debugger Architecture².

The idea being that if you want to write your own debugging tool on top of Java, you could use the JDI to achieve this. And that’s what _Replacement1.java_ does.

Except, where your typical debugger connects to another program, here, our program _connects to itself_. I find the idea of a program debugging itself extremely cool and somewhat subversive. One might argue that this utterly ordinary: the JDI allows connecting to running Java programs; it doesn’t care if that program is another program or itself. This is true but changes nothing for me. I am impressed.

**Ⅰ. Discovery  
**The program’s run instructions include this vital line:

```
-agentlib:jdwp=transport=dt_socket,server=y,address=2718,suspend=n
```

This runs the program normally but also starts a Java Debug server (`server=y`) on port 2718 (`address=2718`).

In the method `doTheDeed` (see [line 63](https://gist.github.com/lvijay/7e2453126a0847e7794eee282200e2d8#file-replacement1-java-L63)) the program gets a reference to JDI’s VirtualMachineManager through which it gets a reference to the Socket connector (`transport=dt_socket`).

**Ⅱ. Connection  
**The program connects to itself (see [line 72](https://gist.github.com/lvijay/7e2453126a0847e7794eee282200e2d8#file-replacement1-java-L72)) and gets a reference to the VirtualMachine. The same VirtualMachine it’s running on.

The self modification happens with the call to `redefineClasses` ([line 77](https://gist.github.com/lvijay/7e2453126a0847e7794eee282200e2d8#file-replacement1-java-L77)) which surreptitiously changes the definition of the method `dwim` and gives us the new result of `2.718281828[4, 5]`. There are also other changes in the byte-code but I’ll leave figuring them out as an exercise to the reader.

#### ⒉ Replacement2.java Java Agent

The Java Instrumentation API, first introduced in Java 1.5, “provides services that allow Java programming language agents to instrument programs running on the JVM. The mechanism for instrumentation is modification of the byte-codes of methods” [³](https://docs.oracle.com/en/java/javase/14/docs/api/java.instrument/java/lang/instrument/package-summary.html).

There are two ways to start Java Agents. The first is to start at the same time as the JVM does and the second allows us to start an Agent after the VM starts. We use the second technique. For details see the section _§Starting an Agent After VM Startup_ in the Java Instrumentation page. I repeat the relevant sections:

> An implementation may provide a mechanism to start agents sometime after the the VM has started. The details as to how this is initiated are implementation specific but typically the application has already started and its `main` method has already been invoked. In cases where an implementation supports the starting of agents after the VM has started the following applies:

> The manifest of the agent JAR must contain the attribute `Agent-Class` in its main manfiest. The value of this attribute is the name of the _agent class_.

> ⒈ The agent class must implement a public static `agentmain` method.

> ⒉ The `agentmain` method has one of two possible signatures. The JVM first attempts to invoke the following method on the agent class:

> `_public static void agentmain(String agentArgs, Instrumentation inst)_`

**Ⅰ. Discovery  
**Now, to start a Java Agent after the VM starts, you need a _.jar_ file. However, our implementation has only a single file. Not to worry, though. The Java SE provides us a class which can create Jar files—[JarOutputStream](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/jar/JarOutputStream.html). We use it to create a file named `selfmod.jar`. We ensure that this file’s manifest points to itself as the Java Agent (see [line 71](https://gist.github.com/lvijay/cc6047fadead497d4c604632c4571348#file-replacement2-java-L71), `"Agent-Class: Replacement2"`).

To prevent messing up our surrounding environment, we also ensure the jar-file is deleted when the program ends (see [line 96](https://gist.github.com/lvijay/cc6047fadead497d4c604632c4571348#file-replacement2-java-L96), `jarFile.toFile().deleteOnExit();`).

**Ⅱ. Connection  
**There are two parts to connecting to the VM. The first is defined by the Java Instrumentation API. This is what the static method `agentmain` does for us. In it we capture the `java.lang.instrument.Instrumentation` instance which later redefines the class to give us our new behavior. The second part, is in the program’s run instructions. When we run the program, we must specify the system property `-Djdk.attach.allowAttachSelf=true` because starting Java 9 the JDK prohibits self attachment by default[⁴](https://www.oracle.com/technetwork/java/javase/9-notes-3745703.html#JDK-8178380).

(As an aside, I contemplated modifying my program so this wouldn’t be necessary. There were two options of which I’ll admit only the first occurred to me. One was the reflectively change the above flag. The second, more ingenious technique, is to start a child process and have _that_ connect to the parent process. See [Byte-Buddy](https://github.com/raphw/byte-buddy/issues/295#issuecomment-297394387)⁵ for examples of both. Eventually, in the interests of simplicity, I decided being explicit was better.)

Once the Agent starts, it gets the new byte-code from `replacement()` which ensures that `dwim()` returns a new result.

---

That’s all there is to it, actually. These are the two simplest ways I know of writing a Java program that modifies itself. If that’s all you were interested in, and only in tangible, working solutions, you can stop here. I can imagine two more ways to achieve the same but they’re more speculative.

#### More ways to self modify

**⒊ Unsafe  
**The internal class com.sun.misc.Unsafe has been around since the very first Java. It’s used by almost all popular libraries that are interested in performance or stretching (sometimes exceeding) the limits of Java. One feature it provides is writing directly to memory locations. I do not know if this will work but the theory is simple: find out where the method `dwim` is defined. Have a replacement implementation. Fill it in the appropriate location.

The fourth technique is the same and is guaranteed to work. However, it’s much harder to implement practically, is not guaranteed to _always_ work, is not platform independent, nor is it JVM independent. Let’s take a look.

**⒋ RAM**  
In Linux kernel systems, any process can read and write its own memory via the file `/proc/self/mem`. Write a Java program that reads from this location. The file `/proc/self/maps` acts as a guide to which locations of RAM are actually accessible. Specifically, the program must search through the `[heap]` locations, locate where `dwim` is defined, modify it and run.

Apart from the more basic challenges of actually executing the above, we also have to contend with the fact that even if we get everything right, the OS might decide to do a page swap as we’re executing our code leading to exceptions. I attempted a basic implementation that changed the bytes of a String using this technique. It worked most of the time but sometimes it failed with an exception. The code for this and the occasional stacktrace are available at the gist [https://gist.github.com/lvijay/7fefd6df99bd7b673aa29775a6dae58d](https://gist.github.com/lvijay/7fefd6df99bd7b673aa29775a6dae58d).

I’m sure with sufficient patience and persistence this is an achievable goal. The Eclipse MAT program is a Java heap analyzer. It dumps a running Java program’s heap. One could analyze this heap, find out where the method under question is defined and modify it[⁶](https://www.eclipse.org/mat/). Needless to say, this is not platform agnostic. Given that different Java implementations might organize their heaps differently, this isn’t even a Java independent solution. But, it’ll be fun.

For details on the `/proc/self/mem`, see the man page of `[proc(5)](https://manpages.debian.org/testing/manpages/proc.5.en.html)`.

### Some non solutions

If we keep only to the original gist and wanted a solution that matched the _input/output_ criteria, we have the following options. I’ll briefly go through them and also explain why they don’t fit the bill of a _self-modifying_ program.

Recall the example shown at _Replacement0.java_. The first time `dwim` is invoked, it duly prints the concatenation of its arguments and the challenge is to have the _second_ time we print the invocation to have a different result. I’ve repeated the snippet below:

```
 9      final Replacement0 r = new Replacement0();
10  
11      final String run1 = r.dwim(i, s, l);
12      System.out.println(run1); // prints 3.14159[2, 6, 53]
13  
14      doTheDeed();
15  
16      final String run2 = r.dwim(i, s, l);
17      System.out.println(run2); // print  2.718281828[4, 5]
```

If we only want the output of line 17 above to be different from line 12, then the following examples would work:

1.  Bootstrap class path[⁷](https://docs.oracle.com/javase/8/docs/technotes/tools/findingclasses.html#bootclass)  
    Java supports the nonstandard option, `**-Xbootclasspath**`, which lets you load custom implementations standard Java classes such as `java.lang.String`. With a custom instance of String, it’s trivial to write a version that returns a different value based on where it’s called from and when it’s called. This will achieve the goal of printing one output the first time (`3.141...`) and some different output the second time.
2.  Redirect stdout to a custom stream  
    Use [System::setOut](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/System.html#setOut%28java.io.PrintStream%29) and write all `System.out` calls to a custom implementation of `java.io.PrintStream`. It will ignore what it gets from `dwim` and instead send a different output to the real stdout.
3.  Java instrumentation at class loading time  
    Using a Java Agent that starts before starting the program will work.

Choices ⑴ and ⑵ fully satisfy the input/output criteria. They will print one output the first time and a different output the second. However, they aren’t examples of _self-modifying_ programs. Choice ⑶ doesn’t count for slightly more elaborate reasons.

Choice ⑶ doesn’t count because it would involve making a change to the _ReplacementX_ class _before_ the first invocation of `dwim`. This isn’t a _self_\-modifying so much as it’s modified beforehand. It’s a little iffy and I see arguments that rebut my case. Again, imo, it goes against the spirit because the modification happens not at `doTheDeed` but earlier.

---

#### The end

If you have more solutions, feel free to share. You don’t need to abide by my constraints though strong constraints typically engender greater creativity.

### Footnotes

¹ Taken from the JPDA Overview and Architecture pages respectively available at [https://docs.oracle.com/javase/8/docs/technotes/guides/jpda/jpda.html](https://docs.oracle.com/javase/8/docs/technotes/guides/jpda/jpda.html) and [https://docs.oracle.com/javase/8/docs/technotes/guides/jpda/architecture.html](https://docs.oracle.com/javase/8/docs/technotes/guides/jpda/architecture.html).

² JPDA’s official website: [https://docs.oracle.com/en/java/javase/14/docs/specs/jpda/jpda.html](https://docs.oracle.com/en/java/javase/14/docs/specs/jpda/jpda.html)

³ Javadocs package summary of the Java Instrumentation module: [https://docs.oracle.com/en/java/javase/14/docs/api/java.instrument/java/lang/instrument/package-summary.html](https://docs.oracle.com/en/java/javase/14/docs/api/java.instrument/java/lang/instrument/package-summary.html).

⁴ See Java 9 release notes at [https://www.oracle.com/technetwork/java/javase/9-notes-3745703.html#JDK-8178380](https://www.oracle.com/technetwork/java/javase/9-notes-3745703.html#JDK-8178380).

⁵ Both proposals were discussed in the same Byte Buddy issue, issue 295 — [https://github.com/raphw/byte-buddy/issues/295](https://github.com/raphw/byte-buddy/issues/295). For the proposed reflective solution, see the [comment](https://github.com/raphw/byte-buddy/issues/295#issuecomment-296438308) by GotoFinal. Byte Buddy’s maintainer, Raphael Winterhalter, confirmed using a child process in [this comment](https://github.com/raphw/byte-buddy/issues/295#issuecomment-297394387).

⁶ Eclipse MAT is available at [https://www.eclipse.org/mat/](https://www.eclipse.org/mat/).

⁷ For details on the Boot classpath, see [https://docs.oracle.com/javase/8/docs/technotes/tools/findingclasses.html#bootclass](https://docs.oracle.com/javase/8/docs/technotes/tools/findingclasses.html#bootclass).
