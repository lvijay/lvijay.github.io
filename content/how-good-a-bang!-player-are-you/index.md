---
title: "How good a Bang! player are you?"
description: "A model to grade the popular card game Bang!"
date: "2017-10-19T19:07:36.675Z"
categories: []
published: true
canonical_link: https://medium.com/@lvijay/how-good-a-bang-player-are-you-5869c39d07ac
redirect_from:
  - /how-good-a-bang-player-are-you-5869c39d07ac
---

undefined

_Bang!_ is a card game my coworkers and I have been playing over the last year. The game is short enough that a single game can be completed in half an hour. The game involves, in our opinion, a good mix of chance and strategy. These two factors combine to make the game enjoyable and playable multiple times without getting predictable or repetitive. As an advertisement for the game, consider that our group have played 300+ games and we still enjoy playing it.

Being techies, we’ve kept track of all our games and, over time, come up with a model for grading our skills. This post describes my grading model. We also use another model developed and designed by my coworker, [Matthew O’Connor](https://github.com/mattroid), but that’s for another post.

### The game

[_Bang!_](https://en.wikipedia.org/wiki/Bang!_%28card_game%29) belongs to the genre of games known as _social-deduction_ _games_. In these games, each player is assigned a secret role, known only to that player. Much of the draw of these games are towards making deductions about a player’s role based on that player’s actions (or lack thereof).

In _Bang!_, players are randomly assigned roles: Sheriff, Deputy, Outlaw, or Renegade. Depending on the number of people playing, there is always one (and only one) Sheriff, two or more Outlaws, one or more Renegades, and zero or more Deputies. The number of players of each role depends on the total number of players in the game. (A 6-player game has 1 Sheriff, 3 Outlaws, 1 Renegade, and 1 Deputy.) The Sheriff’s role isn’t secret and, at the start of the game, the player assigned it declares himself/herself as the Sheriff; all other roles are hidden until their elimination.

The win conditions for each role are as follows:

-   the Law (Sheriff and his/her Deputies) must eliminate all non-Law players (the Renegade and the Outlaws)
-   the Outlaws: eliminate the Sheriff
-   the Renegade (singular): be the last person standing with the Sheriff and eliminate the Sheriff. If there is more than one Renegade, only one of them can win.

An interesting corollary of the above rules is that if the Sheriff is eliminated (not necessarily by an Outlaw) while there are at least two other players still in play, the Outlaws win. For instance, if the only remaining players are the Sheriff, a Renegade, and a Deputy, and the Sheriff is eliminated, the Outlaws win _even though none of them are still in play_.

How players interact with one another and achieve above goals involve the game’s mechanics which I don’t go into here. Google is your friend. Buy the game and expansions. Play the game. You’ll like it. Another reason I don’t discuss the game’s mechanics is I believe this model generalizes over similar games such as [_Bang! the Dice Game_](https://www.boardgamegeek.com/boardgame/143741/bang-dice-game), [_Legends of the Three Kingdoms_](https://en.wikipedia.org/wiki/Legends_of_the_Three_Kingdoms) (LTK), and [_Samurai Sword_](https://boardgamegeek.com/boardgame/128667/samurai-sword)**_._** With tweaking, it could even find use with games like [_Mafia_](https://en.wikipedia.org/wiki/Mafia_%28party_game%29), [_The Resistance_](https://en.wikipedia.org/wiki/The_Resistance_%28game%29), and [_Secret Hitler_](https://www.nytimes.com/2017/09/05/business/secret-hitler-game.html).

This post deals with a model to grade a group of players who (predominantly) play with each other. The model takes into account that any individual group will have its own playing style and so player grading occurs on the basis of that group’s game history. After discussing the model itself, I discuss what the model gets right, what it misses, and conclude with some general strategies.

### The Model

We maintain a table with 9 columns: Winning Team, Sheriff, Deputy 1, Deputy 2, Outlaw 1, Outlaw 2, Outlaw 3, Renegade 1, Renegade 2.

The Winning Team is one of Law, Outlaw, or Renegade. As a matter of convenience, if the renegade wins a game, that renegade is listed under Renegade 1.

For every game played, we note down the team that won that game along with each player under the respective teams.

After a series of games, we look at the number of times each team has won and compute a _win probability_ for each team. Next, for each player, we look at how many times that player has been with the Law, Outlaws, and Renegades, multiply these with that team’s win probability, sum them up and get the player’s _expected wins_, `E`. We also note the player’s _actual wins_, `A`. With these two numbers, we compute the ratio `A/E`. If the ratio is greater than 1, this player has won more than expected, if it’s less than 1, the player is in the losing team more often than not.

#### Example

A game of _Bang!_ can consist of anywhere between 4–8 players. Let’s assume we have a pool of 8 players who play _Bang!_ together though they don’t necessarily play in all games. Let’s call them Aryabhata, Bertrand, Chomsky, Descartes, Euler, Fodor, Goodman, and Hume.

Let’s suppose that these 8 have played ten games and the results are tabulated as shown below.

A record of the games, the winners are highlighted.

Each row describes a game. The first column is the team that won. Each column shows the player and the role they had in that game.

In ten games, we see the Law has won twice, the Outlaws a whopping seven times, and a Renegade once. This gives us the win probability for each team as Law:0.2, Outlaw:0.7, Renegade:0.1.

The per player grades work out as shown below.

Grades for each player

The expected wins for each player is calculated as games-played-as-law×law-probability + games-played-as-outlaw×outlaw-probability + games-played-as-renegade×renegade-probability. For instance, Aryabhata’s expected-wins is computed as `(1×0.2)+(6×0.7)+(0×0.1)=4.4`.

The last column represents the players’ grades. Euler, Bertrand (Russell), and Hume consistently end up on the winning team. Bertrand Russell, though he has only two wins, won a game as a Renegade and because he played three games as a Renegade his expected wins for those games were only `0.3`. The same holds for Goodman. He played four games and, rounding up, was expected to win a game. It’s not a surprise that he won none.

**A refinement**  
While the original model works well towards calculating expected win probabilities, we found that game results varied depending on the number of players. We updated the model compute the win probabilities for each role based on the number of players in the game. In our games the Outlaws win 39% of the 5-player games whereas they win 60% of the 6-player games.

#### The good parts

What this model gets right is that it **treats fairly** roles that are are hard to win with so one isn’t penalized for losing with them. In fact, winning with a difficult role, gives a significant boost to one’s grade. Another benefit is that the weights for each role are **auto-adjusting**. The model has no preconceived notions of how to determine the win probabilities of a role and it adapts different values for different playing groups. A group where the players play aggressively, trying to eliminate others would end up with a different win probability than another group and the model captures this.

#### The bad parts

The model does not take into consideration emergent properties of the grades. For instance, do players with a high grade tend to win when they’re on the same team? How do results turn out when players with high and low grades being on the same team? While these may be discovered (as emergent properties), I don’t know how to make it feed back into the model.

An observation I’ve made is that the Law cannot win unless Renegades play as deputy for an extended period. The model does not take this into account and, given its agnosticism about the game particulars, I do not see how it can. A better model would (somehow) take into account proper Renegade play and accordingly adjust the grading. I expand more below in the section §Findings.

#### The missing parts

There are parts the model does not take into account and cannot because that information isn’t captured. The seating arrangement is one such example. The game is played with players sitting in a circle and the game’s mechanics render high relevance to where a player is seated relative to the Sheriff. Our anecdotal observation has been that if the Sheriff is flanked by the Outlaws they tend to win. If seating order were captured, that could feed back into the model to weight proximity to the Sheriff accordingly. (I’m not sure _how_ to incorporate it yet. Inputs welcome :-)

The character of involved players isn’t captured either. Some characters are _objectively_ better than others. (Looking at you, _Tuco Franziskaner_.) Keeping track of characters, roles, and results will give a more accurate expected wins calculations.

### Findings

Below are the overall win probabilities from our games.

Win probabilities for each role split by number of players

The first row is the number of players in a game. As is evident from the above, the Outlaws have an advantage in games with even number of players and the Law an advantage in games with an odd number. This largely has to do with the distribution of roles with the number of players (shown below).

4 players: 1 Sheriff, 2 Outlaws, 1 Renegade  
5 players: 1 Sheriff, 2 Outlaws, 1 Renegade, 1 Deputy  
6 players: 1 Sheriff, 3 Outlaws, 1 Renegade, 1 Deputy  
7 players: 1 Sheriff, 3 Outlaws, 1 Renegade, 2 Deputies  
8 players: 1 Sheriff, 3 Outlaws, 2 Renegade, 2 Deputies

What we’ve observed is that when the Outlaws are in a minority, the Law tend to win. By minority, this means counting the Renegade as a Deputy. This bears out when we combine the Renegades into the Law. The win probabilities show an even greater skew.

Same as above image but with Law and Renegade 1 summed up

In 4-player games, (Sheriff, 2 Outlaws, and 1 Renegade), the Law has no allies. However, summing up win probabilities for the Law and Renegade gives us an almost 50–50 split between the Law and the Outlaws. In a 5-player game, the Law outnumber the Outlaws by 1 person. In a 6-player game, they are even. I believe we see the Outlaws up by 10 percentage-points because the Outlaws have but one target — the Sheriff — but the Deputies and Renegades do not know who’s who. Since a Deputy’s strategy is typically to attack players who are not the Sheriff, there are probably multiple instances of “friendly fire” — to borrow a term from the US army. Unfortunately, we don’t track these and hence do not know if this _is_ the case. Storing seating order would help answer this question.

When the Outlaws have a player minority their win probabilities decrease progressively with the number of players.

### Finishing up

If you’re already playing the game of _Bang!_ I hope this is a way for you to keep track and grade your games. If you have your own models I’d very much like to hear of them. If you can enhance these models, that would be great.
