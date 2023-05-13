---
title: "Deletion and Quine's Ontology"
description: "WVO Quine's \"On What There Is\" explains data retention policies."
date: "2018-05-24T19:04:32.235Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/deletion-and-quines-ontology-a9e3326a881c
redirect_from:
  - /deletion-and-quines-ontology-a9e3326a881c
---

undefined

In the software world, there are two kinds of deletes — soft and hard. A _soft_ delete is something that’s been marked for removal but is potentially retrievable; whereas a _hard_ delete means the something is now irrecoverable.

For example, moving a file into your computer’s Recycle Bin is a soft delete; “deleting” it in the Recycle Bin is a hard delete. In GMail™, deleting an email sends it to the _Trash_ folder — soft delete; and deleting it from the Trash folder itself is a hard delete. In both examples, the soft-deleted items are fully recoverable. Soft and hard deletes even have real-life analogues. I’ll leave them as an exercise to the reader.

If you’ve read the title and the previous paragraphs you probably have one of two reactions: (1), Quine’s a giant of 20th century analytic philosophy, which specific part do you mean? or (2) who on earth is Quine? I’ll get to both after a _little_ more setup.

Let’s say I manage a software system which supports deletes and let’s further suppose that all my deletes are hard deletes. Now, suppose you allege that I’ve deleted some particular data. Here I’m in a predicament for I cannot admit that I did delete the items you refer to because, for me to admit such a thing would require that I have a record of what was deleted. And if I have such a record then it means I didn’t actually delete it thus contradicting my original claim. ¹

#### Enter Quine

In his legendary 1948 paper, “On What There Is” ², analytical philosopher Willard Van Orman Quine says pretty much the above and then proceeds to answer the problem too. I don’t discuss his answers, you can read his paper (see footnote 2), but here are crucial excerpts of his argument.

> Suppose now that two philosophers, McX and I, differ…. Suppose McX maintains there is something which I maintain there is not. McX can, quite consistently with his own point of view, describe our difference of opinion by saying that I refuse to recognize certain entities.  
> When _I_ try to formulate our difference of opinion, on the other hand, I seem to be in a predicament. I cannot admit that there are some things which McX countenances and I do not, for in admitting that there are such things I should be contradicting my own rejection of them. _\[emphasis in original\]_

### Footnotes

¹ More tech savvy readers might attempt to circumvent my conditions by saying the logs can refer to merely the _id_ of what was deleted without revealing the _contents_ of deletion but this merely puts the problem one step away. To my claim that, say, my transaction was deleted, you might claim that no, your logs have a _record_ of the transaction’s `id`. To this I can claim this `transaction_id` was for _x_ dollars and if you contradict me it means you didn’t _actually_ delete the data, if you actually deleted the data, my claims about the transaction cannot be countered. (Yes, this is convoluted but also explains why companies are understandably reluctant to discard data, especially financial data.)

² A public domain version of this paper is available on Wikisource at [https://en.wikisource.org/wiki/On\_What\_There\_Is](https://en.wikisource.org/wiki/On_What_There_Is).

About the image: The image is from an 1825 book “Urania’s Mirror”. I found it on Wikipedia when I searched for “Pegasus”. Why Pegasus? From Quine’s paper, we have:

> \[T\]ake Pegasus. If Pegasus _were_ not, McX argues, we should not be talking about anything when we use the word; therefore it would be nonsense to say even that Pegasus is not. Thinking to show thus that the denial of Pegasus cannot be coherently maintained, he concludes that Pegasus is.

The Wikipedia link for the image is [https://commons.wikimedia.org/wiki/File:Sidney\_Hall\_-\_Urania's\_Mirror\_-\_Pegasus\_and\_Equuleus\_(best\_currently\_available\_version\_-\_2014).jpg](https://commons.wikimedia.org/wiki/File:Sidney_Hall_-_Urania%27s_Mirror_-_Pegasus_and_Equuleus_%28best_currently_available_version_-_2014%29.jpg).
