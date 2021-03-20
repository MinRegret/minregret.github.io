---
title: Blackwell approachability meets Online Conve Optimization
---

David Blackwell was still roaming the corridors of UC Berkeley's stat department during my postdoc years, circa 2009. Jake Abernethy, Sasha Rakhlin, Peter Bartlett and myself were discussing his results, and his seminal contributions to prediction theory were already well known.

![](/assets/img/2020-10-06-blackwell.jpeg)
David Blackwell

![](/assets/img/2020-10-06-hannan.png)
James Hannan

At that time, still the early days of online convex optimization, we were contemplating everything from adaptive gradient methods to bandit convex optimization. Blackwell's famed approachability theorem was looming in the background, considered to be one of the strongest theorems in the ML-theorists toolkit.

I've recently added a new draft chapter to to V2.0 of [Introduction to Online Convex Optimization](http://ocobook.cs.princeton.edu/), about the connection between OCO and Blackwell approachability: they are algorithmically equivalent! More precisely, an efficient algorithm for approachability gives rise to an efficient algorithm for OCO with sublinear regret, and vice versa.

Details are in the chapter draft, and I recommend this music for reading it: (the song is called "together we won despite everything", dedicated to music and science)
