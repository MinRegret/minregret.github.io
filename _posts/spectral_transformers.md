#Spectral Transformers

by Hazan lab 


One of the biggest challenges for the Transformer architecture, powering modern large language models, is their computational inefficiencies on long sequences. The computational complexity of inference of the attention module scales quadratically with the context length, which is therefore limited in practice.  

The computational bottleneck of transformers gave rise to recent interest in state space models. These alternate architectures are variants of recurrent neural networks that are much faster in terms of inference. Recent works showed their promise in a variety of tasks requiring long context, such as the long range arena benchmark. 

In this post we describe a recent methodological advancement for state space models: spectral filtering. We describe the theoretical foundations of this technique, and how it gives rises to provable methods with long memory for learning linear dynamical systems. We then describe how the spectral filtering algorithm can be used for designing neural architectures and preliminary results in long range tasks.   

##Fundamentals of Sequence Prediction 

Stateful time series prediction have been used to model a plethora of phenomena. Consider a sequence of inputs and outputs, or measurements, coming from some real-world machine \

$$x_1,x_2, \ldots,x_T,\ldots   \ \ \Rightarrow  \ \ \ y_1,y_2, y_3 , \ldots, y_T , \ldots $$

For example, these can be:

-   $y_t$ are measurements of ocean temperature, in a study of global warming. $x_t$ are various environmental knowns, such as time of the year, water acidity, etc.


-   Language modeling or translation, $x_t$ are words in Hebrew, and $y_t$ is their English translation


-   $x_t$ are physical controls of a robot, i.e. force in various directions, and $y_t$ are the location to which it moves


Such systems are generally called dynamical systems, and the simplest type of dynamics is linear dynamics. A linear dynamical system has a particularly intuitive interpretation as a (configurable) vector field (from wikipedia):

A linear dynamical system (LDS) posits the state of a system evolves via the following dynamical relation:


(video by @robertghrist)
Here  represents the state of the system,  represents a control input and  is a perturbation introduced to the dynamics, for the time step t. The vector fields above illustrate the behavior of the system for a few different choices of A, when the control input  is set to zero. The control inputs, when correctly chosen, can modify the dynamics to induce a particular desired behavior. For example, controlling the thermostat in a data center to achieve a particular temperature, applying a force to a pendulum to keep it upright, or driving a drone to a destination.




Geometric Decay in LDS 

The linear equations governing the dynamics are recursive in nature, and imply that in a noiseless environment, the $t$'th output can be written as
$$     y_{t} = C x_t + D u_t &= C (A x_{t-1} +B u_{t}) + D u_t = ... = \sum_{i=0}^{t-1} C A^i  B u_{t-i} + D u_t $$
The matrix $A$ is asymmetric in general, and can have complex eigenvalues. If the amplitude of these eigenvalues is $>1$, then the output $y_t$ can grow without bounds. This is called an ``explosive" system. In a well-behaved system, the eigenvalues of $A$ have magnitude $<1$. If the magnitudes are bounded away from $1$, say $|\lambda_i (A)| < 1- \delta$, for some $\delta > 0$ (referred to as spectral gap), then we can write
$$ y_{t} = \sum_{i=0}^k C A^i  B u_{t-i} +  \omega_k \ \ , \ \   \| \omega_k \| \leq \eps $$ 
for $k = O(\frac{1}{\delta}\log \frac{1}{\eps}) $. This mathematical fact implies that the \textbf{effective memory} of the system is on the order of $\frac{1}{\delta}$. In general, the parameter $\delta$ is unknown apriori and can get arbitrarily small as we approach systems with have long range dependencies leading to instability in training linear dynamical systems with a long context. This issue is specifically highlighted in the work of \cite{orvieto2023resurrecting} who observe that on long range tasks learning an LDS directly does not succeed and requires interventions such as stable exponential parameterizations and specific normalization which have been repeatedly used either implicitly or explicitly in the SSM literature \cite{gu2021efficiently}. Unfortunately these reparametrizations and normalizations come with no theoretical guarantees. In fact this limitation is generally known to be fundamental to the use of linear dynamical systems, and can only be circumvented via a significant increase in sample complexity \cite{ghai2020no} or via control over the input sequence \cite{simchowitz18a}. 

