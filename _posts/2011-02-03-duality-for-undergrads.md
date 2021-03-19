---
layout: post
title:  "Duality for undergrads"
authors: [elad, daniel, Jane Doe]
mathjax: true
---

The [duality theorem](http://en.wikipedia.org/wiki/Linear_programming) of linear programming and its extensions is a fundamental pillar of optimization. It lies at the heart of an elegant theory which allows us not only to reason about the structure of continuous optimization problems, but also design combinatorial optimization and approximation algorithms.

John von Neumann said that *In mathematics you don't understand things. You just get used to them.* This is particularly true for duality (which von Neumann was the first to conjecture and essentially prove). I recall encountering linear programming duality as part of a graduate course. The standard pedagogy is first to try and *write* the dual program from the primal, and much later prove weak and strong duality, a very technical way indeed. All these years since, I still haven't gotten completely used to duality, but as close as I came is in teaching it this last semester, via a non-standard way,  to undergrads, many of whom have never taken a course in basic linear programming.

I'm familiar with three ways to prove duality. The first and hardest is via fixed-point theorems, as pioneered by von-Neumann in his proof of the minimax theorem. Don't try this on your undergrads.

The second, and most popular, is a geometric proof via the [Farkas' lemma](http://en.wikipedia.org/wiki/Farkas'_lemma). This is usually grad-student material.

The way we tried this last semester proceeds as follows:

1. Define zero-sum games, and claim equivalence to linear programming. Zero sum games are clearly a special case, to show the other direction without resorting to heavy tools requires some care, as rigorously done by [Adler](http://www.optimization-online.org/DB_FILE/2010/06/2659.pdf). However, the intuition is very clear, and we did not go into details.

2. Explain the minimax theorem. Again -- a very intuitive theorem, easier to grasp than duaity -- and equivalent by (1).

3. Prove the minimax theorem on the board. We are not going to use toplogy (fixed-point theorems) nor geometry (Farkas), but an elementary construct called experts algorithms. The method of proving the minimax theorem via experts algorithms is due to [Freund and Schapire](http://www.sciencedirect.com/science?_ob=ArticleURL&_udi=B6WFW-45GMDYD-5&_user=10&_coverDate=10/31/1999&_rdoc=1&_fmt=high&_orig=search&_origin=search&_sort=d&_docanchor=&view=c&_searchStrId=1620650650&_rerunOrigin=google&_acct=C000050221&_version=1&_urlVersion=0&_userid=10&md5=eaaa00e3349ee127d6bd7307262ba2b3&searchtype=a).

The last step is of course the main one. Here's an almost precise account of the proof:  Recall that the minimax theorem for zero sum games tells us that

$$ \lambda_A =  \max_p \min_q p^T M q = \min_q \max_p p^T M q = \lambda_B $$

Here $$M$$ is the game payoff matrix (payoffs to the row player and costs to the column player), $$p$$ and $$q$$ are distributions over the strategies of the players. The relation $$ \max_p \min_q p^T M q \le \min_q \max_p p^T M q $$ is called "weak duality", and follows easily from reasoning. The other direction, "strong duality", is where we need experts algorithms.

Consider a repeated game, in which the row player constructs $$p_t$$ at each iteration $$t \in [T]$$ according to an experts' algorithm. An experts algorithm guarantees the following: (this is the definition of an experts' algorithm)

$$ \frac{1}{T} \sum_t p_t^T M q_t \geq \frac{1}{T} \max_{p_*} \sum_t p_*^T M q_t  -- o(1) $$

Here $$t=1,2,...,T$$ are the iterations of the repeated game, $$p_t$$ is the experts' mixed strategy at time $$t$$, and $$q_t$$ can be anything.

Define the average distributions to be: $$\bar{p} = \frac{1}{T} \sum_t p_t$$ and $$\bar{q} = \frac{1}{T} \sum_t q_t$$.

We have:

$$ \lambda_A = \max_p \min_q p^T M q \geq \min_q \bar{p}^T M q = \min_q \frac{1}{T} \sum_t p_t^T M q $$

By minimizing over $$ q $$ at each game iteration instead of minimizing over $$ q $$ on all game rounds, player B can only decrease his loss (and decrease player A's profit) and hence:

$$ \min_q \bar{p}^T M q \geq \frac{1}{T} \sum_t p_t M q_t$$

where $$q_t = \arg \min_q p_t^T M q$$. By the low regret property we have

$$ \frac{1}{T} \sum_t p_t^T M q_t \geq \max_p \frac{1}{T} \sum_t p^T M q_t -- o(1) $$

Hence: $$ \frac{1}{T} \sum_t p_t M q_t \geq \max_p \frac{1}{T} \sum_t p M q_t -- o(1) \geq \min_q \max_p p^T M q -- o(1) $$

Overall we got:

$$\lambda_A \geq \lambda_B -- o(1)$$ as needed.
