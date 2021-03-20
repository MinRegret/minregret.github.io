---
layout: post
title: "Unsupervised Learning II: the power of improper convex relaxations"
authors: [elad]
mathjax: true
---

In this continuation post I'd like to bring out a critical component of learning theory that is essentially missing in today's approaches for unsupervised learning: improper learning by convex relaxations.

Consider the task of learning a sparse linear separator. The sparsity, or $$\ell_0$$, constraint is non-convex and computationally hard. Here comes the [Lasso](http://statweb.stanford.edu/~tibs/lasso.html) -- replace the $$\ell_0$$ constraint with $$\ell_1$$ convex relaxation --- et voila --- you've enabled polynomial-time solvable convex optimization.

Another more timely example: latent variable models for recommender systems, a.k.a. the matrix completion problem. Think of a huge matrix, with one dimension corresponding to users and the other corresponding to media items (e.g. movies as in the Netflix problem). Given a set of entries in the matrix, corresponding to ranking of movies that the users already gave feedback on, the problem is to complete the entire matrix and figure out the preferences of people on movies they haven't seen.\
This is of course ill posed without further assumptions. The low-rank assumption intuitively states that people's preferences are governed by few factors (say genre, director, etc.).  This corresponds to the user-movie matrix having low algebraic rank.

Completing a low-rank matrix is NP-hard in general. However, stemming from the compressed-sensing literature, the statistical-reconstruction approach is to assume additional statistical and structural properties over the user-movie matrix. For example, if this matrix is "incoherent", and the observations of the entires are obtained via a uniform distribution, then [this paper by Emmanuel Candes and Ben Recht](http://pages.cs.wisc.edu/~brecht/papers/08.Candes.Recht.MatrixCompletion.pdf) shows efficient reconstruction is still possible.

But is there an alternative to incoherent assumptions such as incoherence and i.i.d. uniform observations?

A long line of research has taken the "improper learning by convex relaxation approach" and applied it to matrix completion in works such as [Srebro and Shraibman](http://ttic.uchicago.edu/~nati/Publications/SrebroShraibmanCOLT05.pdf), considering convex relaxations to rank such as the trace norm and the max norm. Finally, in  joint work with [Satyen Kale and Shai Shalev-Shwartz](https://arxiv.org/abs/1204.0136), we take this approach to the extreme by not requiring any distribution at all, giving regret bounds in the online convex optimization model (see [previous post](http://www.minimizingregret.com/2016/07/more-than-decade-of-online-convex.html)).

By the exposition above one may think that this technique of improper convex relaxations applies only to problems whose hardness comes from "sparsity".  This is far from the truth, and in the very same [paper](https://arxiv.org/abs/1204.0136) referenced above, we show how the technique can be applied to combinatorial problems such as predicting cuts in graphs, and outcomes of matches in tournaments.

In fact, improper learning is such a powerful concept, that problems such that the complexity of problems such as learning DNF formulas has remained open for quite a long time, despite the fact that showing proper learnability was long known to be NP-hard.

On the other hand, improper convex relaxation is not an all powerful magic pill. When designing convex relaxations to learning problems, special care is required so not to increase sample complexity. Consider for example the question of predicting tournaments, as given in this [COLT open problem formulation by Jake Abernethy](http://web.eecs.umich.edu/~jabernet/OpenProblemAbernethy.pdf). The problem, loosely stated, is to iteratively predict the outcome of a match between two competing teams from a league of N teams. The goal is to compete, or make as few mistakes, as the best ranking of teams in hindsight. Since the number of rankings scales as $$N!$$, the [multiplicative weights update method](http://theoryofcomputing.org/articles/v008a006/) can be used to guarantee regret that scales as $$\sqrt{T \log N!} = O(\sqrt{T N \log N})$$. However, the latter, naively implemented, runs in time proportional to $$N!$$. Is there an efficient algorithm for the problem attaining similar regret bounds?

A naive improper learning relaxation would treat each pair of competing teams as an instance of binary prediction, for which we have efficient algorithms. The resulting regret bound, however, would scale as the number of pairs of teams over $$N$$ candidate teams, or as $$\sqrt{T N^2}$$, essentially removing any meaningful prediction property. What has gone wrong?

By removing the restriction of focus from rankings to pairs of teams, we have enlarged the decision set significantly, and increased the number of examples needed to learn. This is a general and important concern for improper convex relaxations: one needs to relax the problem in such a way that sample complexity (usually measured in terms of Rademacher complexity) doesn't explode. For the aforementioned problem of predicting tournaments, a convex relaxation that preserves sample complexity up to logarithmic factors is indeed possible, and described in the same [paper](https://arxiv.org/abs/1204.0136).

In the coming posts we'll describe a framework for unsupervised learning that allows us to use the power of improper convex relaxations.
