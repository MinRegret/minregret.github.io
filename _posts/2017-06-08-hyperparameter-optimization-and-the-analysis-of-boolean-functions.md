---
layout: post
title: "Hyperparameter optimization and the analysis of boolean functions"
authors: [elad]
---

I've always admired the beautiful theory on the analysis of boolean functions (see the excellent [book](http://dl.acm.org/citation.cfm?id=2683783) of Ryan O'Donnell, as well [Gil Kalai's lectures](http://www.ma.huji.ac.il/~kalai/)). Heck, it used to be my main area of investigation back in the early grad-school days we were studying hardness of approximation, the PCP theorem, and the "new" (back at the time) technology of Fourier analysis for boolean functions.  This technology also gave rise to seminal results on learnability with respect to the uniform distribution. Uniform distribution learning has been widely criticized as unrealistic, and the focus of the theoretical machine learning community has shifted to (mostly) convex, real-valued, agnostic learning in recent years.

It is thus particularly exciting to me that some of the amazing work on boolean learning can be used for the very practical problem of Hyperparameter Optimization (HO), which has on the face of it nothing to do with the uniform distribution. [Here is the draft](https://arxiv.org/abs/1706.00764), joint work with [Adam Klivans](https://www.cs.utexas.edu/~klivans/) and [Yang Yuan](http://www.callowbird.com/).

To describe hyperparameter optimization: many software packages, in particular with the rise of deep learning, come with gazillions of input parameters. An example is the TensorFlow software package for training deep nets. To actually use it the user needs to specify how many layers, which layers are convolutional / full connected, which optimization algorithm to use (stochastic gradient descent, AdaGrad, etc.), whether to add momentum to the optimization or not.... You get the picture -- choosing the parameters is by itself an optimization problem!

It is a highly non-convex optimization problem, over mostly discrete (but some continuous) choices. Evaluating the function, i.e. training a deep net over a large dataset with a specific configuration, is very expensive, and you cannot assume any other information about the function such as gradients (that are not even defined for discrete functions).  In other words, sample complexity is of the essence, whereas computation complexity can be relaxed as long as no function evaluations are required.

The automatic choice of hyperparameters has been hyped recently with various names such as "auto tuning", "auto ML",  and so forth. For an excellent post on existing approaches and their downsides see these posts [Ben Recht's blog](http://www.argmin.net/2016/06/20/hypertuning/).

This is where harmonic analysis and compressed sensing can be of help! While in general hyperparameter optimization is computationally hard, we assume a sparse Fourier representation of the objective function. Under this assumption, one can use compressed sensing techniques to recover and optimize the underlying function with low sample complexity.

Surprisingly, using sparse recovery techniques one can even improve the known sample complexity results for well-studied problems such as learning decision trees under the uniform distribution, improving upon classical results by [Linial, Mansour and Nisan](http://dl.acm.org/citation.cfm?id=174138).

Experiments show that the sparsity assumptions in the Fourier domain are justified for certain hyperparameter optimization settings, in particular, when training of deep nets for vision tasks. The harmonic approach (we call the algorithm "Harmonica") attains a better solution than existing approaches based on multi-armed bandits and Bayesian optimization, and perhaps more importantly, significantly faster. It also beats random search 5X (i.e. random sampling with 5 times as many samples allowed as for our own method, a smart benchmark proposed by [Jamieson](https://people.eecs.berkeley.edu/~kjamieson/hyperband.html)).

Those of you interested in code, my collaborator [Yang Yuan](http://www.callowbird.com/) has promised to release it on GitHub, so please go ahead and email him 😉

PS. We're grateful to Sanjeev Arora for helpful discussions on this topic.

PPS. It has been a long time since my last post, and I still owe the readers an exposition on the data compression approach to unsupervised learning.  In the mean time, you may want to read this [paper with Tengyu Ma](https://arxiv.org/abs/1610.01132) in NIPS 2016.
