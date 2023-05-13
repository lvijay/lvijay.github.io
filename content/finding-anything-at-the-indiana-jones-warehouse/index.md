---
title: "Finding anything at the Indiana Jones Warehouse"
description: "In this post I attempt to explain, to a lay audience, how information is organized for Big Data."
date: "2017-11-13T05:52:29.016Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/finding-anything-at-the-indiana-jones-warehouse-6d0436181f5a
redirect_from:
  - /finding-anything-at-the-indiana-jones-warehouse-6d0436181f5a
---

The warehouse from Indiana Jones

In this post I attempt to explain, to a lay audience, how information is organized for Big Data. I find that I understand Computer Science concepts better when I can relate them to real objects. The visualization for today’s topic is the warehouse shown at the end of the 1981 movie “_Indiana Jones and the Raiders of the Lost Ark_”. The hope is that anyone who gets to the end of this post will have a conceptual understanding of how things work in the Big Data world.

Let’s say we wish to find something in the warehouse above. Picture that this warehouse has a receptionist with an army of slaves ready to do our bidding. When we come to find anything from the warehouse, we present our case to the receptionist and he sends off the slaves to get our results. The receptionist doesn’t know everything that’s maintained in the warehouse because people keep bringing in new artifacts and removing old artifacts. So s/he only maintains details about what’s stored and where at a more approximate level and, when asked for, dispatches the slaves to search through all entries at that location. Given that this is the Indiana Jones Warehouse, we have a rough idea of what’s being stored — precious artifacts from around the world and from various time periods. Let’s come up with a hierarchical organizational scheme to easily find artifacts.

But before that we need an _addressing scheme_, i.e. a way to refer to regions of the warehouse. The warehouse is a flat grid of rows and columns. We’ll say that rows run from `A0,A1,A2,...B0,...Z9` and the columns similarly from `A0...Z9`, giving us a total of 67,600 regions. To refer to a single region of the warehouse, we’ll address it by listing its row followed by its column. So `§Z0R0` refers to row `Z0` and column `R0`. (If you think 67,600 regions is too few, adding more is trivial. One one is to include lower case letters, so that the rows and columns run as `A0,A1,A2...Z9,a0,a1,...z9`. This small change gives us 270,400 regions.) With that out of the way….

We have two top-level attributes common to all artifacts — their location of origin and their era of origin. We’ll divide the warehouse into _partitions_ (like North Africa, East Australia, Northwest Asia) and further partition them into century of artifact origin. So, one address of the warehouse will house all and only artifacts from Asia Minor of the 15th century while another section will house all and only artifacts from Siberia of the 20th century. We then store in our coarse-index the details of Region, Century, Warehouse Location. An example entry would be `North America, 16th century CE, §H0P1`. Anyone wanting to find some artifact can get the address from the index, go there, look through all the items at that address until they find their specific artifact.

Two things to note here: (1) our hierarchical scheme is semi-arbitrary — we could’ve divided the warehouse into centuries and made the regions fall under each century, there’s no necessarily right answer, it just depends on the kinds of questions asked of the warehouse; and (2) _logically_ adjacent regions don’t need to be _physically_ adjacent to one another. For instance, the warehouse location for `Mediterranean, 12th century CE` and `Mediterranean, 13th century CE` could be `§R2D2` and `§C3P0` respectively (31 blocks away from each other). There’s no principled reason for them to actually be near one another on the warehouse floor.

#### Finding stuff

