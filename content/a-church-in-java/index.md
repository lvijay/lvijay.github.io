---
title: "A Church in Java"
description: "An implementation of Alonzo Church’s numerals in the Java Programming Language"
date: "2023-05-13T11:44:50.317Z"
categories: []
published: false
---

Do not be alarmed by the title. This is not a religious post. It refers to the work of [Alonzo Church](https://en.wikipedia.org/wiki/Alonzo_Church), American logician and mathematician. Alonzo Church invented the (untyped) lambda calculus which inspired Artificial Intelligence researcher, [John McCarthy](https://en.wikipedia.org/wiki/Lisp_%28programming_language%29#History), into writing a paper about a hypothetical programming language named LISP which in turn inspired another computer scientist, [Steve Russell](https://en.wikipedia.org/wiki/Steve_Russell_%28computer_scientist%29), into implementing the language (circa 1958). And thus was born one of the two programming languages that’s still in popular use.

Anyway, this isn’t a historical post. It describes the _Church numerals_ implemented in Java. Anachronistically, imagine what would happen if someone was inspired by Church’s lambda calculus and decided to write it Java 11. That’s what this is. _A. Church in Java_.

#### Church Numerals

[Wikipedia](https://en.wikipedia.org/wiki/Church_encoding) has a pretty good explanation of Church Numerals and how they work. Some excerpts below:

> The **Church numerals** are a representation of the natural numbers using lambda notation.  
> Terms that are usually considered primitive in other notations (such as integers, booleans, pairs, lists, and tagged unions) are mapped to [higher-order functions](https://en.wikipedia.org/wiki/Higher-order_function "Higher-order function") under Church encoding…. In the [untyped lambda calculus](https://en.wikipedia.org/wiki/Lambda_calculus "Lambda calculus") the only primitive data type is the function.  
> The Church encoding is not intended as a practical implementation of primitive data types. Its use is to show that other primitive data types are not required to represent any calculation. The completeness is representational. Additional functions are needed to translate the representation into common data types, for display to people.