Spectral Filtering 

A notable deviation from the standard theory of linear dynamical systems that allows efficient learning in the presence of arbitrarily long memory is the technique of spectral filtering \cite{hazan2017learning}. The idea is to project the sequence of inputs to a small subspace that is constructed using special structure of discrete LDS where successive powers of the system matrix appear in the impulse response function. The basic idea is to represent the output as 
$$ {y}_{t} = \sum_{j=1}^k M_{j} \left( \sum_{i} \phi_j(i) \cdot {u}_{t-i} \right) , $$ 
where $\phi_j$ are \textit{spectral filters} which are sequence-length sized vectors that given the target sequence length can be computed offline, and $M_j$ are matrices parameterizing the model. These spectral-filters are the eigenvectors of the matrix constructed as the average of outer products of the discrete impulse-response functions, viz $Z = \int_{0}^1[1, \alpha, \alpha^2 ...][1, \alpha, \alpha^2 ...]^{\top} d\alpha$. It is shown that this matrix is inherently low-dimensional and for all $\alpha \in [0, 1]$, vectors of the form $[1 , \alpha, \alpha^2 \ldots ]$ are well approximated by the top-eigenspace of Z. Figure \ref{fig:filterbank} depicts these filters. For the details of how these filters are derived and their computation, see Section \ref{sec:prelims}.  


\paragraph{Why is spectral filtering important?}
The main advantage of spectral filtering is that for certain types of linear dynamical systems, in particular those with symmetric matrices $A$, the \textit{effective memory}(measured by the number of filters) required to represent an observation at any point in the sequence in the spectral basis is \textbf{independent of the spectral gap parameter $\delta$!}. This guarantee indicates that if we featurize the input into the spectral basis, we can potentially design models that are capable of efficiently and stably representing systems with extremely long memory even with $\delta \rightarrow 0$. This striking fact motivates our derivation of the recurrent spectral architecture, and is the underlying justification for the performance and training stability gains we see in experiments. 







The setting which Kalman considered, and has been a cornerstone of modern control, is that of stateful time-series. More precisely, consider a sequence of inputs and outputs, or measurements, coming from some real-world machine\
$$x_1,x_2,ldots,x_T,\ldots   \ \ \Rightarrow  \ \ \ y_1,y_2, y_3 , \ldots, y_T , \ldots $$
Examples include:

-   $$y_t$$ are measurements of ocean temperature, in a study of global warming. $$x_t$$ are various environmental knowns, such as time of the year, water acidity, etc.
-   Language translation, $$x_t$$ are words in Hebrew, and $$y_t$$ is their English translation
-   $$x_t$$ are physical controls of a robot, i.e. force in various directions, and $$y_t$$ are the location to which it moves

Such systems are generally called dynamical systems, and one of the simplest and most useful mathematical models to capture a subset of them is called  linear dynamical systems (LDS), in which the output is generated according to the following equations:

$$h_{t+1}  = A h_t + B x_t + \eta_t $$

$$y_{t+1}   = C h_t + D x_t + \zeta_t $$

Here $$h_t$$ is a hidden state, which can have very large or even infinite dimensionality, $$A,B,C,D$$ are linear transformations and $$\eta_t,\zeta_t$$ are noise vectors.

