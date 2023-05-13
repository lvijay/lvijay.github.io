---
title: "A Defense of Facebook’s Revenge-Porn Plan"
description: "Facebook’s pilot to address revenge porn is a good one."
date: "2018-01-06T12:55:53.407Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/a-defense-of-facebooks-revenge-porn-plan-b429882b5e4
redirect_from:
  - /a-defense-of-facebooks-revenge-porn-plan-b429882b5e4
---

undefined

Facebook recently announced a pilot program which encourages concerned users to defensively upload their own nude photos to Facebook’s servers to defend themselves from others who might (a) have access to their compromising photos and (typically, for vindictive reasons) (b) upload them to Facebook.

I’m not going to discuss all of it here. You can read about it on their website. ¹ The tech podcast, Data Knightmare also discussed it but negatively. ²

The part I’m going to address here is the uproar over Facebook’s statement that a human will first review all uploaded images.

As preamble, here’s a joke (slightly modified).

> A man in a hot air balloon realized he was lost. He reduced altitude and spotted a man below. He descended a bit more and shouted,  
> “Excuse me, can you help me? I don’t know where I am.”  
> The man below replied, “You are in a hot air balloon hovering approximately 30 feet above the ground. You are between 37.3 and 37.5 degrees north latitude and between 121.8 and 123.0 degrees west longitude.”  
> “You must be an engineer,” said the balloonist.  
>  “I am,” replied the man, “How did you know?”  
>  “Well,” answered the balloonist, “everything you told me is technically correct, but I have no idea what to make of your information, and the fact is I am still lost. Frankly, you’ve not been much help so far.”  
> The engineer replied: “you don’t know where you are or where you are going. You are in your position because of your own mistakes and you expect me to solve your problem. The fact is, you are in exactly the same position you were in before we met, but now, somehow, it’s my fault.” ³

Below are the comments of Facebook’s Chief Security Officer, Alex Stamos. He makes a good argument and I don’t have much to add. I’m merely going to expand on his phrase “adversarial reporting” and agree with the last comment.

> We are aware that having people self-report their images carries risk, but it’s a risk we are trying to balance against the serious, real-world harm that occurs every day when people (mostly women) can’t stop NCII \[Non-Consensual Intimate Imagery\] from being posted. In recognition of that risk, we have taken the steps we can to protect this data and to only retain non-reversible hashes. To prevent adversarial reporting, at this time we need to have humans review the images in a controlled, secure environment. A personal comment:… Our greater infosec/privacy community, including the media, has trouble talking about imperfect solutions to serious problems. ⁵

#### Adversarial Reporting

First, let’s acknowledge that the idea of “revenge porn” is not one Facebook has created. Horrible people have been doing horrible things for all of our evolutionary history. The difference in the modern world is that embarrassing messages can be spread much, much more quickly causing problems for the persons concerned.

When implementing a solution, care must be taken to ensure that it may not be misused. Facebook’s solution to counter NCIIs involves converting an image into multiple strings (_hashes_) that don’t resemble the original image at all. It’s impossible to recreate the original image from these hashes. (Facebook doesn’t store the images.)

Everything here is perfect only if the images submitted are actually NCIIs. But consider what could happen if Facebook has a fully automated system without human intervention:

-   Alice maintains a popular Facebook page in which she posts (say) flowers.
-   Bob gets access to some of her unused flower photos.
-   Bob submits them to Facebook as _his_ NCIIs.
-   Facebook hashes the images, they’re stored in its backend system and the original images are deleted.
-   Alice uploads her flowers only to find that Facebook’s system rejects them as NCII.

To avoid flagging perfectly normal images as NCIIs a human _must_ review the images. I really don’t understand the uproar in this case.

#### “imperfect solutions to serious problems”

Stamos is correct to complain about the media’s inability to discuss “imperfect solutions to serious problems”.

Facebook is rather like the engineer in the above joke. The problem of revenge porn isn’t one Facebook caused. ⁴ The larger problem _cannot_ be solved perfectly or in a general manner, certainly not with today’s technology.

The world is a messy place and imperfect solutions that address problems without causing additional ones are better than inaction.

### Footnotes

¹ Facebook’s blog post describing their program [https://newsroom.fb.com/news/h/non-consensual-intimate-image-pilot-the-facts/](https://newsroom.fb.com/news/h/non-consensual-intimate-image-pilot-the-facts/).

² Data Knightmare, Episode 5 available at [http://dataknightmare.eu/](http://dataknightmare.eu/)

³ Modified from [http://design.caltech.edu/erik/Misc/balloon.html](http://design.caltech.edu/erik/Misc/balloon.html).

⁴ Seriously, look at Wikipedia’s page on the topic [https://en.wikipedia.org/wiki/Revenge\_porn](https://en.wikipedia.org/wiki/Revenge_porn).

⁵ Alex Stamos’s tweets are shown below:

⁶ Image source: [https://en.wikipedia.org/wiki/File:Ballooning\_Away\_in\_Maasai\_Mara.jpg](https://en.wikipedia.org/wiki/File:Ballooning_Away_in_Maasai_Mara.jpg)
