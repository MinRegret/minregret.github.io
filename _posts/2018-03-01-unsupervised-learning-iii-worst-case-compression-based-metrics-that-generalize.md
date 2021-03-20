---
layout: post
title: "Unsupervised learning III: worst-case compression-based metrics that generalize"
authors: [elad]
---

This post is a long-overdue sequel to parts I and II of previous posts on unsupervised learning.  The long time it took me to publish this one is not by chance -- I am still ambivalent on the merit, or lack of, for the notion of a worst-case PAC/statistical learnability (or, god forbid, regret minimization) without supervision.

And yet,\
1\. I owe a followup to the stubborn few readers of the blog who have made it thus far.\
2\. The algorithms we'll discuss are mathematically correct, and even if completely useless in practice, can serve as amusement to us, fans of regret minimization in convex games.\
3\. I really want to get on to more exciting recent developments in control that have kept me busy at night...

So, here goes:

The idea is to define unsupervised learning as PAC learning in the usual sense, with a real-valued objective function, and specially-structured hypothesis classes.

-   A hypothesis is a pair of functions, one from domain to range and the other vice versa, called encoder-decoder pair.
-   The real-valued loss is also composed of two parts, one of which is the reconstruction error of the encoding-decoding scheme, and the other proportional to encoding length.

Et-voila, all notions of generalizability carry over from statistical learning theory together with dimensionality concepts such as Rademacher complexity.

More significantly -- these worst-case definitions allow improper learning of NP-hard concepts. For the fully-precise definitions, see  the [paper with Tengyu Ma](https://arxiv.org/abs/1610.01132). The latter also gives a striking example of a very well-studied NP-hard problem, namely dictionary learning, showing it can be learned in polynomial time using convex relaxations.

Henceforth, I'll give a much simpler example that perhaps illustrates the concepts in an easier way, one that arose in conversations with our post-docs [Roi Livni](http://www.cs.princeton.edu/~rlivni/) and [Pravesh Kothari](http://www.cs.princeton.edu/~kothari/).

This example is on learning the Mixture-Of-Gaussians (MOG) unsupervised learning model, one of the most well-studied problems in machine learning. In this setting, a given distribution over data is assumed to be from a mixture distribution over normal random variables, and the goal is to associate each data point with the corresponding Gaussian, as well as to identify these Gaussians.

The MOG model has long served as a tool for scientific discovery, see e.g. this [blog post by Moritz Hardt](http://blog.mrtz.org/2014/04/22/pearsons-polynomial.html) and links therein. However, computationally it is not well behaved in terms of worst-case complexity. Even the simpler "k-means" model is known to be NP-hard.

Here is where things get interesting: using reconstruction error and compression as a metric, we can learn MOG by a seemingly different unsupervised learning method -- Principle Component Analysis (PCA)! The latter admits very efficient linear-algebra-based algorithms.

More formally: let $$X \in R^{m \times d}$$ be a data matrix sampled i.i.d from some arbitrary distribution $$x \sim D$$. Assume w.l.o.g. that all norms are at most one. Given a set of k centers of Gaussians, $$\mu_1,...,\mu_k$$, minimize reconstruction error given by
$$E_{x \sim D} [ \min_i \| \mu_i - x \|^2]$$.

A more general formulation, allowing several means to contribute to the reconstruction error, is
$$E_{x \sim D} [ \min_{ \| \alpha_x\|_2 \leq 1  }  \| \sum_{j} \alpha_j  \mu_j - x \|^2  ]$$.
Let $$M \in R^{d \times k}$$ be the matrix of all $$\mu$$ vectors. Then we can write the optimization problem as
$$ \min_{M} E_{x \sim D} [ \min_{ \| \alpha_x\|_2 \leq 1  }  \|   x  - M \alpha_x \|^2  ]  $$
This corresponds to an encoding by vector $$\alpha$$ rather than by a single coordinate. We can write the closed form solution to $$\alpha_x$$ as: $$ \arg \min_{\alpha_x }    \|   x  - M \alpha_x \|^2   = M^{-1} x $$ and the objective becomes $$ \min_{\alpha_x }    \|   x  - M \alpha_x \|^2   = \| x - M M^{-1} x\|_\star^2 $$ for $$\| \|_\star$$ being the spectral norm. Thus, we're left with the optimization problem of $$ \min_{M} E_{x \sim D} [  \|   x  - M M^{\dagger} x \|_\star^2  ]  $$ which amounts to PCA.

We have just semi-formally seen how MOG can be learned by PCA!

A more general theorem applies also to MOG that are not spherical, some details appear in the paper with Tengyu, in the section on spectral auto-encoders.

The keen readers will notice we lost something in compression along the way: the encoding is now a k-dimensional vector as opposed to a 1-hot k-dimensional vector, and thus takes $$k \log \frac{1}{\epsilon}$$ bits to represent in binary, as opposed to $$O(\log k)$$. We leave it as an open question to come up with an *efficient* poly-log(k) compression that matches MOG. The solver gets a free humus at Sayeed's, my treat!