Suppose we wish to find the [manuscript](http://www.nybooks.com/articles/2017/02/23/can-we-ever-master-king-lear/) of William Shakespeare’s _King Lear_, we know the following: it dates to the 17th century and belongs to England.

First we get the best region in the warehouse that represents England. We ask the receptionist

We: “What regions do you have?”  
Receptionist: North Africa, Asia Minor, South Africa, West Africa, North West Africa, Europe, South-East Asia, … \[and several more items\]

We go through the list and find the one that best covers England, say, Europe.

Then we go back to the receptionist with the details: `**in** _region_=Europe, _century_=1500 CE, _item description_ **contains** "William Shakespeare" **and** **contains** "King Lear" **and** _item_ **isa** "manuscript"`.

The receptionist first looks up the address of `«Europe, 1600 CE»` (say, `§D4Z3`) and gives the following instructions to the slaves

1.  Go to address `§D4Z3`
2.  Look at every item
3.  Read the attribute description of the item, if it contains the words `"William Shakespeare"` and the item description contains the words `"King Lear"` and it is a `"quill"`, then collect it; otherwise ignore it.
4.  Once done, return to me with the collected items.

It really is that simple. Note that though _we_ know there’s only one manuscript, neither the receptionist nor the slaves know this. And, with the above description, it’s possible that we might also get false positives like the quill of a review of William Shakespeare’s King Lear.

#### More than finding

People usually want more than just to find artifacts. They want to perform some computations like finding the earliest artifact we have from Latin America. Here, the procedure is similar to above, except we may have to look through all centuries of Latin American artifacts. The Index will contain the centuries of Latin American artifacts, but given that the earliest record of humans in Latin America dates to [18,000 years ago](https://www.csmonitor.com/Science/2015/1120/When-did-people-first-arrive-in-South-America), we’re potentially looking through 180 addresses in the warehouse. Of course, since we only want the _earliest_ artifact we just need the earliest time and we go to that address, search through and we’re done.

#### Organizational challenges

What if, instead of the earliest Latin American artifact, someone wanted to find the oldest artifact in the color fluorescent orange. Now, we have two problems — we don’t know where to look and we don’t know when we’ll stop. Our data isn’t organized by color. We have a few hints — we need the _oldest._ So we have a rough idea of where to start but we have no idea when we’ll stop.

We know that fluorescent colors were [invented](https://www.acs.org/content/acs/en/education/whatischemistry/landmarks/dayglo.html) only in the 20th century but the receptionist doesn’t. Asking the receptionist to find the _earliest_ artifact in fluorescent orange providing no additional information will entail a search across _all_ regions and _all_ times. It’ll be a long wait to get an answer.

Incorporating color into the warehouse would ease up the problem. But is it justified? What if these color requests aren’t so common. Adding that information into the receptionist’s register only makes the register bigger without sufficient pay off. There are other attributes that could also be included in the hierarchical scheme. Adding every attribute entails a cost and every cost must be justified. There’s no simple answer and warehouse organizers must determine the best scheme based on the kinds of requests the receptionist gets.

#### Other questions

No research is useful unless we ask comparative questions. Consider the question, which had more artifacts: 18th century France or 4th century West Africa? (Left as exercise.)

Or consider: how many of the Ottoman Empire’s generals had the same name as the generals of Genghis Khan’s empire? Here we send out one set of slaves to get the names of Ottoman Empire generals, another set to get Genghis Khan’s generals, and compare them.

### Different concerns

The engineers who _organize_ the warehouse and those who wish to _use_ the warehouse have different interests.

The _user_ cares about the artifacts and their particulars. And about getting their questions answered quickly. Warehouses that house different artifacts will have different concerns and different answers.

An _engineer_, on the other hand, isn’t at all interested in the actual warehouse artifacts. The ideal world for an engineer would be one where their solution is so general that it works over a wide variety of problems. In a hypothetical world, if an engineer was approached by a potential warehouse user and told that the most common uses for their warehouse were “brillig, and the slithy toves, and gyre and gimble” [\[1\]](http://www.jabberwocky.com/carroll/jabber/jabberwocky.html), the engineer would be happy to recommend organizing the warehouse in the hierarchical order of “gimbles” under “gyres” under “slithy toves” under “brilligs” without the slightest concern about what, if anything, those terms mean.

The things about which an engineers care are of a more general nature.

-   How can the warehouse be organized so that artifacts can be quickly returned (regardless of _what_ they are)?
-   What kind of searching strategies must be employed to coordinate work between slaves?
-   How do we evenly divide work amongst the slaves so they aren’t overworked? (More accurately, if work isn’t evenly divided, the results will be delayed. We don’t _actually_ care about the slaves.)
-   How do we keep the receptionist from being overloaded? (So that users don’t have to wait for results.)
-   Should we bring oft requested artifacts closer to the slaves so they can reach them quicker?
-   (Come to think of it, how do we identify _which_ artifacts are oft requested?)

The problems are endless, the solutions aplenty, the fun never ends.

This post was a about small fraction of a small corner of Software Engineering concerns.

### A mini conclusion

> “All happy families are alike; each unhappy family is unhappy in its own way.” — Leo Tolstoy, _Anna Karenina_, 1878

While what engineers enjoy solving are problems of a more abstract nature, it remains true that the real world is a messy place and every entity has its own particular challenges. And it’s in this gap that many problems remain unsolved.
