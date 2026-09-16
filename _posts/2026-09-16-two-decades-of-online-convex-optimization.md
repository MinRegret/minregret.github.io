---
title: "Two decades of online convex optimization: a personal recollection"
authors: [elad]
permalink: /2026/09/15/two-decades-of-online-convex-optimization.html
---

<small> _(note: I’m inevitably leaving out many wonderful collaborators and stories, forgive me! more details at the end. -EH)_ </small>

I began working on online convex optimization as a third-year graduate student. At that time, [Zinkevich’s paper](https://www.cs.cmu.edu/~maz/publications/techconvex.pdf) came out, and we were reading [Cover’s paper on universal portfolios](https://isl.stanford.edu/~cover/papers/paper93.pdf) with fellow students (more about my friendship w. [Satyen Kale](https://www.satyenkale.com/) later).

My goal, at the time, was to hedge against not finding an academic job. You see, I entered graduate school to study computational complexity. At that time, I was regularly hanging out with mathematical prodigies like [Ryan O’Donnell](https://www.cs.cmu.edu/~odonnell/), [Irit Dinur](https://www.wisdom.weizmann.ac.il/~dinuri/), [Scott Aaronson](https://scottaaronson.com/), [Dana Moshkovitz](https://www.cs.utexas.edu/~danama/), [Robert Krauthgamer](https://www.wisdom.weizmann.ac.il/~robi/), [Muli Safra](https://sites.google.com/site/mulisafra/home), and (of course) my advisor, [Sanjeev Arora](https://profsanjeevarora.github.io/). It was an intimidating environment. STOC/FOCS were as rigorous then as they are today, possibly more. The main criterion was mathematical prowess. It is particularly interesting to me these days, that AI is better at exactly what FOCS/STOC favors, and less so at inventing new frameworks… I’ll come back to this at the end. My fear was that competing with these geniuses for a theory job was hopeless.

This is amusing to me in retrospect. They are all close friends today. I can have Scott and Dana over for dinner, coffee with [Noga Alon](https://web.math.princeton.edu/~nalon/) the following week, and chat with [Avi Wigderson](https://www.math.ias.edu/avi/home) about my younger son Oded. As a graduate student, I could not have imagined being half as close to these people as I eventually became.

So, leaving all my modesty on the floor, it was totally my idea to start a student group to become experts in finance, so we could get a job in that industry if our academic prospects failed…

We took a finance course at the Bendheim Center (I believe Satyen is the only one to take it to completion…), and at the same time studied Cover’s portfolio theory. Our immediate goal was to improve it to be an efficient algorithm, with as good regret bounds as the optimal bounds Cover got. To make a long story short, we discovered a beautiful connection to Newton’s method, regret minimization, and online convex optimization, in what became one of my favorite papers of all time that introduced the [Online Newton Step algorithm](https://www.satyenkale.com/papers/log-regret.pdf). I felt at the time it was an important result, despite being rejected from FOCS/STOC, and felt there was more to it than met the eye. In hindsight, the algorithm was the smaller part. The bigger part was realizing that “efficiently compete with the best fixed decision in hindsight using whatever method” was a single lens through which portfolio selection, gradient descent, and Newton’s method became one.

A technical note: Cover’s paper was about an investment strategy called “universal portfolios”, one that has a guarantee compared to the optimal fixed, rebalanced portfolio over stocks **in hindsight, without assuming anything about the market.** Zinkevich’s paper studied a similar quantity, borrowed from game theory: regret. Regret measures how far away we are, in terms of loss, from the best fixed decision in hindsight. His paper showed that a natural version of gradient descent obtains near-optimal regret bounds. Our idea was as follows: what if Newton’s method could give better regret bounds than gradient descent? What if that could give an efficient portfolio selection algorithm?

What struck me the most was the connection between mathematical optimization and learning, which at that time, seemed totally unexplored. I remember asking an expert in optimization at ORFE at the time (name withheld) a very basic question: “What is the worst-case computational complexity of constrained convex optimization?” I could not get a clear answer.

So I turned to the [seminal book of Nesterov and Nemirovski](https://epubs.siam.org/doi/book/10.1137/1.9781611970791). Both [Yuri Nesterov](https://sds.cuhk.edu.cn/en/node/1634) and [Arkadi Nemirovski](https://www2.isye.gatech.edu/~nemirovs/) later became my scientific heroes. Arkadi I was fortunate to interact with in person—one of the greatest scientists I have ever known. But I have to admit: that book was nearly unreadable.

That, from the perspective of a theory student, was the strange state of optimization at the time. It was an extraordinarily deep and mature field, but it did not yet have the clean algorithmic language that would soon connect optimization, learning, and sequential decision-making. That connection became [online convex optimization](https://arxiv.org/abs/1909.05207).

## From ONS to Adaptive Gradient Methods

Perhaps the largest impact of the field is the development of [adaptive gradient methods](https://jmlr.org/papers/v12/duchi11a.html), the workhorse of modern deep learning and AI, starting with the [AdaGrad algorithm](https://jmlr.org/papers/v12/duchi11a.html). The story behind them is fun, as I’ve recently described at two 60th birthday celebrations of colleagues: [Yoram Singer](https://yoram-singer.github.io/) (my co-inventor with [John Duchi](https://web.stanford.edu/~jduchi/)) and [Peter Bartlett](https://www.stat.berkeley.edu/~bartlett/).

After grad school, I went to do a postdoc in the famed “theory group” of IBM Almaden, hosted by the excellent mathematician [Nimrod Megiddo](https://theory.stanford.edu/~megiddo/bio.html). From the very start, my goal was to be a professor in my home country of Israel. But I had no Israeli connections and an Indian-American advisor… 

So, motivated by networking with senior Israeli professors, I went to seek out the great optimizer Yoram Singer. It was easy - Yoram knew me from our [2006 ONS paper](https://www.satyenkale.com/papers/log-regret.pdf), which he was the first to appreciate and understand (and later used ideas from to create [Pegasos](https://home.ttic.edu/~shai/papers/ShalevSiSr07.pdf), with my friends [Shai Shalev-Shwartz](https://www.cs.huji.ac.il/~shais/) and [Nati Srebro](https://nati.ttic.edu/)).

Yoram, to his credit, was as open in research as you can be. He welcomed me to his office at Google MTV with open arms, and together with John Duchi, back then a student from Berkeley who biked back and forth about an hour every day from Berkeley to the Mountain View campus of Google, we set out to improve optimization. I LOVED the MTV campus: free food and amazing nerdy vibe, an ideal environment for research.

The key idea was: how can we compete with the best regularization in hindsight?!

This basically applies regret to the optimizer family itself: the same lens that had unified the learners, now pointed one level up, at the optimizer. It is an idea which by now is commonplace in optimization, but was brand new at the time.

So Yoram was motivated by optimization, improving the practice of machine learning. John was enamored by the matrix mathematics (which is indeed beautiful :-), and I was seeking an academic position in Israel… This trio was successful, and adaptive gradient methods were born!

## Adaptation, Computation, and Friendship

The postdoc years up to my first faculty job were a golden age for online convex optimization. Satyen and I were on fire; we functioned like a well-oiled research machine. Any topic we looked at was somehow overlooked from the point of view of regret, or optimization, or both. The question was always the same: what does this problem look like if you assume nothing and just ask for no regret? Time of our lives. In a short amount of time, we wrote about 20 papers together, spanning:

1. [Projection-free methods](https://arxiv.org/abs/1206.4657)
2. [Variational bounds in regret](https://link.springer.com/article/10.1007/s10994-010-5175-x)
3. [Bandit algorithms](https://jmlr.org/papers/v12/hazan11a.html)
4. [Game theory, equilibrium, and fixed points](https://proceedings.neurips.cc/paper/2007/hash/e4bb4c5173c2ce17fd8fcd40041c068f-Abstract.html)
5. [Optimal stochastic strongly-convex optimization](https://jmlr.org/papers/v15/hazan14a.html)
6. [Online submodular minimization](https://jmlr.org/papers/v13/hazan12a.html)
7. [Online matrix prediction](https://arxiv.org/abs/1204.0136), with Shai Shalev-Shwartz
8. [Multiplicative weights and its applications](https://theoryofcomputing.org/articles/v008a006/), with our advisor, Sanjeev Arora

All of this was accompanied by an amazing sense of camaraderie. We didn’t need to complete each other's sentences; it was like we were on the same frequency. We even liked the same food and hangouts.

<div class="oco-photo-pair">
  <figure class="oco-photo">
    <a href="/assets/img/2026-09-15-oco-collaborators-whiteboard.png"><img src="/assets/img/2026-09-15-oco-collaborators-whiteboard.jpg" alt="Two collaborators standing in front of a whiteboard covered with equations" width="1134" height="812" loading="lazy"></a>
    <figcaption>Satyen and me at the whiteboard, during grad school.</figcaption>
  </figure>
  <figure class="oco-photo">
    <a href="/assets/img/2026-09-15-oco-collaborators-lounge.png"><img src="/assets/img/2026-09-15-oco-collaborators-lounge.jpg" alt="Two collaborators together in a university lounge" width="920" height="650" loading="lazy"></a>
    <figcaption>Satyen and me during grad school.</figcaption>
  </figure>
</div>

I recall a particular NeurIPS, perhaps 2009, which was held in Vancouver, Canada. I needed to extend my visa, and was basically denied, or told to expect a few months of processing, during which I had to remain outside the US. I explained at the consulate that I have a baby at home in California. To no avail - I was stuck, and had no clue what to do.

A friend in need is a friend indeed: Satyen stayed with me in Vancouver, rented a hotel room next to mine (or stayed with me, I don’t remember), and we worked and hung out till I figured out what to do (it ended up being a trip to Patagonia… :-). During that time we wrote three new papers together!

## Young faculty days

The dream came true: I got a faculty position in Israel, at the Technion (which is a top tier school), in the faculty of industrial engineering (which was not my first choice). Not only that, I met the great Arkadi Nemirovski in his final days as faculty there. Could not be more perfect.

But actually it could. No one prepared me for the sheer joy of advising grad students. A relationship like no other - whatever you put in, you get 10x back. I advised four graduate students, three of whom became amazing professors: [Tomer Koren](https://tomerkoren.github.io/), [Dan Garber](https://dangar.net.technion.ac.il/) and [Kfir Levy](https://kfiryehud.wixsite.com/kfir-y-levy). OCO was progressing at that time, with results from all over the world, and also from my small piece of heaven. My friends visited, including Jake Abernethy, [Manfred Warmuth](https://mwarmuth.bitbucket.io/), [Sham Kakade](https://shamulent.github.io/), [Alex Madry](https://madry.mit.edu/), Satyen of course, and many more. Some of my favorite results from that time:

1. [Playing non-linear games with linear oracles](https://arxiv.org/abs/1301.4666), with Dan Garber
2. [The equivalence of Blackwell approachability and no-regret learning](https://proceedings.mlr.press/v19/abernethy11b.html), with Jake Abernethy and Peter Bartlett
3. [Beating SGD: learning SVMs in sublinear time](https://papers.neurips.cc/paper_files/paper/2011/hash/5f2c22cb4a5380af7ca75622a6426917-Abstract.html), with Tomer Koren and Nati Srebro
4. [Tight bounds for stochastic and online logistic regression](https://arxiv.org/abs/1405.3843), with Tomer Koren and Kfir Levy

<div class="oco-photo-pair oco-photo-pair-technion">
  <figure class="oco-photo">
    <a href="/assets/img/2026-09-15-oco-technion-office.png"><img src="/assets/img/2026-09-15-oco-technion-office.jpg" alt="Two collaborators embracing in an office" width="2048" height="1536" loading="lazy"></a>
    <figcaption>Jake Abernethy and me in my Technion office.</figcaption>
  </figure>
  <figure class="oco-photo">
    <a href="/assets/img/2026-09-15-oco-technion-friends.png"><img class="oco-photo-night" src="/assets/img/2026-09-15-oco-technion-friends.jpg" alt="Four friends standing together outside at night" width="1473" height="1970" loading="lazy"></a>
    <figcaption>With my students Tomer Koren, Kfir Levy and <a href="https://www.linkedin.com/in/oren-anava-ba97954b/">Oren Anava</a> during the Technion years, outside Alabama, a smoked-meat restaurant. Dan Garber is missing—he’s vegetarian :-)</figcaption>
  </figure>
</div>

## Dynamical systems, control, and spectral transformers

With the rise of deep learning, adaptive gradient methods were recognized as important in the revolution. I got an offer from Stanford and Princeton, and chose to return to my alma mater. After starting as a faculty member at Princeton and spending a few more years on optimization, my interest in OCO was fading. The root cause was the rise of ever more sophisticated AI. Back then I already talked to Scott Aaronson about the alignment problem (which he can attest to, Scott?!).

The actual trigger was a talk by [Tengyu Ma](https://ai.stanford.edu/~tengyuma/), a former Sanjeev student at Princeton, on his work with [Recht](https://people.eecs.berkeley.edu/~brecht/) and [Moritz Hardt](https://mrtz.org/). The talk was about learning linear dynamical systems in a statistical setting. I get an allergy when I hear about statistical models… :-) So I told my students [Cyril](https://cyrilzhang.com/) and [Karan](https://i-am-karan-singh.github.io/), there must be another way, let's give it the regret treatment…

My brilliant kids invented a new technique that carried us much more than anticipated, [spectral filtering](https://arxiv.org/abs/1711.00946). The underlying techniques are very much OCO’ish, from improper learning to fast online optimization and regret minimization.  Rather than identify the hidden dynamical system itself, we could compete with it using a different, larger class of predictors. This was the same move for the N'th time, now aimed at dynamical systems: improper learning via regret was the framework, and spectral filtering was its first instance. We convolved the history with a small collection of fixed filters derived from a Hankel matrix, and learned how to combine them. The prediction problem became convex in the new parameters! The first result was for symmetric systems; but later extended dramatically, most recently with my postdoc [Annie Marsden](https://acmarsden.github.io/) (who is a student of John Duchi!) to [universal sequence preconditioning](https://arxiv.org/abs/2502.06545).

Control added another complication: an action changes not only the current loss, but also the future state. In [nonstochastic control](https://proceedings.mlr.press/v117/hazan20a.html), we compare against what another controller would have achieved under the same disturbances, along its own trajectory. Again, the [right controller parametrization](https://arxiv.org/abs/1902.08721) allowed us to use online convex optimization inside a dynamical problem. Karan and I eventually wrote [a book about this](https://arxiv.org/abs/2211.09619). So perhaps I had not really left OCO after all…

And then came a twist: these ideas brought us back to deep learning. With [Naman Agarwal](https://naman33k.github.io/), [Daniel Suo](https://www.danielsuo.com/), and [Xinyi Chen](https://xinyi.github.io/), we used spectral filtering to build [spectral state space models](https://arxiv.org/abs/2312.06837), and later [Flash STU](https://arxiv.org/abs/2409.10489). A representation developed for a regret theorem had become part of a neural architecture. Not quite what we had in mind when we started reading Cover :-)

<div class="oco-photo-pair">
  <figure class="oco-photo">
    <a href="/assets/img/2026-09-15-oco-group-office.png"><img src="/assets/img/2026-09-15-oco-group-office.jpg" alt="Research group gathered in an office" width="900" height="675" loading="lazy"></a>
    <figcaption>My early lab at Princeton. From left to right: Xinyi, Karan, <a href="https://bbullins.github.io/">Brian</a>, me and Naman.</figcaption>
  </figure>
  <figure class="oco-photo">
    <a href="/assets/img/2026-09-15-oco-group-dinner.png"><img src="/assets/img/2026-09-15-oco-group-dinner.jpg" alt="Research group gathered around a dinner table" width="2048" height="1163" loading="lazy"></a>
    <figcaption>Dinner with my Princeton students. Around the table: Cyril, me, <a href="https://leozoroaster.github.io/">Zhou</a>, <a href="https://www.udayaghai.com/">Udaya</a>, <a href="https://nbrukhim.com/">Nataly</a>, <a href="https://wenhanlunaxia.github.io/">Wenhan</a>, Naman, <a href="https://jysun105.github.io/">Jennifer</a> and Xinyi.</figcaption>
  </figure>
</div>

## A final word

Looking back, I don’t think it’s a coincidence that it all started due to my fear of not getting an academic job. It moved me on the path from theorem proving prowess (which was a competitive field) to framework building. In the age of AI, I would make the choice deliberately. As AI gets better at proving theorems, choosing interesting questions and building new frameworks becomes even more important. For me, that was always the more valuable part.

I’m very very happy with the science of OCO. It exceeded my expectations in all respects, mathematical elegance and practical relevance. But undoubtedly, my main achievements are the relationships built along that road, with students and collaborators. I have zero regret :-)

<small> _My apologies for leaving out many collaborations and interactions. In particular, my work with [Jake Abernethy](https://jakeabernethy.github.io/) and [Sasha Rakhlin](https://www.mit.edu/~rakhlin/) on bandit optimization deserves a story of its own, as do my interactions w. Adam Kalai, Sham Kakade, Shay Moran, Paula Gradu, Xinyi Chen, Jennifer Sun, and many others._ </small>


