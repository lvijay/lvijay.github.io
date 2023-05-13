---
title: "Ken Thompson and John Searle one-up Déscartes"
description: ""
date: "2023-05-13T11:45:03.310Z"
categories: []
published: false
---

Ken Thompson, source: [ACM Turing Awards](https://amturing.acm.org/images/thompson-1.jpg)

Seventeenth century philosopher, René Descartes would’ve fit right in with modern computers. In his 1641 book, _Meditations on First Philosophy_, in sixty odd pages, he called into doubt everything and concluded with the existence and goodness of god. In an [earlier post](https://medium.com/galileo-onwards/rené-descartes-security-engineer-777a3d051864) I discussed how his philosophical thesis perfectly fit Computer Security models. In this post we revisit his thesis, in slightly more detail than that post but keeping computers as the model, and break it. To break his thesis, we’ll follow Ken Thompson’s lead.

Ken Thompson is a computer pioneer widely considered cofounder of the UNIX® operating system (an attribution he rejects). The UNIX® system is still the model for today’s more popular operating systems such as [GNU/Linux](https://www.gnu.org/gnu/linux-and-gnu.en.html) (in [various distributions](https://www.gnu.org/distros/free-distros.en.html)). In 1984, Thompson won the Turing Award, the most prestigious award for people in the Computer Science profession. For his Turing Award lecture, he wrote a short, three-page article titled “[Reflections on trusting trust](https://dl.acm.org/citation.cfm?id=358210)”. This article shows us the deep flaw in Descartes’s thesis.

In the appendix, we’ll briefly discuss whether Descartes himself recognized these flaws. It’s likely he did which only, in my opinion, more highlights his genius.

### Descartes’s thesis

To recap, here’s a _really_ short summary of Decartes’s _Meditations on First Philosophy_. It has to be short because the book itself is only around 60 pages. ¹

#### Meditations on First Philosophy

Descartes starts with wondering if everything he knows is a lie. He asks, look, how can I trust my senses? how can I know that what I see is the real world and not some illusion? after all, several times, I’ve had dreams that _during the course of the dream_ felt real but upon awaking I realized that they weren’t real. how do I know that isn’t the case now?

Fine, said Descartes, “I will suppose, then, that everything I see is spurious. I will believe that my memory tells me lies, and that none of the things that it reports ever happened. I have no senses. Body, shape, extension, movement and place are chimeras.” Instead, like “Archimedes used to demand just one firm and immovable point in order to shift the entire earth; so I too can hope for great things if I manage to find just one thing, however slight, that is certain and unshakeable.”

With that nice Archimedes metaphor, Descartes concludes he can only be sure of his own existence. Not his body or his senses but his own thinking.

#### Lost in the supermarket

To more easily understand Descartes, let’s make a stop at the supermarket. Specifically, let’s take a look at the supermarket’s barcode scanner.

A simple barcode scanner. Annotated by author. Image taken from [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:CCD_Barcode_Scanner.jpg). License: public domain.

A simple barcode scanner consists of four components: a camera, a button, a processor, and an output device. (Lest plastic mould manufacturers complain, I’ll admit there’s more to the scanner but these are the ones that matter to us.)

When you point the scanner’s camera at a barcode and press the button the processor reads the input from the camera, interprets it as a barcode number and sends that through the output wire. If you point the camera at something that’s not a barcode and still press the button, nothing will go on the output. Sometimes, as I’m sure you’ve experienced, even pointing the camera at a real barcode sends no outputs to the billing machines.

A simple barcode. On the left, the barcode and on the right the output results returned by the scanner. Source: Wikipedia page on barcodes. Licence

ab

  

### Ken Thompson calls

---

### Appendix–Descartes’s propaganda

When Descartes wrote the _Meditations_, he had only one concern—the Church. What he really wanted people to focus on were his works in mathematics² and physics but the Church was after him. Descartes didn’t want to suffer the fate of Galileo Galilei. Just a few years prior, in 1633, Galileo was arrested and later consigned to a house-arrest in which he remained through the rest of his life. And only in 1600 was Giordano Bruno burned on the stake—again by the Catholic Church.

1

### Footnotes

¹ The book used in this post, [https://www.cambridge.org/9780521191388](https://www.cambridge.org/9780521191388), “_René Descartes: Meditations on First Philosophy_”, Edited and Translated by John Cottingham (2013), is a mere 66 pages.

² Descartes puts the _Carte_ in _Cartesian_ mathematics.

  

 — -

[https://dl.acm.org/citation.cfm?id=358210](https://dl.acm.org/citation.cfm?id=358210) ken thompson’s turing lecture
