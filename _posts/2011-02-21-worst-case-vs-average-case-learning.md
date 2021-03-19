---
layout: post
title:  "Worst-case vs. average-case learning"
authors: [elad_hazan]
---

Classical statistical learning theory deals with finding a consistent hypothesis given sufficiently many examples. Such a hypothesis may be a rule for classifying emails into spam/not-spam, and examples are classified emails.

Statistical and computational learning theories tell us how many examples are needed to be able to generate a good hypothesis -- one that can correctly classify instances that it had not seen, given that they are generated from the same distribution from which we have seen classified examples.

This spam problem precisely demonstrates the caveat of making statistical assumptions -- clearly the spammers are adaptive and adversarial. The characteristics of spam emails change over time, adapting to the filters.

Here comes online learning theory: in online learning we do not make any assumptions about the data, but rather sequentially modify our hypothesis such that our average performance approaches that of the best hypothesis in hindsight.  The difference between this average performance and the best-in-hindsight performance is called  *regret*, and the foundation of online learning are algorithms whose regret is bounded by a sublinear function of the number of iterations (hence the average regret approaches zero).

Can we interpolate between the two approaches ? That is, can we design algorithms which have a good regret-guarantee if the data is adversarial, but perform much better if there exists benign and simple distribution governing nature.

This natural question was raised several times in the last few years, with some partial progress and many interesting open questions, one of which is made explicit with all required background [here](http://ie.technion.ac.il/~ehazan/papers/openvar.pdf) (submitted to [COLT 2011 open problems session](http://colt2011.sztaki.hu/cfop.html)).
