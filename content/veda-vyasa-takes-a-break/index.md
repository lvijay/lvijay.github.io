---
title: "Veda Vyasa takes a break"
description: "Philosopher Jerry Fodor explains how Veda Vyasa, the Mahabharata’s author, bought time from its scribe, the god Ganesha."
date: "2019-09-01T02:26:01.098Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/veda-vyasa-takes-a-break-b7d9cdbd795f
redirect_from:
  - /veda-vyasa-takes-a-break-b7d9cdbd795f
---

An eco-friendly, biodegradable Ganesha made with salt dough for Ganesha Chaturti by [Aksvij](https://medium.com/u/4fc7ae7a6d83) and son. Photo also by [Aksvij](https://medium.com/u/4fc7ae7a6d83). License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0).

The Mahabharata is humanity’s largest epic. It comprises two hundred thousand verses. In print, it comes to around twelve thousand pages. [¹](#19c0)

Written in a time well before the printing press and typewriters, penning the epic was no human task. Thus, Veda Vyasa, the Mahabharata’s author, asked the god Ganesha to transcribe his first narration of 8,800 verses. Ganesha made one condition to Vyasa: once he—Ganesha—started writing he would need to continue without pause. If there were pauses in the narration, he would get bored and he would quit. Vyasa knew it was impossible for him to narrate the entire epic without stopping—he had to eat, drink, and sleep, among other things. Vyasa then made a counter condition to Ganesha: that Ganesha write a vers_e_ if a_nd only_ if he ful_l_y understood the meaning of the verse. Ganesha agreed. The rest is history.

The story goes that Vyasa intentionally complicated his verses so Ganesha would have difficulty comprehending them and thus, when Ganesha was contemplating upon the verses, Vyasa was able to eat, sleep, rest, and think up the next set of verses. However, my argument in this post is that rather than wonder how Vyasa got sufficient rest, we ought to wonder how he was able to complete the story at all. My conclusion will be that Vyasa narrated only 8,800 verses because with more Ganesha would not have been able to arrive at full understanding.

My arguments were inspired by the arguments of twentieth century philosophical giant, Jerry Fodor (1935–2017). I’d initially thought to discuss his ideas after illustrating how Vyasa got Ganesha to pen the Mahabharata but just the illustration has made this post a 20-minute-read so I’m afraid discussions around the Frame Problem and Jerry Fodor need to be deferred, perhaps indefinitely.

First, let’s talk about what this post isn’t:

1.  It is not an introduction to the Mahabharata.  
    You should be able to understand this post with no prior knowledge of the epic. Anything you learn about the Mahabharata in this post is purely accidental. The information presented is accurate but without the details or nuances.
2.  It is not an introduction into the Theory of Computation.  
    To show that it was impossible for Ganesha to arrive at a _complete understanding_ of Vyasa’s narration, we need to show that the problem was too hard to compute (computationally intractable). To show this we see a glimpse of the problems computational theorists and software engineers encounter.
3.  It is not an introduction to Cognitive Science or Artificial Intelligence.  
    I will (very) briefly discuss Jerry Fodor’s discussion around an as-of-yet unsolved problem in both cogsci and Artificial Intelligence. The Frame Problem originated in Computer Science, Artificial Intelligence, and Philosophy and that’s from where Jerry Fodor (and may other philosophers) took it.

Each of these topics is vast. The latter two are active areas of research. There are a few mathematical equations presented below but feel free to ignore them. They are presented for completeness and are not essential to understanding the post. The numbers and graphs, it is hoped, will suffice.

Next, let’s discuss the presentation strategy:

1.  We’ll discuss some strategies available to Vyasa.
2.  A quick look at some characters in the Mahabharata.   
    We’ll use their relationships as a means to elaborate and discuss Ganesha’s task of understanding.
3.  An actual look at _complete understanding_. We’ll look this in some detail. Remember, the theme of this article is to show that it was hard for Ganesha to arrive at a complete understanding of Vyasa’s narration. Showing this isn’t easy so we’ll build up to it slowly and methodically. (Perhaps aptly, I’ve titled some subsections _§Are we done?_ and _§Are we done, yet?_)  
    • We’ll show that the problem of understanding is computationally intractable. This is a way of saying that it’ll take more time to complete the problem than there are resources available in the universe.
4.  A conclusion.

---

### Table of contents

If you’ve already read the post or, if you started to read it but stopped and would like to resume where you left off, use the section links below. Since each section is closely tied to previous sections skipping sections isn’t advised.

⒈ [Vyasa’s Strategy](#5938)  
⒉ [The Mahabharata Family Tree](#972e)  
⒊ [Are we done?](http://c807)  
⒋ [Computational costs](http://431d)  
⒌ [Are we done, yet?](#e863)  
⒍ [Processing power](#cba6)  
⒎ [The end](#4683)  
⒏ [Footnotes](#4036)  
⒐ [Acknowledgements](#f37b)

---

### Vyasa’s strategy

Let’s consider Vyasa’s options. He needs ways to slow down Ganesha. Ganesha’s no fool so the techniques will need to be rock solid.

Ganesha’s writing process would be something like below:

**⒈** Listen to Vyasa recite a verse.  
**⒉** Understand the verse.  
**⒊** Write it down.

Let’s spell these out in a little more detail.

⑴ is not particularly interesting. Regardless of how long it takes Vyasa to recite a verse, Ganesha must listen and, in any case, Vyasa doesn’t get a break when reciting.  
We’ll get to ⑵, understanding, in more detail later in the article. In fact, we’ll be devoting the bulk of our time to it.  
How long would ⑶, writing, take Ganesha? Keeping to Ganesha’s own words to Vyasa, we’ll assume that Ganesha could write at the same pace as Vyasa could recite and suppose that it took thirty-seconds to recite a verse.

Thus, from Vyasa’s view, he must make Ganesha spend a lot of time in ⑵ since the time Ganesha spends in ⑴ and ⑶ include Vyasa’s equal time commitment. Equal time commitment equals no free time.

How could Vyasa guarantee himself rest? What could he do to ensure that Ganesha spent a lot of time just _understanding_?

One simple technique available to Vyasa is to just use what, centuries later, Scheherazade used to survive for One Thousand Arabian Nights — end every verse with information that’s incomplete and forthcoming. Ganesha, denied full understanding, would be forced to wait for the information. In this way, if Vyasa recited thirty verses without pause, would get fifteen-minutes of rest. Simple, inelegant, functional.

But where we may excuse Scheherazade for choosing skullduggery over death, the same doesn’t hold for Vyasa. Could he have done better? I argue that he did. In fact, I argue, Vyasa’s counter condition to Ganesha guaranteed him time. How? That’s what follows. Illustrated with many images and animated GIFs.

### The Mahabharata Family Tree

The Mahabharata is primarily the story of a family, the Lunar dynasty. A partial family tree is shown below. And yes, the “Vyasa” shown below _is_ also its author. Keep this image in your mind or as a handy reference because the images shown later in this article won’t be as clear.

A partial family tree of the central characters in the Mahabharata. Female characters are shown in yellow boxes and make characters in green boxes. Arrows leading down from a circle ○→ indicate a child born and its parents. King Shantanu, shown at the top, was a descendent of the Kuru dynasty. He first married the river goddess, Ganga, and with her had eight children, the eighth of whom was Bheeshma. After Bheeshma’s birth, Ganga left Shantanu, and he later married Satyavati with whom he had two sons. Without getting into the details of their lives, the primary characters of the Mahabharata are shown at bottom. On the left, the 100 Kauravas and on the right the 5 Pandavas. Image generated by author. Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Mahabharata_Partial_Family_Tree.png). License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0).

Vyasa’s _Mahabharata_ doesn’t start with an explanation of the family tree but, for our present purposes, it’s a good place to start. The following paragraph is a lightning summary of the Mahabharata family tree shown in the image above. It’s accurate but light on details.

Very briefly, King Shantanu, descendant of the Kuru dynasty, marries Ganga. With her he has eight children the first seven of whom die the day of their birth. The eighth is Bheeshma. After the birth of Bheeshma, Ganga leaves Shantanu. A few years later, Shantanu marries Satyavati. With Satyavati he has two sons, Chitrangada and Vichitravirya. Vichitravirya is married to sisters, Ambika and Ambalika. Vichitravirya dies before leaving any progeny so Satyavati asks her son Vyasa to sire heirs to the throne. Vyasa agrees. Ambika births Dhritarashtra and Ambalika births Pandu. Dhritarashtra is wedded to Gandhari, princess of the Gandhara kingdom and they have a hundred children; Pandu has five children with his two wives, Kunti and Madri. Dhritarashtra’s children are called the Kauravas and Pandu’s children are called the Pandavas.

Let’s play out Ganesha’s thought process. Now, as Vyasa describes the family tree, Ganesha must _fully_ understand it before he can pen it down. For simplicity, let’s assume Ganesha first starts with a blank slate.

Ganesha’s blank slate. Naturally, he uses [GNU Emacs](https://www.gnu.org/software/emacs/). Source: screenshot on author’s computer. License: public domain.

Ganesha is told of the existence of Parashara, Satyavati, and the birth of Vyasa. We can represent his understanding as shown in the image below. The ovals indicate the characters and arrows between them indicate their relationship. Thus, Satyavati and Vyasa are in ovals and there’s an arrow “mother” between Satyavati and Vyasa indicating the former is the latter’s mother. For brevity, I don’t show the inverse relationships such as Vyasa being Satyavati’s son.

Vyasa is sired by Parashara’s union with Satyavati. (Source: generated by author. License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0).)

Continuing this way, we see the introduction of several other characters. (Fancy animated GIF coming up.)

**Quick sidebar**: since this post is full of animated GIFs that are better watched from the beginning and scrolling through the post will start the animation before you’re ready to see it, the captions of all the animated images provide a hyperlink to themselves. Clicking the link will let you view it from the beginning.

An animated, somewhat chronological, illustration of the parital Mahabharata family tree. Many details left out for brevity, clarity, and simplicity but the details are accurate. Click [here](https://cdn-images-1.medium.com/max/2400/1*3YbhnyMlbt-YFuFgwwLJ6w.gif) if you want to see the animation from the beginning. (Source: generated by author. License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0).)

The above is an illustration but does it illustrate _complete understanding_? I argue: no, it does not. While one can _derive_ that, say, Pandu is Duryodhana’s uncle, it goes against what Vyasa asked for and why he asked for it. Vyasa’s condition to Ganesha was under the explicit condition that Ganesha first understand and, to understand, Ganesha must, at minimum, consider every bit of information he gets. Below is an animated GIF of Ganesha doing exactly this.

(In the interests of space I’ve kept the below only until Ambika and Ambalika wed Vichitravirya. Where the earlier animation had 23 characters and 18 transitions, this one has only 10 characters but 40 transitions. But, because I find it fun, I do show all links between all 23 characters later.)

The first animation keeps closely to the layout of the above image but, as you’ll see, it gets messy fast. The animation after this is the same but prettier.

Same animation as the one above except in addition to the regular relationships shown above here, when a character is introduced, Ganesha also computes the “second order relationship” between them every other existing character. A second order relationship is a link between two characters that must be derived—for example, Gandhari is Arjuna’s paternal aunt. All second order relationships are described with a ‘?’ because it is assumed that Ganesha will compute the correct relationship even if I, the author, can’t. Click [here](https://cdn-images-1.medium.com/max/1600/1*_lyvmMNvc9nsIGWkq3f_mg.gif) if you want to see the animation from the beginning. (Source: generated by author. License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0).)

In the above image, when any character is introduced, Ganesha computes the relationship between that character and every other existing character. The relationship between any two characters that’s not the direct relationship from earlier images is described as a _second-order relationship_. An example second-order relationship is that Ganga is Vichitravirya’s step-grandmother.

All the second order relations are labeled with a ‘?’ for my simplicity. Maybe in some future date I’ll write the program which computes that, say, Ganga is Vyasa’s stepmother, that Bheeshma is Gandhari’s step-uncle, and that though Vyasa sired Pandu, by the laws of _niyoga_[²](#10cc) (नियोग), Vichitravirya is the father. While writing such a computer program is non-trivial, I claim that Ganesha won’t have any problem determining the relationship between any two people. He _will_ have to run through all the pairs and note their relationship, though.

A more neatly organized image is shown below. It shows the same characters and the same edges between the characters but without getting messy like before. The downside to the below image is that the chronological nature is lost because no longer are characters who were born first at the top of the image. Click on the image to see the animation start from scratch.

A more comprehensible second-order-relationship animation. This image is the exact same as the one right above except all the characters are placed at the periphery of the image with their relationships all in the middle. Click [here](https://cdn-images-1.medium.com/max/1600/1*uTQfNi06jJhJWFzY0mfX2A.gif) if you want to see the animation from the beginning. (Source: generated by author. License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0).)

Recall that Vyasa said Ganesha wasn’t to write until he had achieved a full understanding. As is hinted in the above image, every character’s relation with every other must be calculated. However, not every character is introduced at the same time. The above animations apply only after we know of the given twenty-three. More realistically, the introduction of each character will trigger a loop of all characters to the newly introduced character. That would look something like below. This time, the animation shows all twenty-three characters.

The image shows what we would expect from Ganesha. With the introduction of every character, Ganesha would consider every other character’s relationship to the introduced character. Here I haven’t even tried to label the relationships. Instead, every relationship (i.e., line connecting two characters) is numbered. The title shows the introduced character and their rank. With 23 characters, there are 253 relationships. More correctly all arrows should have double-headed arrows (↔) but I’ve used single-headed ones (→) to capture the chronology of character introduction. More arrow heads on a character indicates a later introduction. Thus, Satyavati has none, and Sahadeva has 23. Click [here](https://cdn-images-1.medium.com/max/2400/1*C7UOgCy_sWoWsppKYnwXqw.gif) if you want to see the animation from the beginning. (Source: generated by author. License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0).)

The image shows what we would expect from Ganesha. With the introduction of every character, Ganesha would consider every other character’s relationship to the introduced character. Here I haven’t even tried to label the relationships. Instead, every relationship is numbered. The title shows the introduced character and their rank; “Ambalika #10” implies she’s the tenth character. With 23 characters, there are 253 relationship computations to perform. We’ll get to how 253 relates to 23 in the next paragraph.

As is evident from the above image, the number of relationship computations that occur with each character’s introduction is equal to the number of characters already in existence. Numerically, the number of computations is equal to the sum of `1+2+3+4+...+n-1` where `_n_` is the number of characters so far introduced. As we all know, this summation is equal to `n×(n-1)÷2`. This explains 253 links for 23 characters since`253=23×22÷2`.

That’s a simple strategy for Vyasa, then. Just introduce a whole host of characters and Ganesha will be caught up computing their relationships and Vyasa gets enough time to rest. I’m reminded of the joke about the man who read and reviewed the phonebook: “It has a lot of characters but no plot.” (My sympathies if the word “phonebook” makes no sense to you.)

And Ganesha’s strategy is also set. He just has to understand the relationships between all characters, locations, kingdoms, etc. Yes, locations and other things would also apply because that’s also part of understanding. Knowing that, say, _Shantanu_ is the king necessarily implies understanding that _Ganga_ is queen. Knowing that _Bheeshma_ is _Shantanu’s_ son and _only_ Shantanu’s son implies understanding that he’s _not_ _Parashara’s_ son.

#### Are we done?

> “No, no! You have merely painted what is! Anyone can paint what is; the real secret is to paint what isn’t!” — sorcerer Bu Fu in Oscar Mandel’s 1964 book, “Chi Po and the Sorcerer” [³](#734b).

As Bu Fu says, we’ve shown what’s there but we haven’t shown what isn’t. Now, like Chi Po, Bu Fu’s student, you too might fairly ask, “But what is there that isn’t?” Let’s consider.

What Ganesha has so far done is only consider every existing character’s relationship with a newly introduced character. For instance, when _Chitrangada_ is born Ganesha understands that Chitrangada is Shantanu’s son and Bheeshma’s half-brother. However, must not Ganesha also understand that no longer are Shantanu and Satyavati a childless couple? Likewise, when _Yudhishtra_ is born, yes, Gandhari becomes an aunt, she also realizes that her as-yet unborn children will not be first-in-line to the throne. (This is a later plot point.)

Thus, the introduction of a single character entails, not only the relationship of all characters with the new one, but calculating the relationships of _all characters against all characters_.

What does this look like? I’ve shown an illustration below. Where the earlier graph had 40 transitions for 10 nodes, this one below has 166 transitions for the same 10. Unlike earlier, I don’t show the relationship graph for the 23 characters because that has a whopping 2,024 transitions. We’ll address the connection between 10 nodes and 166 computations after the animation.

This animation has Ganesha computing all relationships between all characters when each character enters the mix. The colors are random but used to indicate when a previously computed relationship is redrawn. Click [here](https://cdn-images-1.medium.com/max/1600/1*RK5rRdLQkGIFBTBahr9bdA.gif) if you want to see the animation from the beginning. (Source: generated by author. License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0).)

Why does it have so many transitions? Recall that computing relationships upon introduction of every character went as `1+2+3+4+5+n-1`. In this case, though, since the introduction of each character entails a full computation, the number of computations is the summation of the array \[`1`, `1`, `1+2`, `1+2+3`, `1+2+3+4`, `1+2+3+4+5`, … `1+2+3+…+n-1`\]. Mathematically, it is ΣⁿᵢΣⁱ₁j.

To fully appreciate how quickly the number of computations grow, see the below graph. It shows the growth in comparisons for the three techniques we’ve so far encountered (1) jotting down Vyasa’s verses as-is, (2) the number of computations when only considering _what-there-is_ and finally, (3) the number of computations that must be performed when also considering _what-there-isn’t_.

This graph compares the cost of computation for each of the 3 strategies described so far. The blue line is Ganesha computing all relationships for all characters when one is introduced; the green line is him only computing the relationship of every introduced character with a newly introduced one; and the barely visible orange line is Ganesha writing down Vyasa’s verses as-is. The X-axis describes the number of facts Vyasa gives Ganesha and the Y-axis is the corresponding number of computations for each strategy. Click [here](https://cdn-images-1.medium.com/max/1600/1*1UApL6q1iUwhovoftHNTYA.gif) if you want to see the animation from the beginning. (Source: generated by author. License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0).)

Note that none of the graphs are actually dipping, their individual values are constantly on the rise. It’s just that because the blue line grows so fast (see the y-axis scale), the other two give the appearance of going down.

Note further that the above graph’s X-axis is the number of _facts_ Vyasa gives Ganesha. While I’ve used familial relationships as an example, clearly Ganesha must perform his computations for all information.

#### Computational costs

In computational terms, the strategies described so far grow at the rate of `O(n)`, `O(n²)`, and `O(n³)`, respectively. The `_n_`, in all cases, is the number of characters and the result is the number of relationships Ganesha must compute. The capital letter O, (more commonly called Big-O), describes as an upper bound the number of computations. For instance, in the second strategy (_what-there-is_), as we’ve seen, Ganesha must perform `n×(n-1)÷2` computations. When expanded, this evaluates to `n²-2n` computations. The big-O notation gives us an upper bound on the number of computations, that an algorithm _shall-not-exceed._ Thus, at very large numbers, the value of `n²` is approximately the same as `n²-2n` and `4n²+70n` or off only by a _constant_ factor. (Try it out! Compare the results of two quadratic equations as you vary the value of n. They’ll tend to converge to some constant.)

While we don’t care about what constants we multiply or add to our equations (`n² ≅ 2n² ≅ n²÷200 ≅ n²-58n+2718281828 ≡ O(n²)`, the ≡ is the mathematical symbol for approximately equal to); the slightest change to the highest power changes the value of big-O and determines the big-O. Thus, `4n²-2n+58` is `O(n²)`, `14.7n³-224n²+10000` is `O(n³)` and, perhaps unintuitively, `17n²ᐧ⁰⁰⁰⁰⁰⁰⁰⁰¹+3n²` is `O(n²ᐧ⁰⁰⁰⁰⁰⁰⁰⁰¹)`.

Polynomial problems (ones of the form `nᶜ` where `c` is a constant) are typically considered tractable while exponential equations (of the form `cⁿ` where `c` is a constant greater than 1) are considered _in_tractable. By tractability we mean is the rate-of-growth of computational resources needed to solve the problem. For exponential problems, the required resources quickly outgrow the size of the known universe.

The good news, then, for Ganesha is that the problem of understanding is only an `O(n³)` problem.

Or is it?

#### Are we done, yet?

Thus far we’ve only considered _binary relationships_—mother, father, husband, grandparent. But there’s more. There are also _unary_, _ternary, quaternary, quinary,_ relationships. In fact, there are as many relationships are there characters! For instance, when Pandu gets married, he’s no longer a bachelor. When Bhima’s born, Yudhishtra’s no longer an only-child. These are unary relationships. When Ambika and Ambalika are wedded to Vichitravirya, together they form a wedded triple, a ternary relationship. Four people would form quaternary relationships and so on. What does it take for Ganesha to compute these relationships?

Let’s consider an example:  
1\. **Satyavati**. What properties do we note about Satyavati?   
1\. To name a few, she’s female, unmarried, a virgin, smells of fish. Notice that all these are _unary_ relationships. Naturally, since with one person, one can only have unary relations.  
2\. Next, in comes **Parashara**. What do we note about him?   
2.1. Well, _his_ unary relationships are that he’s male, a sage, and wants[⁴](#7763) to cross a river.  
2.2. What about him and Satyavati? Well, they liaise (a binary relationship). We covered that earlier but what else?   
2.3. Once again, we have to consider Satyavati’s unary relationships some of which are: she’s no longer childless, still a virgin (it’s complicated), and no longer smells of fish (also complicated).  
2.4. Then it’s Parashara’s updated unary relationships. He’s also no longer childless, still male (we’ll cover this in the Jerry Fodor part), on an island, and so on.  
3\. **Vyasa** is born.  
3.1. He’s male. He’s on an island.  
3.2. He’s Satyavati’s son, he’s Parashara’s son.  
…  
3.7. Satyavati, Parashara, and Vyasa form a family (ternary relationship).  
4\. **Shantanu** is introduced.   
4.1. Shantanu’s unary properties—king, male  
4.2. What’s the (binary) relationship between Shantanu and Parashara—nothing at this juncture because they haven’t met.  
…  
4.15. What’s the quaternary relationship between Shantanu, Parashara, Satyavati, and Vyasa?

It’s possible that there will be character combinations that have no relationship worth noting. But it still falls upon Ganesha to _review_ those combinations to note their null relationships.

I don’t have a graphic illustration for this but the below block shows the character combinations when there are just 6 people: Satyavati, Parashara, Vyasa, Shantanu, Ganga, and Bheeshma. Think of it as an elaboration of the above example. Note that there are 63 combinations. We’ll get to the relationship between 6 and 63 after the image.

All combinations of relationships Ganesha must review. The relationships are labeled with their arity (how many items go into that relationship), and grouped within parentheses. So, for a Quinary relation, you have five items grouped within ‘(’ ‘)’s. Given n entities, the number of relationships to be computed is always 2`ⁿ`. (Source: screenshot of author’s GNU Emacs frame. License: public domain.)

I’ve grouped the relationship combinations that occur between all six characters. (This is probably the only time I’ll ever get to use _quaternary, quinary,_ and _senary_. I probably shouldn’t even use it here.) Since there are six characters, Ganesha has to compute _6_ _unary_, _15 binary_, _20 ternary_, _15 quaternary_, _6 quinary_, and _1 senary_ relationships. This adds up to 63.

Readers with some familiarity with Set Theory will find the above image familiar. The above image denotes the _power set_ of the given set of characters. The power set of a set S is the set of all subsets of S. For instance, with a simple set of three elements, say, `{a, b, c}`, the set of its subsets is `{Ø, {a}, {b}, {c}, {a, b}, {a, c}, {b, c}, {a, b, c}}` where Ø is the empty set. (By definition every set is a subset of itself.) It’s known that if a set has _n_ elements, its power set has 2ⁿ elements—observe that the above power set has 8 elements for a three element set. For Ganesha, given a set of facts, to fully understand them he must compute the power set of these facts since each subset forms an arity relationship. (Arity is the number of elements in a relationship. A set with just one element is _Un_ary, a set with two elements is Bin_ary_, and so on.). In our case, Ganesha does not need to understand Ø, the empty set, so given 6 characters he has to compute `2⁶-1=63` relationships.

As noted in the above section, [§Are we done?](#c807), Ganesha must recompute everything with every character addition. This translates the equation to `Σⁿᵣ2ʳ` but I’m not going into it. Vyasa has already won. The problem of complete understanding has translated into an exponential problem. (One way Ganesha can avoid the summation problem is to simply hear out Vyasa, wait until all facts are gathered, and then perform the needed 2ⁿ relationship computations in one go. This too implies Vyasa gets time to rest.)

Similar to the growth graph above, here’s a growth graph comparing `O(n³)` with `O(2ⁿ)`. I only go until 30 to illustrate my point. Recall that I went until 200 in the previous graph.

This graph compares the cost of computation for each of the 4 strategies described so far. Unlike the previous graph, the pink line completely dominates all the others. Before you know it, all the other lines end up so close to the X-axis that you don’t even see them. The X-axis describes the number of facts Vyasa gives Ganesha and the Y-axis is the corresponding number of computations for each strategy. Click [here](https://cdn-images-1.medium.com/max/1600/1*Vx31tNi6VFeWsTg3hti4qA.gif) if you want to see the animation from the beginning. (Source: generated by author. License: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0).)

The above graph illustrates why exponential functions are considered intractable. Notice that by around 16, 17 the O(n³) graph has been flatlined.

#### Processing power

Let’s put some numbers here. I googled for “the world’s fastest processor” and got two results. One, from 2011, saying AMD have an 8.29GHz processor with 8 cores, and another, from 2018, saying AMD have a 3.4GHz processor with 32 cores. Ignoring all the caveats, let’s suppose they’re both capable of processing instructions at their face values—8.29×10⁹×8=**6.7×10¹⁰** and 3.4×10⁹×32=**1.1×10¹¹** respectively. Taken very coarsely, this means the processors can each compute around _100 billion_ instructions in a second. In simplistic terms, (that no expert will agree to but we may for idealization), this means that they can count up to 100 billion in one second[⁵](#3025).

Let’s further suppose that Ganesha is faster than these processors. Let’s give him a processing power of 10¹⁵ instructions in a second. (Note: this is most probably a _technical_ impossibility. For one, it’s six orders of magnitude faster than the fastest clocked processor, not including the cores which are an idealization anyway. The famous Moore’s Law is expected to stop working within a decade[⁶](#c7e4). Also, I found this website, which I’ll assume is accurate, that says the fastest processor we can ever get is around 100 GHz—10¹¹ instructions per second[⁷](#055c). So we’re in very safe waters giving Ganesha this speed.)

This means that, given an O(n³) problem, Ganesha would process one hundred thousand facts in a mere second and one million facts in just 17 minutes. Barely any breathing-time for Vyasa.

undefined

On the other hand, with a O(2ⁿ) algorithm, processing just 50 facts would take Ganesha a second, processing 51 facts would take him two seconds, and processing _just_ the 127 family members in the [image](https://commons.wikimedia.org/wiki/File:Mahabharata_Partial_Family_Tree.png) (23 named characters, 97 more Kaurava brothers, and Ganga’s 7 unnamed children), would take him 1.7×10³⁸ seconds. To put that number in perspective, the age of the universe is 4×10¹⁷ seconds.

_That’s_ exponential growth.

### The end

I don’t know how Ganesha finished. Maybe he had a much faster processor. Maybe 47 is the highest arity for any relationship. But this kind of exponential growth is why Vyasa kept Ganesha’s portion to a mere 8,800 verses. Not because his verses were complicated. Both unabridged versions of the Mahabharata that I know of—P. Lal’s[¹](#19c0) “transcreation” (his word) and Kisari Mohan Ganguli’s[⁸](#b689) translation—are remarkably easy and simple to read.

Where Ganesha saddled himself, perhaps unintentionally, with _complete understanding_, philosopher Jerry Fodor worried about the most basic reasonings we humans undertake in the most ordinary of circumstances (folk psychology). He would often talk about the Frame Problem[⁹](#76a1): when we receive a new fact, how do we know (a) where in our mind we must slot this new fact and (b) how do we keep from falling into the computational conundrum described in _§Are we done_ and (c) still make the correct decisions? How is it we know which facts are relevant for the task at hand and which aren’t?

For instance, when told Yudhishtra is born how does Gandhari both know that her unborn child is no longer the first in line to the throne but also that this doesn’t affect her afternoon nap?

It’s not under dispute that we do this. It’s completely and utterly unknown _how_ we do it. Some facts affect many other things we know and we immediately and reflexively know which. We don’t have a means to describe how to organize our data in a manner such that it _won’t_ run into these problems. That’s the central problem of cognitive science. (And Artificial Intelligence too, for that matter.)

Citing Fodor:

> Though we don’t alter our cognitive commitments one by one, it’s also not true that everything we believe is up for grabs all of the time…. The long and short is: in science and elsewhere, it appears that the processes by which we evaluate nondemonstrative inferences for simplicity, coherence, conservatism, and the like are both sensitive to global properties of our cognitive commitments and tractable. What cognitive science would like to understand, but doesn’t, is how on earth that could be so. [¹⁰](#a624)

Jerry Fodor’s take (and mine, for what it’s worth) is that we don’t “actually know how the mind works…and such is the state of the art that, if God were to tell us how it works, none of us would understand Him.” [¹⁰](#a624)

#### January 2020: A Minor Update

The problem writing about technology is that it keeps changing and (typically) progressing. The _Science_ journal [reports](https://science.sciencemag.org/content/367/6473/6#sec-21) that we should expect to see the debut of an Exascale supercomputer. That’s a supercomputer which processes 10¹⁸ instructions per second. Vyasa would still win though.

### Footnotes

¹ The print version refers to the work by P. Lal of the Writers Workshop of India, Kolkota listed at [http://www.writersworkshopindia.com/](http://www.writersworkshopindia.com/).

² An introduction to Niyoga is available at [https://en.wikipedia.org/wiki/Niyoga](https://en.wikipedia.org/wiki/Niyoga).

³ Source: “_Chi Po and the Sorcerer: A Chinese Tale for Children and Philosophers”_ by Oscar Mandel (1964) cited in Raymond Smullyan’s 1983 book, “_5000 B.C. and Other Philosophical Fantasies”_.

⁴ It’s still an open topic in philosophy and cognitive science whether _mental properties_ like _wants_ and _beliefs_ actually exist. Jerry Fodor believed they do, Dan Dennett argues they don’t. For this post, Ganesha might prefer Dennett’s position. I myself take no stance in the matter.

⁵ See news articles at NotebookCheck by Matthew Conriaster (Aug 14, 2018) [https://www.notebookcheck.net/AMD-s-new-2990WX-is-now-the-world-s-fastest-CPU-with-some-caveats.322960.0.html](https://www.notebookcheck.net/AMD-s-new-2990WX-is-now-the-world-s-fastest-CPU-with-some-caveats.322960.0.html) and ZDNet by Tuan Nguyen (Sep 14, 2011) [https://www.zdnet.com/article/worlds-fastest-processor-is-an-overclocked-beast-video/](https://www.zdnet.com/article/worlds-fastest-processor-is-an-overclocked-beast-video/).

⁶ For a description of Moore’s law, see the Wikipedia page at [https://en.wikipedia.org/wiki/Moore’s\_law](https://en.wikipedia.org/wiki/Moore%27s_law). In the very first section, we have Gordon Moore, the after whom it’s named, saying “I see Moore’s law dying here in the next decade or so.”

⁷ The following link, whose accuracy I’m not qualified to judge, puts the upper bound on CPU processing speeds at 100Ghz, [https://www.physlink.com/education/askexperts/ae391.cfm](https://www.physlink.com/education/askexperts/ae391.cfm).

⁸ Kisari Mohan Ganguli’s translation of the first book is available on Gutenberg at [http://www.gutenberg.org/ebooks/7864](http://www.gutenberg.org/ebooks/7864). His books available on Gutenberg are listed at [http://www.gutenberg.org/ebooks/author/2563](http://www.gutenberg.org/ebooks/author/2563).

⁹ I should state here that this was Fodor’s interpretation of the Frame Problem. Some other computer scientists and philosophers disagreed with his use of the term.

¹⁰ Jerry Fodor, “How the mind works: what we still don’t know”, from Daedalus Volume 135, Issue 3, Summer 2006 available online at [https://www.mitpressjournals.org/doi/10.1162/daed.2006.135.3.86](https://www.mitpressjournals.org/doi/10.1162/daed.2006.135.3.86).

¹¹ Science magazine [https://science.sciencemag.org/content/367/6473/6#sec-21](https://science.sciencemag.org/content/367/6473/6#sec-21).

### Acknowledgements

Thanks go out to [Aksvij](https://medium.com/u/4fc7ae7a6d83) for, variously, editing this post, the cover photo, and suffering me the last month as I worked on this post. (I don’t count the eleven years of our marriage.)

Though I didn’t initially plan it out that way, this post is published on Ganesha’s birthday — Ganesh Chaturthi, गणेश चतुर्थी — as a tribute to Him, the great god of beginnings.

### Code

The source code used to generate the animated images used in this post are available as a GitHub gist at [https://gist.github.com/lvijay/b12f4d1d98df9ad95b2fff0c8b8ef94e](https://gist.github.com/lvijay/b12f4d1d98df9ad95b2fff0c8b8ef94e). The static images have their sources listed under them.