This setting is general enough to capture a variety of machine learning models previously considered in isolation, such as HMM (hidden Markov models), principle and independent component analysis, mixture of Gaussian clusters and many more, see this [survey by Roweis and Ghahramani](https://cs.nyu.edu/~roweis/papers/NC110201.pdf).

Alas -- without any further assumptions the Kalman filtering model is non-convex and computationally hard, thus general polynomial time algorithms for efficient worst-case prediction were not known, till some exciting recent developments I'll survey below.

If the linear transformations $$A,B,C,D$$ are known, then it is possible to efficiently predict $$y_t$$ given all previous inputs and outputs of the system using convex optimization. Indeed, this is what the Kalman filter famously achieves, and in an optimal way. Similarly, if there is no hidden state, the problem becomes trivially convex, and thus easily solvable (see recent blog posts and papers by the Recht group further analyzing this case).

However, if the system given by the transformations A,B,C,D is unknown, recovering them from observations is called "system identification", a notoriously hard problem. Even for HMMs, which can be seen as a special case of LDS (see the [RG](http://mlg.eng.cam.ac.uk/zoubin/papers/lds.pdf) survey), the identification problem is known to be [NP-hard](http://www.math.ru.nl/~terwijn/publications/icgiFinal.pdf) without additional assumptions. (Aside: HMMs are identifiable with further distributional assumption, see the breakthrough paper of[ Hsu, Kakade and Zhang](http://www.cs.columbia.edu/~djhsu/papers/hmm.pdf), which started the recent tensor revolution in theoretical ML).

In the face of NP-hardness, state-of-the-art reduces to a set of heuristics. Amongst them are:

-   By far the most common is the use of EM, or expectation maximization, to alternately solve for the system and the hidden states. Since this is a heuristic for non-convex optimization, global optimality is not guaranteed, and indeed EM can settle on a local optimum, as shown [here](https://arxiv.org/abs/1711.00946).
-   Gradient descent: this wonderful heuristic can be applied for the non-convex problem of finding both the system and hidden states simultaneously. In a striking recent result, [Hardt and Ma](https://arxiv.org/abs/1609.05191) showed that under some generative assumptions, gradient descent converges to the global minimum.

This is where we go back to the convex path: using the failsafe methodology of convex relaxation and regret minimization in games, in a [recent](https://arxiv.org/abs/1711.00946) set of [results](https://arxiv.org/abs/1802.03981) our group has found assumption-free, efficient algorithms for predicting in general LDS, as well as some other control extensions. At the heart of these results is a new method of spectral filtering. This method requires some mathematical exposition, we'll defer it to a future longer post. For the rest of this post, we'll describe the autoregressive (a.k.a. regression) methodology for LDS, which similar to our result, is a worst-case and convex-relaxation based method.

To see how this works, consider the LDS equations above, and notice that for zero-mean noise, the expected output at time $$t+1$$ is given by: (we take $$D=0$$ for simplicity) $$E[y_{t+1} ] =  \sum_{i=1}^t  C A^i B x_{t-i} $$.
This has few parameters to learn, namely only three matrices A,B,C, but has a very visible non-convex component of raising A to high powers.

The obvious convex relaxation takes $$M_i = C A^i B$$ as a set of matrices for $$i=1,...,t$$. We now have a set of linear equalities of the form:

$$y_{t+1}  = \sum_{i=1}^t M_i x_{t-1}$$

which can be solved by your favorite convex linear-regression optimizer. The fallacy is also clear: we have parameters that scale as the number of observations, and thus cannot hope to generalize.

Luckily, many systems are well-behaved in the following way. First, notice that the very definition of an LDS requires the spectral norm of A to be bounded by one, otherwise we have signal explosion -- it's magnitude grows indefinitely with time. It is thus not too unreasonable to assume a strict bound away from one, say $$\|A\| \leq 1 - \delta$$, for some small constant $$ \delta >0 $$. This allows us to bound the magnitude of the i'th matrix $$M_i$$, that is supposed to represent $$C A^i B$$, by $$(1-\delta)^i$$.

With this assumption, we can then take only $$k = O(\frac{1}{\delta} \log \frac{1}{\epsilon})$$ matrices, and write

$$y_{t+1} = \sum_{i=1}^k M_i x_{t-1} + O(\epsilon) $$

This folklore method, called an autoregressive model or simply learning LDS by regression, is very powerful despite its simplicity. It has the usual wonderful merits of online learning by convex relaxation: is worst-case (no generative assumptions), agnostic, and online. Caveats? we have a linear dependence on the eigengap of the system, which can be very large for many interesting systems.

However, it is possible to remove this gap completely, and learn arbitrarily ill-defined LDS without dependence on the condition number. This method is also online, agnostic, and worst case, and is based on a new tool: wave-filtering. In essence it applies the online regression method on a specially-designed fixed filter of the input. To see how these filters are designed, and their theoretical properties, check out our recent [papers](https://arxiv.org/abs/1711.00946)!








