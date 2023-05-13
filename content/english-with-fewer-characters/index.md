---
title: "English with fewer characters"
description: "In an earlier post, I discussed the problem of reducing character count of Latin using digraphs. Here I solve it."
date: "2017-11-14T08:13:45.792Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/english-with-fewer-characters-479042fb8697
redirect_from:
  - /english-with-fewer-characters-479042fb8697
---

In an [earlier post](https://medium.com/@lvijay/twitter-and-280-characters-still-unjustified-8edad9e3b0dd), I discussed the problem of, given various Unicode ligatures and digraphs in Latin, by how much could we reduce the number of characters used to show an English word. For example, with the special ligatures “`ﬂ`” and “`ﬀ`”, we could replace the word “`fluff`” to be instead written as “`ﬂuﬀ`” thereby using only 3 characters instead of 5. I write these words in `monospace` so that the differences are clear. Shown in Medium’s regular font, they look (mostly) indistinguishable from regular fonts. Compare, “fluff” versus “ﬂuﬀ”.

I wrote a program that, given digraphs and ligatures, and a word, generates the optimal (i.e. shortest) character representation that looks the same.

This post will be technical. I discuss the problem and don’t try to explain the technical details. If you wish to see the final results, they’re at the bottom.

There is a [technical distinction](http://www.unicode.org/faq/ligature_digraph.html#Lig1) between a ligature and a digraph but I’m going to ignore it for the rest of this post. Read ligature as ligature or digraph where appropriate.

### The problem

We maintain a map of Latin string to ligature (below). Given any string, we need to find the best reduction of the given word into ligatures.

```
map = {
    'aa': r'ꜳ', 'ae': r'æ', 'ao': r'ꜵ', 'av': r'ꜹ', 'ay': r'ꜽ',
    'lj': r'ǉ', 'nj': r'ǌ', 'oo': r'ꝏ', 'ue': r'ᵫ', 'vy': r'ꝡ',
    'ff': r'ﬀ', 'ffi': r'ﬃ', 'ffl': r'ﬄ', 'fi': r'ﬁ', 'fl': r'ﬂ',
    'ij': r'ĳ', 'ft': r'ﬅ', 'oe': r'œ', 'st': r'ﬆ', 'db': r'ȸ',
    'dz': r'ʣ', 'ls': r'ʪ', 'lz': r'ʫ', 'qp': r'ȹ', 'ts': r'ʦ'
}
```

For now we only care about `map.keys()`. We’ll worry about the values later.

Suppose the keys of Latin ligatures are “fl, of, ffi, ffl, oo”, and we’re given the `word` “ffloof”, the word can be broken into the following combinations:

```
fl + l + oo + f       (4 characters)
ffl + oo + f          (3)
ff + fl + oo + f      (4)
ff + l + o + of       (4)
...
f + f + l + o + o + f (6)
```

As evident above, many solutions exist. Our aim is to find the one that minimizes the number of characters needed. Three, in the above example.

### Solution

We wish to minimize the number of characters. The simplest way is to iterate through the keys and find matches in the word. When we find a match, we recurse, and collect optimal solutions of the substrings on either side of the match.

We must sort the keys because, all else being equal, a ligature that represents more letters (like `ﬃ`) beats one that represents fewer (like `ꜵ`). So we sort the keys on length first, and then lexicographically.

Since multiple optimal solutions may exist we’ll only pick the first one. And we’re done.

The full code is available is available as a GitHub Gist (shown below)

### Execution

To use this, I need words, and luckily for me, the Mac OS X ships with a word list at `/usr/share/dict/words`

We feed these to the script, sort on efficient reduction, and print. Here we go:

```
$ < /usr/share/dict/words ./compressed-words.py | sort -nr -k3,4
```

### Proof of correctness

I’m skipping this for now. I might ﬁll it in at a later time. (Am tempted to say left as exercise ;-)

### Complexity Analysis

The worst case scenario is that the given word has no matches with the ligatures. So, given a word of length _n_ and _m_ ligatures would need comparison until the end with the first ligature, taking time n. This would happen m times for each of the m ligatures. Ordering the ligatures will take time O(m lg m), giving us an overall complexity of O(nm + m lg m). (We ignore the length of individual ligatures.)

### Results

Out of 235,886 words in the dictionary, the program was able to convert 45,928 words. The most effective reductions are shown below. For the first few, I show the breakdown. The others can be figured out.

studbook ﬆuȸꝏk `ﬆ + u + ȸ + ꝏ + k`  
floorway ﬂꝏrwꜽ `ﬂ + ꝏ + r + w + ꜽ`  
floodway ﬂꝏdwꜽ   
coeffluent cœﬄᵫnt  
voodooist vꝏdꝏiﬆ  
stue ﬆᵫ `ﬆ + ᵫ`  
strayaway ﬆrꜽawꜽ  
stay ﬆꜽ `ﬆ + ꜽ`  
stavewood ﬆꜹewꝏd `ﬆ + ꜹ + e + w + ꝏ + d`  
footstool fꝏtﬆꝏl  
foodstuff fꝏdﬆuﬀ  
flue ﬂᵫ `ﬂ + ᵫ`  
floodwood ﬂꝏdwꝏd  
flagstaff ﬂagﬆaﬀ  
fisticuff ﬁﬆicuﬀ `ﬁ + ﬆ + i+ c+ u + ﬀ`  
fist ﬁﬆ `ﬁ + ﬆ  
`statuesque ﬆatᵫsqᵫ  
floodproof ﬂꝏdprꝏf  
floodboard ﬂꝏȸoard  
broomstaff brꝏmﬆaﬀ

The longest word which could be replaced was 24 letters long, “scientificophilosophical” as “scientiﬁcophilosophical” but alas, it had but one replacement.  
The longest word with 3 replacements is 23 letters long, “gastroenteroanastomosis” as “gaﬆrœnteroanaﬆomosis” (`ﬆ + œ + ﬆ`).  
The longest word with 3 unique replacements is 22 letters long, “zoologicoarchaeologist” as “zꝏlogicoarchæologiﬆ” (`ꝏ + æ + ﬆ`).

Let me conclude this poﬆ by sꜽing, once again, that Twitter’s character increase was uǌuﬆiﬁed.

`Uǌuﬆiﬁed.`

— Vĳꜽ
