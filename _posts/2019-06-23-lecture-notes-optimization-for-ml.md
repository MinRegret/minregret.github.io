---
layout: post
title: "Lecture notes: optimization for ML"
authors: [elad]
---

Spring semester is over, yay! To celebrate summer, I've compiled lecture notes from the graduate course COS 598D, a.k.a. "[optimization for machine learning](https://sites.google.com/view/optimization4machinelearning/home)".

The course is an aftermath of a few lectures and summer school tutorials given in various locations, in which  lectures goal of the course was to present the most useful methods and ideas in a rigorous-but-not-tedious way:

-   Suitable for a mathematically-prepared undergraduate student, and/or researcher beginning their endeavor into machine learning.
-   Focus on the important: we start with stochastic gradient descent for training deep neural networks.
-   Bring out the main ideas: i.e. projection-free methods, second-order optimization, the three main acceleration techniques, qualitatively discuss the advantages and applicability of each.
-   *short* proofs, that everyone can follow and extend in their future research. I prefer being off by a constant/log factor from the best known bound with a more insightful proof.
-   Not loose track of the goal: generalization/regret, rather than final accuracy. This means we talked about online learning, generalization and precision issues in ML.

The most recent version can be downloaded here:\
[OPTtutorial](https://drive.google.com/open?id=1GIDnw7T-NT4Do3eC0B5kYJlzwOs6nzIO "OPTtutorial")

This is still work in progress, please feel free to send me typos/corrections, as well as other topics you'd like to see (on my todos already: lower bounds, quasi-convexity, and the homotopy method).

Note: zero-order/bandit optimization is an obvious topic that's not address. The reason is purely subjective -- it appears as a chapter in [this textbook](http://ocobook.cs.princeton.edu/) (that also started as lecture notes!).
