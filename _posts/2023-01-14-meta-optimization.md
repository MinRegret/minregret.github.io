# Meta Optimization, adaptive gradient methods and parameter-free optimization

by Xinyi Chen and Elad Hazan

  
  

The study of mathematical optimization is a hallmark of the application of the scientific method to almost all engineering fields. With the rise of machine learning, methods shifted from interior point methods based on Newton’s methods to first order methods (FOM). The most popular and efficient FOM are adaptive gradient methods (AGM),[see chapter 6 of lecture notes here](https://arxiv.org/pdf/1909.03550.pdf) and also explained below.

Recent refinements to FOM, that are motivated by AGM, are adaptations that remove the need for fine-tuning of parameters. These include a flurry of recent papers, to give a short list:  
1. [coin-betting methods](https://arxiv.org/abs/1602.04128)

2. [D-adaptation](https://arxiv.org/abs/2301.07733)

3. [DoG optimizer](https://arxiv.org/abs/2302.12022)

4. [Mechanic learning rate tuner](https://arxiv.org/pdf/2306.00144.pdf),

5. [SAMUEL method based on adaptive regret](https://arxiv.org/pdf/2203.01400.pdf),

and definitely more that are not surveyed here.

  

The developments in mathematical programming that led to AGM and its refinements is rooted in the following fundamental question:

  

## CAN WE AUTOMATICALLY FIND THE BEST OPTIMIZER FOR A GIVEN TASK?

  

In a recent work, we give a surprising positive answer to this question that stems from the same motivation as AGM, in a very general setting of mathematical optimization called meta-optimization. The solution proposed is based on a new formulation of optimization as online control, and makes crucial use of tools in a new methodology of online control called [online nonstochastic control](https://arxiv.org/abs/2211.09619).

  

In this post we summarize this recent optimization framework and how it relates to AGM and parameter-free auto-tuning methods.

  

## The motivation for Meta Optimization

  

The motivation for meta-optimization is the question of how to learn the best optimizer for given tasks. We approach this question from an [online convex optimization](https://arxiv.org/abs/1909.05207) perspective:  
In [meta-optimization](https://arxiv.org/abs/2301.07902), the optimizer is given a sequence of tasks, and can make T optimization steps per task. These tasks can be separate optimization problems, such as neural network training tasks, or online learning problems where data arrives iteratively in an online manner.

  

At each step, the optimizer suffers instantaneous costs, and the goal is to compete with the best optimization algorithm in hindsight in terms of total cost. We call the excess total cost the “meta-regret”, since this notion is analogous to the usual definition of regret in vanilla online optimization. If we can develop a method with sublinear meta-regret, then we can argue that this method converges to the cost of the best optimization algorithm on average, and compete with it.

  

Here is an illustrative example: consider an optimization task of linear regression over random data, i.i.d. sampled from the same distribution. Such an interesting setting was proposed in [this paper](https://arxiv.org/abs/2002.04756), where the motivation was to design the best FOM for a certain data distribution in linear regression problems. The plot below shows training error decrease as a function of time, where the error bars represent different trials. The band around meta-optimization shows that over time, the algorithm’s performance improves; meanwhile, there is almost no variation around the performance of the other methods. The meta-optimization approach improves over time as it learns the best optimizer for the task. Below we explain this experiment and the entire approach a bit more precisely…

  

![](https://lh4.googleusercontent.com/NOTAsZcKkyZGz_7SaXbVvNcI0q3Xc2D1zBUuaGfHDMiYYJjeBokx5QuQTLJUgd3Xt4sHgFknzFz7FqNQIo3tF9IgZ36HO50n7c2lhzrA6lVUWW4Agg-5NcgTy90DrSKSufObtYtE3RCDI0TPgnUyma4)

  
  
  
  

## Why is learning the learning rate hard?

  

Consider a restricted setting of learning the best optimizer, where we are given an optimization problem with T fixed learning rate gradient descent iterations, and the goal is to find the best learning rate to minimize the objective function at the last iteration. Finding the optimal gradient descent learning rate takes the form of the following minimization problem:

$$\min_\eta f(x_T),\ \ \text{subject to } x_{t+1} = x_t - \eta\nabla f(x_t).$$

We can unroll the minimization objective from the initial point $x_1$,

$$f(x_T) = f(x_1 - \eta\nabla f(x_1) - \eta\sum_{t=2}^{T-1} \nabla f(x_t)) = f(x_1 - \eta\nabla f(x_1) - \eta \nabla f(x_1 - \eta\nabla f(x_1)) - ...)$$

From this expression, it is clear that $f(x_T)$ is a nonconvex function of $\eta$. This means that the natural approach of applying FOM to the learning rate itself, a.k.a. Hypergradient descent, is not guaranteed to converge to global optimality.

Meta optimization methods guarantee competing with the global optimum for the learning rate, for example for the case of convex quadratic objectives!

## Adaptive gradient methods

  

The search for the best algorithm for a given problem has a long history, and perhaps the biggest success story thus far is the development of adaptive gradient methods. In this section we review the development of AGM and the intuition behind them.

  

The theory of adaptive regularization is well-developed and highly active, and has led to numerous algorithmic refinements that have shaped the field of optimization for machine learning. Here is a nice illustration by Sebastian Ruder on adaptive optimizers vs. SGD, showing clear acceleration

[http://ruder.io/optimizing-gradient-descent/](http://ruder.io/optimizing-gradient-descent/)

![](https://lh6.googleusercontent.com/z-B-wZVbGF5HFGZn4xaEB5IX9D7y2ynaNWtQsI4-oG56-qAuZ4Tyi3T8W9XUzlEFKMAHtuEuxAqWmx775liWqolE-8zuP9_TaPesn81Dyw5aP1JbSPAR-OdpP590SnpAhoLmfX-64wK8wUDtVxbNRX8)

  

Adaptive optimizers reach state of the art in a variety of deep learning tasks, in both generalization and training error. But what is the theory behind them?

  

Let’s start from the textbook basics: stochastic gradient descent for non-smooth convex optimization. This is without loss of generality, since one can reduce the problem of finding an approximate local minimum of a smooth non-convex function (say the training error for a deep neural network) to iterated convex optimization (see Lemma A.21 [here](https://arxiv.org/pdf/1806.02958.pdf)).

SGD has the following update rule

$$x_{t+1} \leftarrow x_t - \eta \tilde{\nabla}_t$$

  

Where $ \tilde{\nabla}_t $ is a random estimator for the gradient (given by usually looking at only a few examples out of the training set). The textbook proof says that SGD for non-smooth convex optimization converges to the optimal solution at a rate of
$$O(\frac{ \sqrt{ \sigma^2 } }{\sqrt{T} } ).$$

  

Here $\sigma^2$ is the variance of the stochastic gradient estimator, and T is the number of iterations. The variance has clear importance to the overall running time. This rate is optimal, and obtained by carefully tuning the learning rate $\eta$ to be inversely proportional to the variance, more precisely, $\eta = O(\frac{1}{\sqrt{t \sigma^2}})$. The proof of this fact is elementary, and details can be found in [these lecture notes](https://arxiv.org/abs/1909.03550), chapter 2.

  

The intuition for adaptive regularization is now simple: consider an optimization problem, in which each coordinate is independent of the rest. It is reasonable to fine tune the learning rate for each coordinate separately - to achieve optimal convergence in that particular subspace of the problem, independently of the rest.

  

Thus, it is reasonable to change the SGD update rule to the more robust

$$x_{t+1} \leftarrow x_t - D_t \nabla_t ,$$

where $D_t$ is a diagonal matrix that contains in coordinate $(i,i)$ the learning rate for coordinate i in the gradient. Thus, the robust version of stochastic gradient descent should behave as the above equation, with the empirical variance on the diagonal of $D_t$,

$$D_t(i,i) = \frac{1}{\sqrt{\sum_{i < t} \nabla_t(i)^2}} .$$

This is exactly the diagonal version of the Adagrad algorithm!

  

The intuition above can give rise to strong theorems about regularization in online learning. But what is regularization and why is it useful? Regularization can be seen as a method of transforming the geometry of space in order to condition the optimization problem for faster first order optimization, as in the illustration below.

  

![](https://lh5.googleusercontent.com/ts9CIRyFeAQ_iRGNTar4hZnwYjRfpCfV4w9Os-uypVZnM8wD_nzA8Uas1Prx7Pw23tEZvfZRxIqMVLtohZzLbVN_LRj633GBZikt2Y7ExGnryFggYezDaty3rrX1-ucnH_HV9SirqxoPgG3cDMg80N8)

  
  

More formally, regularization changes the update rule of the algorithm at hand, and captures a variety of methods commonly known as Mirrored-Descent. The zoo of different regularizations raises an obvious question: which one is best? Reality, as always, is complicated: different data properties and different applications will render different algorithms better. This question directly relates to the first question we started the post with: which algorithm is best for the task, in a more limited setting.

  

The machine learning specialist has an equally obvious answer: can we learn the best regularization (or algorithm) on the fly? This is exactly the motivating question that gave rise to Adaptive Regularization! The Adagrad algorithm was the first to formalize this question, and prove that with a changing regularization, it can compete with the best algorithm in hindsight over the data (see [chapter 5.6 here](http://ocobook.cs.princeton.edu/OCObook.pdf)).

  

## Parameter-free optimization: removing the pesky scale term

  

Anyone with practical experience in optimization is aware of the need for hyperparameter tuning. Virtually all algorithms come with tunable parameters, and the practitioner needs to set these correctly to attain optimal behavior. Can we avoid this practice, and come up with completely automated methods?

  

This is a closely related question to the one we started with! Indeed, the relationship is more than superficial: the motivation for AGM is to automate the choice of the preconditioner. This solves part of the tuning problem, but the “scale” term remains, which is closely related to the distance of the initial point from the global optimum.

  

From a theoretical perspective, the goal is to obtain the optimal regret bound for online learning, which online gradient descent / Adagrad obtains depending on the geometry of the problem. However, not knowing the initial distance to optimality introduces a log(distance) term to the regret bound of Theorem 3.1 [in this book](https://arxiv.org/pdf/1909.05207.pdf). Removing this log(diameter) term requires sophisticated machinery and different approaches have been applied, e.g.

1. [coin-betting methods](https://arxiv.org/abs/1602.04128)

2. using the empirical distance in lieu of diameter as per [D-adaptation](https://arxiv.org/abs/2301.07733), [DoG optimizer](https://arxiv.org/abs/2302.12022)

3. Black-box reduction via online balancing as per [Mechanic](https://arxiv.org/pdf/2306.00144.pdf)

4. Adaptive regret in [SAMUEL](https://arxiv.org/pdf/2203.01400.pdf)

  

The Meta Optimization methodology addresses a significantly more general problem via different tools. We turn to describe it next.

  
  

## Online Control for Meta Optimization

  

The relationship between control and optimization spans decades: even the names of optimization algorithms, such as the “heavy ball method” and “momentum”, borrow from the realm of physical dynamical systems.

  

The analysis of mathematical optimization algorithms often makes use of control methodology. The most common application is that of the Lyapunov direct method for analyzing stability of a dynamical system. Lyapunov's direct method involves creating an energy or potential function, also called the ``Lyapunov function". This function needs to be non-increasing along the trajectory of the dynamics, and strictly positive for states other than the equilibrium (global minimum for an optimization problem) to certify the stability of the system. A common example given in introductory courses on dynamics is that of the motion equations of the pendulum.

![](https://lh6.googleusercontent.com/PP9GPrqyjvSvWvKlBLV--IGLy5DdP4UH5NI-Y0vLGO_DeEGTyU8s8XPGqBhIWSIK0IGKJHUohPuV72A8CMyTETYz6_YknY9CJhIPSrHWhK_MgrKzKXLHGL7h93v4nHiwPYu7m8-E-NJ94X6jlH5Gsek)

The Lyapunov function for this system is taken to be the total energy, kinetic and potential. [Tedrake’s book provides an excellent exposition](https://underactuated.csail.mit.edu/).

  
  

The connections between [Lyapunov’s direct method for stability](https://en.wikipedia.org/wiki/Lyapunov_stability) analysis and optimization were further explored by [Lassard, Recht and Packard](https://arxiv.org/abs/1408.3595), and recently in the extensive thesis of [Wilson](https://search.proquest.com/openview/3b93e91616bf45f222b02cbaf3ec5c53/1?pq-origsite=gscholar&cbl=18750).

  

However, the direct method is less suited to our purpose of finding the best algorithm for a task. Most notably, the direct method is useful for analyzing existing methods, and does not come with a recipe for deriving/learning a task-specific algorithm.

  

An alternative to Lyapunov’s direct method is Lyapunov linearization, which approximates a dynamical system with a time-varying linear dynamical system. Linear dynamics are significantly better understood compared to nonlinear dynamical systems, especially after the work of Kalman on state space control and the [Linear Quadratic Regulator](https://en.wikipedia.org/wiki/Linear%E2%80%93quadratic_regulator). However, Lyapunov’s linearization is seldom used in the analysis of optimization methods, possibly due to the limitations of existing control methods for linear systems These methods typically assume the knowledge of the system matrices in advance, and efficient methods are only known for quadratic losses. Moreover, the noise in the system is commonly assumed to be stochastic, which is a restriction on the formulation of the dynamical system from optimization trajectories.

Here comes a new theory for online control that was recently developed in the machine learning literature: [Online Nonstochastic Control](https://arxiv.org/abs/2211.09619) (see also [ICML tutorial](https://sites.google.com/view/nsc-tutorial/home) and code therein). This new methodology can overcome these limitations of control for the design and analysis of optimization algorithms:

1.  The framework is online and does not require a-priori knowledge of the dynamical system
    
2.  Efficient algorithms (such as [GPC](https://proceedings.mlr.press/v97/agarwal19c.html)) exist for any convex costs
    
3.  The framework is regret-based, and allows for nonstochastic noise
    

  

With the use of online nonstochastic control, we can model meta optimization as an iterative control problem and derive new efficient algorithms for learning the best algorithm for a sequence of optimization tasks! Not only that, the use of online nonstochastic control overcomes the challenge of nonconvexity, which exists even for learning the learning rate as we explained before, through the use of convex relaxation.

  

## Formalization of Meta Optimization

The formal setting of meta-optimization is as follows. We are given a sequence of optimization problems, called episodes. The goal of the player is not only to minimize the total cost in each episode, but also to compete with a set of available optimization methods.

  

Specifically, in each of the $N$ episodes, we have a sequence of $T$ optimization steps that are either deterministic, stochastic, or online. At the beginning of an episode, the iterate is ``reset" to a given starting point $x_{1, i}$. In the most general formulation of the problem, at time $(t, i)$, an optimization algorithm $A$ chooses a point $x_{t, i} \in K$, in a convex domain $K \subseteq R^d$. It then suffers a cost $f_{t, i}(x_{t, i})$. Let $x_{t, i}(A)$ denote the point chosen by $A$ at time $(t, i)$, and for a certain episode $i \in [N]$, denote the cost of an optimization algorithm $A$ by

$$ J_i(A) = \sum_{t=1}^T f_{t, i}(x_{t, i}(A) ) - \min_{x^* \in K} \sum_t f_t^i(x^*) . $$

  

The standard goal in optimization, either deterministic, stochastic, or online, is to minimize each $J_i$ in isolation. In meta-optimization, the goal is to minimize the cumulative cost in both each episode, and overall in terms of the choice of the algorithm. We thus define meta-regret to be

$$\text{meta-regret}(A) = \sum_{i=1}^N J_i(A) - \min_{A^* \in \Pi} \sum_{i=1}^N J_i(A^*) ,$$ where $\Pi$ is the benchmark algorithm class. The meta-regret is the regret incurred for learning the best optimization algorithm in hindsight, and captures both efficient per-episode optimization as well as competing with the best algorithm in $\Pi$.

  

In a recent paper, we give efficient methods based on the [GPC](https://proceedings.mlr.press/v97/agarwal19c.html) that guarantee meta-regret that scales as $O(\sqrt{NT})$ for meta optimization of quadratic functions. If the functions are smooth, the method has meta-regret scaling as $O({NT}^{¾})$ in expectation. In certain settings, this captures learning the learning rate for smooth optimization as a special case!

  

We hope this was a fun introduction to a new approach for learning the best algorithm, for more details, [please see the full paper](https://arxiv.org/abs/2301.07902)!
