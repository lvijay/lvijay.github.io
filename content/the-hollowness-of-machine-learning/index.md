---
title: "The hollowness of Machine Learning"
description: "The emperor has no clothes and now some ministers are saying it out loud."
date: "2019-02-09T13:01:27.722Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/the-hollowness-of-machine-learning-b347fff17c73
redirect_from:
  - /the-hollowness-of-machine-learning-b347fff17c73
---

Ilustration of “[The Emperor’s New Clothes](https://en.wikipedia.org/wiki/The_Emperor%27s_New_Clothes "w:The Emperor's New Clothes")”, Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Emperor_Clothes_01.jpg), License: public domain.

Strong critics of Neural Networks/Machine Learning/Deep Learning (all referred to as _ML_ here) have often said that it is fundamentally wrong. Now, the field’s practitioners are beginning to admit as much. Consider two recent articles in Quanta Magazine. The first has Boris Hanin, a mathematician at Texas A&M University and a visiting scientist at Facebook AI Research, saying the following[¹](https://www.quantamagazine.org/foundations-built-for-a-general-theory-of-neural-networks-20190131)

> “\[T\]he best approximation to what we know is that **we know almost nothing about how neural networks actually work** and what a really insightful theory would be” \[my emphasis\]

That’s a pretty straightforward admission of the state of cluelessness in ML. The second article has Been Kim, research scientist at Google Brain saying:[²](https://www.quantamagazine.org/been-kim-is-building-a-translator-for-artificial-intelligence-20190110/)

> “AI is in this critical moment where humankind is trying to decide whether this technology is good for us or not, \[and i\]f we don’t solve this problem of interpretability… \[w\]e might just drop it”

Of course, both Hanin and Kim, as far as I can tell, hold that the ML approach is the right way to solve the problems it claims it can solve.

Kim also admits that there are two approaches to the “interpretability” goal and that her interests, like her employers’[³](https://en.wikipedia.org/wiki/Dodge_v._Ford_Motor_Co), are pecuniary[⁴](https://www.nytimes.com/2016/07/24/technology/they-promised-us-jet-packs-they-promised-the-bosses-profit.html).

Here’s Kim:

> “There are two branches of interpretability. One branch is interpretability for science…\[where\] you consider a neural network as an object of study, then you… conduct scientific experiments to really understand the gory details about the model.  
> “The second branch of interpretability, which **I’ve been mostly focused on, is** interpretability…. You don’t have to understand every single thing about the model… just enough to safely use the tool.” ² \[my emphasis\]

The interests are also more towards _utility_ than discovery of the truth which is not how science works. For instance, when Queen Victoria asked Michael Faraday of what use his rudimentary experiments in electricity[⁵](http://www.rigb.org/christmas-lectures/supercharged-fuelling-the-future/thermodynamics-2016-advent-calendar/15--faradays-frogs) were he (supposedly) responded with “of what use is a newborn baby?” Faraday could neither have imagined how ubiquitous electricity electricity would become nor the various ways we would use it nor the ways we would generate it. Newton could not have predicted that we would use his theories to travel to the moon, no more than Darwin could have predicted CRISPR, nor Alan Turing predicted the Internet as a medium to look at kittens. As astrophysicist Neil deGrasse Tyson says,

> When Einstein derived his equations, I’d bet neither he nor anyone else was thinking “Barcodes!” or “Lasik Surgery!” or “Rock Concerts!” [⁶](https://www.facebook.com/notes/neil-degrasse-tyson/science-in-america/10155202535296613/)

The history of science is scientists attempting to understand some phenomenon and later, sometimes, finding ways to use these discoveries.

The Quanta article also has an equally damning confession, this again by Boris Hanin (edits in original)

> if you have a specific task in mind, how do you know which neural network architecture will accomplish it best? There are some broad rules of thumb.  
> Beyond those general guidelines, however, engineers largely have to rely on experimental evidence: They run 1,000 different neural networks **and simply observe which one gets the job done**.  
> “These choices are often made by trial and error in practice,” Hanin said. “That’s sort of a tough \[way to do it\] because there are infinitely many choices and one really doesn’t know what’s the best.” \[my emphasis\]

As linguist and philosopher, Noam Chomsky, has been saying for ages: in ML “success is defined as getting a fair approximation to a mass of chaotic unanalyzed data” which won’t lead to “the kind of understanding that the sciences have always… aimed at.” [⁷](https://www.theatlantic.com/technology/archive/2012/11/noam-chomsky-on-where-artificial-intelligence-went-wrong/261637/)

---

The problem with using Black Box technologies, such as ML, is that you can quickly lose sight of who’s chasing whom, as nicely illustrated by the following joke about Native Americans predicting the weather [⁸](http://voices.washingtonpost.com/capitalweathergang/2008/11/winter_weather_joke.html):

> It was autumn, and members of a Native American tribe asked their new Chief if the coming winter was going to be cold or mild. Since he was a new Chief in a modern society and had never been taught the old secrets of Nature, he looked up at the sky and had no clue what to do. To play it safe, he replied to his tribe that the winter could definitely be cold and that they should collect firewood early, just to be prepared. So, the members began gathering wood.  
> Being a practical leader, he figured he should also use the resources available to the modern society. He went to the phone booth, called the National Weather Service and asked, “Will this winter be cold?”  
> “As of now, it looks like this winter is going to be quite cold,” the forecaster said.  
> So the Chief went back to his tribe and told them to collect even more wood. A week later he called the National Weather Service again and asked for an update.  
> “Yes,” the man at National Weather Service again replied, “based on incoming data, this winter is looking to be colder than we expected.” The Chief was surprised, but again went back to his tribe, told them that this might be a very cold winter, and asked them to collect every scrap of wood they could find.  
> One week later, the Chief called the National Weather Service yet again, hoping for a new answer. “Are you absolutely sure that the winter is going to be very cold?”  
> “Positive,” the man replied. “It’s going to be one of the coldest winters ever.”  
> “Really?” the shocked Chief exclaimed. “How can you be so sure?”  
> “First,” the forecaster replied, “The Indians are collecting firewood like crazy…”.

A real life analog to the above joke was inadvertently demonstrated in 2017. Sameer Singh, assistant professor at University of California, Irvine, spoke about a “black box” ML system, developed by his student, “to classify image\[s\]… as either a husky… or a wolf”. The “seemingly accurate \[ML system\] his student had created was in fact just learning how to recognize snow in images: if it detected snow, it predicted wolf, and if not, it predicted husky”. [⁹](http://innovation.uci.edu/2017/08/husky-or-wolf-using-a-black-box-learning-model-to-avoid-adoption-errors/)

---

Last year, I bemoaned the fact that there were no simple examples in ML. Not that anybody listens to me but it seems that now some ML practitioners feel simple examples are important for ML. The Quanta Magazine article cited above¹ discusses a 2018 paper put out by David Rolnick and Max Tegmark, a mathematician at the University of Pennsylvania and a physicist at MIT respectively. Their paper focused on using ML “to perform a simple task” because “‘\[i\]f a shallow network can’t even do \[something simple\] then we shouldn’t trust it with anything else’”. Notice, though, that the researchers are focusing more on _implementation strategies_ rather than _correctness_. A more robust approach would first try to prove that the technique achieves what it wants to and later focus on achieving the same faster. (What’s the point in developing, say, a car and optimizing its fuel injection without first confirming whether the car itself works? It’s better to first get a _working_ model before optimizing it.)

A better example from the history of science of possibly looking at the wrong place is from Robert Boyle’s experiments showing that water _transmutes_ into living matter. The experimental setup was simple and remarkably convincing. Citing from Chomsky from the above Atlantic interview,

> “\[Y\]ou take a pile of earth, you heat it so all the water escapes. You weigh it, and put \[in it\] a branch of a willow tree, and pour water on it, and measure you the amount of water you put in. When you’re done, you the willow tree is grown, you again take the earth and heat it so all the water is gone — same as before. Therefore, you’ve shown that water can turn into \[life\]. It is an experiment, it’s sort of right, but it’s just that you don’t know what things you ought to be looking for.”

### Footnotes

¹ Kevin Hartnett, “Foundations Built for a General Theory of Neural Networks”, Jan 31, 2019, [https://www.quantamagazine.org/foundations-built-for-a-general-theory-of-neural-networks-20190131](https://www.quantamagazine.org/foundations-built-for-a-general-theory-of-neural-networks-20190131).

² John Pavlus, “A New Approach to Understanding How Machines Think”, Jan 10, 2019, [https://www.quantamagazine.org/been-kim-is-building-a-translator-for-artificial-intelligence-20190110/](https://www.quantamagazine.org/been-kim-is-building-a-translator-for-artificial-intelligence-20190110/).

³ In 1919, the Michigan Supreme Court ruled that publicly owned corporations had but a sole purpose — to deliver profits to their shareholders rather than in a “manner for the benefit of \[its\] employees or customers”, [https://en.wikipedia.org/wiki/Dodge\_v.\_Ford\_Motor\_Co](https://en.wikipedia.org/wiki/Dodge_v._Ford_Motor_Co).

⁴ Lest one believe that Alphabet, Google’s parent company, Kim’s employer, is any different, see the following article in the New York Times Magazine about how Alphabet’s “moonshot” company, X, where they “encourage employees to kill projects before they become expensive”. See Conor Dougherty, “They Promised Us Jet Packs. They Promised the Bosses Profit.” Jul 23, 2016, [https://www.nytimes.com/2016/07/24/technology/they-promised-us-jet-packs-they-promised-the-bosses-profit.html](https://www.nytimes.com/2016/07/24/technology/they-promised-us-jet-packs-they-promised-the-bosses-profit.html).

⁵ To see some sample experiments Faraday performed, see [http://www.rigb.org/christmas-lectures/supercharged-fuelling-the-future/thermodynamics-2016-advent-calendar/15--faradays-frogs](http://www.rigb.org/christmas-lectures/supercharged-fuelling-the-future/thermodynamics-2016-advent-calendar/15--faradays-frogs).

⁶ Neil deGrasse Tyson, “Science in America”, Apr 21, 2017 [https://www.facebook.com/notes/neil-degrasse-tyson/science-in-america/10155202535296613/](https://www.facebook.com/notes/neil-degrasse-tyson/science-in-america/10155202535296613/).

⁷ Noam Chomsky interviewed by Yarden Katz, “Where Artificial Intelligence Went Wrong”, Nov 1, 2012, [https://www.theatlantic.com/technology/archive/2012/11/noam-chomsky-on-where-artificial-intelligence-went-wrong/261637/](https://www.theatlantic.com/technology/archive/2012/11/noam-chomsky-on-where-artificial-intelligence-went-wrong/261637/).

⁸ Ann Posegate, “Winter Weather Joke”, Nov 28, 2008 [http://voices.washingtonpost.com/capitalweathergang/2008/11/winter\_weather\_joke.html](http://voices.washingtonpost.com/capitalweathergang/2008/11/winter_weather_joke.html).

⁹ “Husky or Wolf? Using a Black Box Learning Model to Avoid Adoption Errors”, Aug 24, 2017, [http://innovation.uci.edu/2017/08/husky-or-wolf-using-a-black-box-learning-model-to-avoid-adoption-errors/](http://innovation.uci.edu/2017/08/husky-or-wolf-using-a-black-box-learning-model-to-avoid-adoption-errors/)

¹⁰ [https://medium.com/galileo-onwards/the-machine-learning-of-simple-things-e6bca6d5283f](https://medium.com/galileo-onwards/the-machine-learning-of-simple-things-e6bca6d5283f).
