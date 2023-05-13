---
title: "Toddler Typing: Emacs to the rescue"
description: "Custom Emacs major-mode to ease a toddler into using computers"
date: "2017-12-30T16:39:06.567Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/toddler-typing-emacs-to-the-rescue-6b653ce5bcaa
redirect_from:
  - /toddler-typing-emacs-to-the-rescue-6b653ce5bcaa
---

Jasper Johns, [_Alphabet, 1963_](https://www.flickr.com/photos/lurie/27314908113)

My son loves the computer. He sees me touch-typing and he wants to do the same. Of course, all he does is button mash and the results are usually disastrous.

At around age 3 he started to learn the alphabet and could actually tell which letter was which. Suddenly the glyphs on the computer keyboard were random squiggles no more but something meaningful. I let him type on the keyboard that he could see his handiwork on the screen (pun intended).

Computer keyboards have a serious design flaw that I’d never before noticed. The keys are all in upper case but the results of typing are all in lower case. To a child just learning the alphabet this is quite confusing. Given that he still loves to button mash, keeping the Caps Lock key down is not an option (he’ll probably press it, it won’t be Caps Lock any more and we’re back to seeing lower case letters). Also, it wouldn’t work because I _hate_ (absolutely _loathe_) the Caps Lock key and always set it to function as a Ctrl key thereby giving my keyboard an extra Ctrl. You could say I’m a Ctrl freak. (This post is full of bad puns.)

Emacs to the rescue. [GNU Emacs](https://www.gnu.org/software/emacs/), for the uninitiated, is the best editor ever written in the history of humanity. Its origins trace to approximately 1976. In its current incarnation, it probably traces back to the early 1980s and is among the flagship products of the [GNU Project](https://www.gnu.org/gnu/gnu.html) and the [Free Software Foundation](https://www.fsf.org/).

Emacs is a highly customizable software and the perfect tool for my purposes. It supports different types of formatting depending on what kind of a file is being edited. For instance, if you’re editing files in the Python programming language, it’ll do Python specific formatting for you; if you’re browsing the Internet it’ll [highlight links, show your images](https://www.reddit.com/r/emacs/comments/4srze9/watching_youtube_inside_emacs_25/) etc; back in 2012, if you wanted to read your twitter feed ([shameless plug](https://github.com/lvijay/twitching/)) Emacs was up to the task; or if you just want to take down notes, Emacs’s [org-mode](http://orgmode.org/) lets you do so and beautifully. Anyway, each of these individual file-type-based options are, in Emacs terms, called _Major Modes._

To allow my son explore the computer keyboard I wrote a custom [major-mode](https://gist.github.com/lvijay/1b3a7df4369a7ec02980732eefbce34c) which just prints all alphabets in upper-case. The default font in emacs is `monospaced` and the zeros showed up as `0` which jarred with his experience. Not a problem. The major-mode prints all `0`s as upper case `O` (Oh).

A more recent addition to the roster is reading the numbers that are written. When the cursor (_point_ in emacs lingo) is over a number and the F8 key is pressed the computer reads out the number. It uses a combination of other GNU software `echo` and `[gawk](https://www.gnu.org/software/gawk/)` and the program `say` which ships with all Macs.

So far it’s been great fun. In addition, I’ve also been able to surreptitiously teach him addition, reading, and writing.

It’s only fair that I end with a pun. I asked him to use phonetics and write the name of his favorite superhero, Ironman. He ended it with “N-M-A-N” but he started it with “[I-Y-E-R](https://en.wikipedia.org/wiki/Iyer)” and it was perfect.

### The code

For privacy, I’ve redacted my son’s name.
