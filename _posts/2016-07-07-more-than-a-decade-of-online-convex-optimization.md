---
layout: post
title: More than a decade of online convex optimization
authors: [elad]
---

This nostalgic post is written after a [tutorial in ICML 2016](http://www.cs.princeton.edu/~ehazan/tutorial/tutorial.htm) as a recollection of a few memories with my friend [Satyen Kale](http://www.satyenkale.com/).

In ICML 2003 Zinkevich published his paper "[Online Convex Programming and Generalized Infinitesimal Gradient Ascent](https://www.aaai.org/Papers/ICML/2003/ICML03-120.pdf)" analyzing the performance of the popular gradient descent method in an online decision-making framework.

The framework addressed in his paper was an iterative game, in which a player chooses a point in a convex decision set, an adversary chooses a cost function, and the player suffers the cost which is the value of the cost function evaluated at the point she chose. The performance metric in this setting is taken from game theory: minimize the regret of the player -- which is defined to be the difference of the total cost suffered by the player and that of the best fixed decision in hindsight.

A couple of years later, circa 2004-2005, a group of theory students at Princeton decide to hedge their bets in the research world. At that time, finding an academic position in theoretical computer science was extremely challenging, and looking at other options was a reasonable thing to do. These were the days before the financial meltdown, when a Wall-Street job was the dream of Ivy League graduates.

In our case -- hedging our bets meant taking a course in finance at the ORFE department and to look at research problems in finance. We fell upon Tom Cover's timeless paper "[universal portfolios](http://www-isl.stanford.edu/~cover/papers/paper93.pdf)" (I was very fortunate to talk with the great information theorist a few years later in San Diego and him tell about his influence in machine learning). As good theorists, our first stab at the problem was to obtain a polynomial time algorithm for universal portfolio selection, which we did. Our paper didn't get accepted to the main theory venues at the time, which turned out for the best in hindsight, pun intended 🙂

Cover's paper on universal portfolios was written in the language of information theory and universal sequences, and applied to wealth which is multiplicatively changing. This was very different than the additive, regret-based and optimization-based paper of Zinkevich.

One of my best memories of all times is the moment in which the connection between optimization and Cover's method came to mind. It was more than a "guess" at first: if online gradient descent is effective in online optimization, and if Newton's method is even better for offline optimization, why can we use Newton's method in the online world? Better yet -- why can't we use it for portfolio selection?

It turns out that indeed it can, thereby the [Online Newton Step](http://cs.princeton.edu/~ehazan/papers/log-journal.pdf) algorithm came to life, applied to portfolio selection, and presented in COLT 2016 (along with a follow-up paper devoted only to portfolio selection, with [Rob Schapire](http://rob.schapire.net/). Satyen and me had the nerve to climb up to Rob's office and waste his time for hours at a time, and Rob was too nice to kick us out...).

The connection between optimization, online learning, and the game theoretic notion of regret has been very fruitful since, giving rise to a multitude of applications, algorithms and settings. To mention a few areas that spawned off:

-   Bandit convex optimization -- in which the cost value is the only information available to the online player (rather than the entire cost function, or its derivatives).
    This setting is useful to model a host of limited-observation problems common in online routing and reinforcement learning.
-   Matrix learning (also called "local learning") -- for capturing problems such as recommendation systems and the matrix completion problem, online gambling and online constraint-satisfaction problems such as online max-cut.
-   Projection free methods -- motivated by the high computational cost of projections of first order methods, the Frank-Wolfe algorithm came into renewed interest in recent years. The [online version](http://icml.cc/2012/papers/292.pdf) is particularly useful for problems whose decision set is hard to project upon, but easy to perform linear optimization over. Examples include the spectahedron for various matrix problems, the flow polytope for various graph problems, the cube for submodular optimization, etc.

-   Fast first-order methods -- the connection of online learning to optimization introduced some new ideas into optimization for machine learning. One of the first examples is the [Pegasus](http://ttic.uchicago.edu/~nati/Publications/PegasosMPB.pdf) paper. By now there is a flurry of optimization papers in each and every major ML conference, some incorporate ideas from online convex optimization such as adaptive regularization, introduced in the [AdaGrad](http://www.magicbroom.info/Papers/DuchiHaSi10.pdf) paper. 

There are a multitude of other connections that should be mentioned here, such as the recent literature on adversarial MDPs and online learning, connections to game theory and equilibrium in online games, and many more. For more (partial) information, see our [tutorial webpage](http://www.cs.princeton.edu/~ehazan/tutorial/tutorial.htm) and this [book draft](http://ocobook.cs.princeton.edu/OCObook.pdf). 

It was a wild ride! What's next in store for online learning? Some exciting new directions in future posts...
