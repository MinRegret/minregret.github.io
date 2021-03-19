---
layout: default
title: Research
---

# Research

## Control and Reinforcement Learning

- A new framework for robust control called [Non-Stochastic Control](https://sites.google.com/view/cos59x-cct/lecture-notes). This permits control in adversarial environments via a new type of algorithm, the [Gradient Perturbation Controller](https://arxiv.org/abs/1902.08721), which also gives rise to the first [logarithmic regret](https://arxiv.org/abs/1909.05062) in online control.

  In this framework we can also control with [unknown systems](https://arxiv.org/abs/1911.12178) and [partially observed states](https://arxiv.org/abs/2001.09254).

  Recent additions include  [Non-Stochastic Control with Bandit Feedback](https://arxiv.org/pdf/2008.05523) , [Black-Box Control for Linear Dynamical Systems](https://arxiv.org/pdf/2007.06650) , [Adaptive Regret for Control of Time-Varying Dynamics](https://arxiv.org/pdf/2007.04393)

  For a survey, see [these lecture notes](https://sites.google.com/view/cos59x-cct/lecture-notes).

- Combining time series and control algorithms via the new technique of [Boosting for Dynamical Systems](https://arxiv.org/abs/1906.08720).

- The [Spectral Filtering](https://arxiv.org/abs/1711.00946), technique, and its [application to asymmetric](https://arxiv.org/abs/1802.03981) linear dynamical systems.

- Learning auto-regressive moving-average [time series with adversarial noise](http://proceedings.mlr.press/v30/Anava13.pdf).

- [Maximum-entropy exploration](https://arxiv.org/abs/1812.02690) in partially observed and/or approximated Markov Decision Processes.

- [Machine learning methods for control of medical ventilator](https://arxiv.org/abs/2102.06779), see [press release](https://www.cs.princeton.edu/news/engineering-and-artificial-intelligence-combine-safeguard-patients%E2%80%99-lives).

## Optimization for Machine Learning

Machine learning moves us from the custom-designed algorithm to generic models, such as neural networks, that are trained by optimization algorithms. For a survey see [these lecture notes](https://arxiv.org/abs/1909.03550). Some of the most useful and efficient methods for training convex as well as non-convex methods that we have worked on include:

- The [AdaGrad algorithm](http://www.jmlr.org/papers/volume12/duchi11a/duchi11a.pdf), and the technique of adaptive preconditioning.

- Sublinear optimization algorithms for [linear classification](https://arxiv.org/abs/1010.4408), [training support vector machines](http://papers.nips.cc/paper/4359-beating-sgd-learning-svms-in-sublinear-time), [semidefinite optimization](http://arxiv.org/abs/1208.5211) and to other problems.

- [Projection-free algorithms](https://arxiv.org/abs/1206.4657) for online learning in the context of recommender systems, and [the first linearly convergent projection-free algorithm.](http://arxiv.org/abs/1301.4666)

![projection-free](/research/projection-free.jpg)

## Online Convex Optimizatiom

In recent years, convex optimization and the notion of regret minimization in games, have been combined and applied to machine learning in a general framework called online convex optimization. For more information see [graduate text book](http://ocobook.cs.princeton.edu/) on online convex optimization in machine learning, or survey on the [convex optimization approach to regret minimization](https://pdfs.semanticscholar.org/cea0/1bd3c778418117f447417f7c457eac94f992.pdf). Our research spans [efficient online algorithms](https://dl.acm.org/citation.cfm?id=1296051) as well as [matrix prediction](https://arxiv.org/abs/1204.0136) algorithms, and [decision making under uncertainty and continuous multi-armed bandits](https://ieeexplore.ieee.org/document/6191328?arnumber=6191328).

{% assign image-link = "/research/cover.jpg" %}
{% include center-image.html %}

