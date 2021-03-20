---
layout: post
title: Taking control by convex optimization
authors: [elad]
---

The picture to the right depicts Rudolf Kalman, a pioneer of modern control, receiving the presidential medal of freedom from president Barack Obama.

{% assign image = "2018-05-29-kalman.jpeg" %}
{% include center-image.html %}

The setting which Kalman considered, and has been a cornerstone of modern control, is that of stateful time-series. More precisely, consider a sequence of inputs and outputs, or measurements, coming from some real-world machine\
$$x_1,x_2,ldots,x_T,\ldots   \ \ \Rightarrow  \ \ \ y_1,y_2, y_3 , \ldots, y_T , \ldots $$
Examples include:

-   $$y_t$$ are measurements of ocean temperature, in a study of global warming. $$x_t$$ are various environmental knowns, such as time of the year, water acidity, etc.
-   Language translation, $$x_t$$ are words in Hebrew, and $$y_t$$ is their English translation
-   $$x_t$$ are physical controls of a robot, i.e. force in various directions, and $$y_t$$ are the location to which it moves

Such systems are generally called dynamical systems, and one of the simplest and most useful mathematical models to capture a subset of them is called  linear dynamical systems (LDS), in which the output is generated according to the following equations:

$$h_{t+1}  = A h_t + B x_t + \eta_t $$

$$y_{t+1}   = C h_t + D x_t + \zeta_t $$

Here $$h_t$$ is a hidden state, which can have very large or even infinite dimensionality, $$A,B,C,D$$ are linear transformations and $$\eta_t,\zeta_t$$ are noise vectors.

This setting is general enough to capture a variety of machine learning models previously considered in isolation, such as HMM (hidden Markov models), principle and independent component analysis, mixture of Gaussian clusters and many more, see this [survey by Roweis and Ghahramani](https://cs.nyu.edu/~roweis/papers/NC110201.pdf).

Alas -- without any further assumptions the Kalman filtering model is non-convex and computationally hard, thus general polynomial time algorithms for efficient worst-case prediction were not known, till some exciting recent developments I'll survey below.

If the linear transformations $$A,B,C,D$$ are known, then it is possible to efficiently predict $$y_t$$ given all previous inputs and outputs of the system using convex optimization. Indeed, this is what the Kalman filter famously achieves, and in an optimal way. Similarly, if there is no hidden state, the problem becomes trivially convex, and thus easily solvable (see recent blog posts and papers by the Recht group further analyzing this case).

However, if the system given by the transformations A,B,C,D is unknown, recovering them from observations is called "system identification", a notoriously hard problem. Even for HMMs, which can be seen as a special case of LDS (see the [RG](http://mlg.eng.cam.ac.uk/zoubin/papers/lds.pdf) survey), the identification problem is known to be [NP-hard](http://www.math.ru.nl/~terwijn/publications/icgiFinal.pdf) without additional assumptions. (Aside: HMMs are identifiable with further distributional assumption, see the breakthrough paper of[ Hsu, Kakade and Zhang](http://www.cs.columbia.edu/~djhsu/papers/hmm.pdf), which started the recent tensor revolution in theoretical ML).

In the face of NP-hardness, state-of-the-art reduces to a set of heuristics. Amongst them are:

-   By far the most common is the use of EM, or expectation maximization, to alternately solve for the system and the hidden states. Since this is a heuristic for non-convex optimization, global optimality is not guaranteed, and indeed EM can settle on a local optimum, as shown [here](https://arxiv.org/abs/1711.00946).
-   Gradient descent: this wonderful heuristic can be applied for the non-convex problem of finding both the system and hidden states simultaneously. In a striking recent result, [Hardt and Ma](https://arxiv.org/abs/1609.05191) showed that under some generative assumptions, gradient descent converges to the global minimum.

This is where we go back to the convex path: using the failsafe methodology of convex relaxation and regret minimization in games, in a [recent](https://arxiv.org/abs/1711.00946) set of [results](https://arxiv.org/abs/1802.03981) our group has found assumption-free, efficient algorithms for predicting in general LDS, as well as some other control extensions. At the heart of these results is a new method of spectral filtering. This method requires some mathematical exposition, we'll defer it to a future longer post. For the rest of this post, we'll describe the autoregressive (a.k.a. regression) methodology for LDS, which similar to our result, is a worst-case and convex-relaxation based method.

To see how this works, consider the LDS equations above, and notice that for zero-mean noise, the expected output at time $$t+1$$ is given by: (we take $$D=0$$ for simplicity) $$E[y_{t+1} ] =  \sum_{i=1}^t  C A^i B x_{t-i} $$.
This has few parameters to learn, namely only three matrices A,B,C, but has a very visible non-convex component of raising A to high powers.

The obvious convex relaxation takes $$M_i = C A^i B$$ as a set of matrices for $$i=1,...,t$$. We now have a set of linear equalities of the form:

$$y_{t+1}  = \sum_{i=1}^t M_i x_{t-1}$$

which can be solved by your favorite convex linear-regression optimizer. The fallacy is also clear: we have parameters that scale as the number of observations, and thus cannot hope to generalize.

Luckily, many systems are well-behaved in the following way. First, notice that the very definition of an LDS requires the spectral norm of A to be bounded by one, otherwise we have signal explosion -- it's magnitude grows indefinitely with time. It is thus not too unreasonable to assume a strict bound away from one, say $$\|A\| \leq 1 - \delta$$, for some small constant $$ \delta >0 $$. This allows us to bound the magnitude of the i'th matrix $$M_i$$, that is supposed to represent $$C A^i B$$, by $$(1-\delta)^i$$.

With this assumption, we can then take only $$k = O(\frac{1}{\delta} \log \frac{1}{\epsilon})$$ matrices, and write

$$y_{t+1} = \sum_{i=1}^k M_i x_{t-1} + O(\epsilon) $$

This folklore method, called an autoregressive model or simply learning LDS by regression, is very powerful despite its simplicity. It has the usual wonderful merits of online learning by convex relaxation: is worst-case (no generative assumptions), agnostic, and online. Caveats? we have a linear dependence on the eigengap of the system, which can be very large for many interesting systems.

However, it is possible to remove this gap completely, and learn arbitrarily ill-defined LDS without dependence on the condition number. This method is also online, agnostic, and worst case, and is based on a new tool: wave-filtering. In essence it applies the online regression method on a specially-designed fixed filter of the input. To see how these filters are designed, and their theoretical properties, check out our recent [papers](https://arxiv.org/abs/1711.00946)!
