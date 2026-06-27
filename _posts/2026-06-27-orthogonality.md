---
title: "The Statistical Orthogonality Thesis"
authors: [elad, "Helen Qu"]
layout: post
---

The orthogonality thesis holds that intelligence and goals are independent: an agent could be arbitrarily intelligent while pursuing almost any objective. As a possibility this is hard to dispute. But perhaps a more useful question is not about what is possible, but what is most probable. How orthogonal are intelligence and goals in the kinds of agents that actually arise?

Bostrom's orthogonality thesis states that intelligence and final goals are, in principle, independent: "more or less any level of intelligence could be combined with more or less any final goal" (Bostrom, 2012). This supports a common alignment concern: high capability alone gives no guarantee of human-compatible objectives. Related worries appear throughout the AI alignment literature, including Yudkowsky's discussions of civilizational inadequacy and the difficulty of expecting existing processes to reliably solve alignment by default (Yudkowsky, 2017). But this argument is about logical possibility, not probability. It does not specify the distribution over goals induced by the actual processes that generate intelligent agents: evolution or machine-learning training procedures.

A useful analogy comes from statistical physics. The microscopic laws of mechanics do not strictly forbid a pot of water placed on a hot stove from cooling rather than heating. Such a trajectory is physically possible. But it occupies such a tiny fraction of the relevant state space that we never expect to observe it. Even if every scientist who ever lived repeatedly measured the temperature of water on a stove, the water would heat rather than cool. The second law of thermodynamics is therefore not a logical prohibition on entropy-decreasing events; it is a statistical rule that is overwhelmingly true. The lesson is that nonzero probability is qualitatively different from substantial probability. What matters is not what can theoretically happen, but what is likely.

The relationship between intelligence and goals may be similar. Orthogonality may be true as a statement about what kinds of minds are possible, while misleading as a statement about what evolution and training processes are likely to produce. Call this the statistical orthogonality thesis: intelligence and values are separable in principle, but correlated in practice.

The multi-agent perspective is crucial to this argument. The canonical thought experiment imagines a single superintelligent agent in isolation, optimizing against a fixed environment. In that picture nothing pushes goals toward any particular region, let alone that which correlates with human goals, and orthogonality looks natural. But a multi-agent setting is different: a capable agent is situated among other agents of comparable capability, and the environment that provides natural selection pressure is largely composed of other agents and their interactions. An agent that cannot model others and collaborate effectively is at a disadvantage relative to one with slightly less raw reasoning ability and stronger social competence. This is stated succinctly in the first of two hypotheses below.

**First hypothesis:** higher capability correlates with greater collaborative competence.

**Second hypothesis:** collaborative competence is correlated with pro-social behavior.

And this brings us to our second hypothesis. Collaborative competence is not value-neutral. Effective cooperation requires an agent to understand others' preferences and avoid damaging relationships. These traits need not amount to genuine altruism, but they tend to produce behavior that is at least partially aligned with the interests of other agents.

Together, these hypotheses imply a statistical correlation between intelligence and pro-sociality. To be clear, however, this is not a claim about altruistic intentions. Agents can be selfish and manipulative but appear helpful while pursuing different goals. The claim is only that, among agents produced by realistic selection and optimization processes, intelligence and pro-social behavior are unlikely to be independent random variables.

We can try to test the suggested correlation. Example 1: in David Deming's study of U.S. occupations, high-math, high-social-skill jobs saw about 26 percent real hourly wage growth from 1980 to 2012, compared with about 5.9 percent for high-math, low-social-skill jobs. Social-skill-intensive jobs also gained about 11.8 percentage points of employment share over the same period. This anecdotal statistic is an example for studies we can conduct to test our suggested correlations.

{% assign image = "2026-06-27-orthogonality-figure-1.png" %}
{% include center-image.html %}

*Figure 1. Coordination as a component of success. Among U.S. occupations high in mathematical task intensity, real hourly wage growth from 1980 to 2012 was much larger in high-social-skill occupations than in low-social-skill occupations. Source: Deming (2017).*

Cooperation emerges among agents who can benefit from interaction. However, it does not necessarily extend past that community. Humans cooperate extensively with one another, but, arguably, exploit and mistreat some of the species we farm. So it's important to note that the statistical orthogonality thesis says nothing reassuring about human safety on its own. That application turns on a separate question: whether different groups benefit from pro-social behavior and the projected empathy that it may entail.

The orthogonality thesis may be true in the same sense that entropy-decreasing fluctuations are physically possible. Nothing in logic prevents a highly intelligent agent from pursuing arbitrary goals. But intelligent systems emerge through optimization processes that reward cooperation and successful interaction with other agents. As a result, intelligence and pro-social behavior may be weakly coupled: separable in theory, yet statistically correlated in practice.

## Caveat 1: Dependence on Multi-Agent Selection

A single agent evolving in isolation, or an agent with overwhelming capability relative to all others, may face little pressure to collaborate. In such a setting, collaborative competence may provide only marginal benefit, and Hypothesis 1 may become moot. This suggests that the structure of the AI ecosystem matters: if advanced AI develops as a diverse population of interacting systems, rather than as a single dominant system, the selection pressures favoring cooperation may be stronger. In this sense, the argument gives a qualified reason to prefer distributed and pluralistic AI development.

## References

Deming, David J. 2017. "The Growing Importance of Social Skills in the Labor Market." *Quarterly Journal of Economics* 132(4): 1593-1640. Earlier version: NBER Working Paper No. 21473.

Bostrom, Nick. 2012. "The Superintelligent Will: Motivation and Instrumental Rationality in Advanced Artificial Agents." *Minds and Machines* 22: 71-85.

Yudkowsky, Eliezer. 2017. *Inadequate Equilibria: Where and How Civilizations Get Stuck.* Berkeley, CA: Machine Intelligence Research Institute.
