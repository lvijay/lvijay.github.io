---
title: "Why do Python 3’s IntEnums start at 1?"
description: "Why the discrepancy? Python’s array indexes start at 0."
date: "2023-05-13T11:44:34.643Z"
categories: []
published: false
---

_Question_: Why do `IntEnum`s, introduced in Python 3.4, start their indexing at 1 when all other Python indexes start at 0? Was it in response to the rising popularity of the `R` programming language?  
_Answer_: Because Python semantics dictate that `0` is _false_ which clashed with typical desired behavior that none of the Enum’s values are false. Hence, to maintain expected semantics Python’s `IntEnum`s start at 1.

---
