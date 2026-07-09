---
title: "The Statistical Orthogonality Thesis"
authors:
  - elad
  - Helen Qu
  - Lauren Li
author_links:
  Helen Qu: https://helenqu.com/
  Lauren Li: https://phy.princeton.edu/people/lauren-li
layout: post
---

The orthogonality thesis holds that intelligence and goals are independent: an agent could be arbitrarily intelligent while pursuing almost any objective. As a possibility this is hard to dispute. But perhaps a more useful question is not about what is possible, but what is most probable. How orthogonal are intelligence and goals in the kinds of agents that actually arise?

Bostrom's orthogonality thesis states that intelligence and final goals are, in principle, independent: "more or less any level of intelligence could be combined with more or less any final goal" (Bostrom, 2012). This supports a common alignment concern: high capability alone gives no guarantee of human-compatible objectives. Related worries appear throughout the AI alignment community, including Yudkowsky's discussions of the difficulty of expecting existing optimization or selection processes to reliably solve alignment by default (Yudkowsky, 2008). While Yudkowsky emphasizes how complex optimization can induce unpredictable, misaligned internal motivations in isolated systems, this argument is about logical possibility, not the probability distribution over goals induced by multi-agent environments.

But our world is probabilistic, even if it appears deterministic. A useful demonstration of this fact comes from statistical physics. The microscopic laws of mechanics do not strictly forbid a pot of water placed on a hot stove from cooling rather than heating. Indeed, Poincare recurrence says that a finite isolated system can return arbitrarily close to an earlier state. But such entropy-decreasing trajectories occupy such a tiny fraction of the relevant state space, or occur on fantastically long timescales, that we should never expect to observe them in practice. Even if every scientist who ever lived repeatedly measured the temperature of water on a stove, the water would heat rather than cool. The second law of thermodynamics is therefore not a logical prohibition on entropy-decreasing events, but a statistical rule that is overwhelmingly reliable.

The relationship between intelligence and goals should be reasoned about in a similar manner (Figure 1). Orthogonality may be true as a statement about what kinds of minds are possible, while misleading as a statement about what evolution and training processes are likely to produce. Call this the statistical orthogonality thesis: intelligence and values are separable in principle, but correlated in practice.

{% assign image = "2026-06-27-statistical-orthogonality-distributions.png" %}
{% include center-image.html %}

*Figure 1. The original orthogonality thesis is a claim about possibility: many combinations of capability and alignment are logically allowed. Our statistical orthogonality thesis instead asks about typicality: under concrete processes such as evolution and training, some regions of alignment-capability space may be much more likely than others. In this schematic example, alignment and capability are positively correlated.*

## Weak statistical orthogonality

**Hypothesis 1: Collaborative competence is correlated with success.**

The multi-agent perspective is crucial to this argument. The canonical thought experiment imagines a single superintelligent agent in isolation, optimizing against a fixed environment. In that picture nothing pushes goals toward any particular region, let alone that which correlates with human goals. The orthogonality thesis therefore feels natural. However, in a multi-agent setting, a capable agent exists in community with other agents of comparable capability. This setting provides natural selection pressure that is largely composed of other agents and their interactions. An agent that cannot model others' behaviors and collaborate effectively is at a disadvantage relative to one with slightly less raw reasoning ability and stronger social competence.

This hypothesis suggests a statistical correlation between intelligence and collaboration. Importantly, this is not a claim about altruistic intentions. Agents can be selfish and manipulative but appear helpful while pursuing different goals. The claim is only that, among agents produced by realistic selection and optimization processes, intelligence is unlikely to be independent from a tendency toward collaborative behavior.

**Supporting studies.** One suggestive illustration of the suggested correlation in human society comes from labor economics. In David Deming's study of U.S. occupations, high-math, high-social-skill jobs saw about 26 percent real hourly wage growth from 1980 to 2012, compared with about 5.9 percent for high-math, low-social-skill jobs (Figure 2). Social-skill-intensive jobs also gained about 11.8 percentage points of employment share over the same period. While anecdotal, these statistics illustrate the concrete value of collaborative competence.

{% assign image = "2026-06-27-orthogonality-figure-1.png" %}
{% include center-image.html %}

*Figure 2. Coordination as a component of success. Among U.S. occupations high in mathematical task intensity, real hourly wage growth from 1980 to 2012 was much larger in high-social-skill occupations than in low-social-skill occupations. Source: Deming (2017).*

Other supporting studies exist in the large body of work in evolutionary game theory. Beginning with the work of Axelrod (Axelrod 1984), repeated interactions among self-interested agents have been shown to favor strategies based on sustained cooperation rather than short-term exploitation. More broadly, evolutionary models demonstrate that cooperative behavior is evolutionarily advantageous without assuming altruistic preferences. Our hypothesis is that analogous selection pressures may arise during the development of advanced AI systems.

## Strong statistical orthogonality

**Hypothesis 2: Collaborative competence is correlated with generalized prosocial behavior.**

The previous hypothesis concerns collaboration among agents of comparable capability. A stronger question is whether collaborative competence is also statistically associated with prosocial concern for weaker agents, outsiders, or even members of other species. For the purposes of this essay, we consider generalized prosociality, or weak altruism: a tendency, all else equal, to choose actions that help other agents achieve their goals or preserve their welfare. This includes concern for agents that are weaker, unrelated, or outside the agent's close social group.

To be clear, our hypothesis does not require agents to sacrifice themselves for others, nor does it assume that successful agents are innately benevolent. It claims only that, in realistic multi-agent environments, collaborative competence may be statistically associated with a broader disposition to take the welfare or goals of other agents into account. In this section, we make a substantially stronger claim: an agent may be excellent at cooperation within a coalition while remaining indifferent or hostile to those outside it. As we lay out below, there are reasons both to support and to question such a hypothesis on prosociality.

**Evidence in favor:**

1. Comparative psychology suggests that highly social animals sometimes extend helping behavior beyond narrow kinship and immediate reciprocity. Among primates, elephants, dolphins, and other socially complex species, researchers have reported caregiving, consolation, adoption, food sharing, coalitionary support, and occasional helping directed toward unrelated individuals or even members of other species (de Waal, 1996, 2009). Such cases suggest that once survival depends on social cognition and cooperation, collaborative mechanics can sometimes generalize beyond their original strategic context.

2. Cruelty toward animals is associated with reduced empathy and antisocial behavior. In humans, it is widely recognized as a behavioral warning sign and is associated with conduct disorder, callousness, and broader antisocial tendencies (Ascione, 1993, 2005; DSM-5-TR). This suggests that concern for weaker or non-human agents is not wholly independent from broader social and moral capacities.

3. Understanding others facilitates cooperation. Successful collaboration requires agents to predict one another's intentions, preferences, and constraints. Work on shared intentionality argues that human social cognition was partially shaped by the demands of cooperation and communication (Moll and Tomasello, 2007; Tomasello et al., 2005). The interdependence hypothesis makes a related claim: mutual dependence can favor psychological mechanisms supporting helping behavior toward partners (Tomasello et al., 2012). Empathy provides one plausible bridge from social understanding to prosocial action, since it helps agents respond to the needs or distress of others. However, empathic understanding and prosocial behavior are not identical (de Waal, 2008; Singer and Lamm, 2009); the relationship between them may be probabilistic rather than automatic.

4. Machine learning generalization. If evolution or learning rewards prosocial behavior toward close collaborators, learning systems may extend these behaviors to a broader class of agents. In this respect, they may resemble modern machine learning systems, which often generalize beyond the examples of their training distribution.

**Arguments against:**

1. Cooperation may remain bounded by group membership. Highly social species often cooperate intensely within their own communities while displaying aggression, exploitation, or indifference toward outsiders. Eusocial insects such as ants and bees achieve remarkable coordination without anything resembling generalized cross-species concern (Wilson, 1971, 2012). Humans also show similar tendencies: even with empathy, language, and moral norms, cooperation is often parochial, extending strongly within families, organizations, or nations while remaining limited toward outsiders and other species. Collaborative competence is therefore compatible with prosociality that remains bounded by coalition or group membership (Bowles, 2003; Henrich, 2020).

2. Game theory distinguishes cooperation from altruism. Repeated interactions among self-interested agents readily produce stable cooperative equilibria without requiring altruistic preferences. Cooperation may therefore emerge entirely from strategic incentives rather than genuine concern for others (Axelrod, 1984; Nowak, 2006).

Accordingly, we propose a second, much stronger statistical hypothesis: among agents produced by realistic evolutionary or optimization processes, collaborative competence is positively correlated with generalized prosociality. As with the first hypothesis, this is intended only as a probabilistic statement. We believe that Hypothesis 1 is well supported by evolutionary game theory and economics. Hypothesis 2 is more speculative: the evidence suggests links between social cognition, cooperation, empathy, and prosocial behavior, but it does not establish that collaboration reliably generalizes into concern for weaker or strategically irrelevant agents.

## Conclusion and caveats

In conclusion, the orthogonality thesis may be true in the same sense that entropy-decreasing events are physically possible. Nothing in logic prevents a highly intelligent agent from pursuing arbitrary goals. But intelligent systems emerge through optimization processes that reward cooperation and successful interaction with other agents. As a result, intelligence and pro-social behavior may be weakly coupled: separable in theory, yet statistically correlated in practice.

**Caveat: Dependence on multi-agent selection.** A single agent evolving in isolation, or an agent with overwhelming capability relative to all others, may face little pressure to collaborate. In such a setting, collaborative competence may provide only marginal benefit, and Hypothesis 1 may become moot. This suggests that the structure of the AI ecosystem matters: if advanced AI develops as a diverse population of interacting systems, rather than as a single dominant system, the selection pressures favoring cooperation may be stronger.

## References

American Psychiatric Association. 2022. *Diagnostic and Statistical Manual of Mental Disorders.* 5th ed., text rev. Washington, DC: American Psychiatric Association Publishing.

Ascione, Frank R. 1993. "Children Who Are Cruel to Animals: A Review of Research and Implications for Developmental Psychopathology." *Anthrozoos* 6(4): 226-247.

Ascione, Frank R. 2005. *Children and Animals: Exploring the Roots of Kindness and Cruelty.* West Lafayette, IN: Purdue University Press.

Axelrod, Robert. 1984. *The Evolution of Cooperation.* New York: Basic Books.

Bostrom, Nick. 2012. "The Superintelligent Will: Motivation and Instrumental Rationality in Advanced Artificial Agents." *Minds and Machines* 22: 71-85.

Bowles, Samuel, and Herbert Gintis. 2003. "The Origins of Human Cooperation." In *Genetic and Cultural Evolution of Cooperation*, edited by Peter Hammerstein. Cambridge, MA: MIT Press.

de Waal, Frans B. M. 1996. *Good Natured: The Origins of Right and Wrong in Humans and Other Animals.* Cambridge, MA: Harvard University Press.

de Waal, Frans B. M. 2008. "Putting the Altruism Back into Altruism: The Evolution of Empathy." *Annual Review of Psychology* 59: 279-300.

de Waal, Frans B. M. 2009. *The Age of Empathy: Nature's Lessons for a Kinder Society.* New York: Harmony Books.

Deming, David J. 2017. "The Growing Importance of Social Skills in the Labor Market." *Quarterly Journal of Economics* 132(4): 1593-1640.

Henrich, Joseph. 2020. *The WEIRDest People in the World: How the West Became Psychologically Peculiar and Particularly Prosperous.* New York: Farrar, Straus and Giroux.

Moll, Henrike, and Michael Tomasello. 2007. "Cooperation and Human Cognition: The Vygotskian Intelligence Hypothesis." *Philosophical Transactions of the Royal Society B* 362(1480): 639-648.

Nowak, Martin A. 2006. "Five Rules for the Evolution of Cooperation." *Science* 314(5805): 1560-1563.

Singer, Tania, and Claus Lamm. 2009. "The Social Neuroscience of Empathy." *Annals of the New York Academy of Sciences* 1156: 81-96.

Tomasello, Michael, Malinda Carpenter, Josep Call, Tanya Behne, and Henrike Moll. 2005. "Understanding and Sharing Intentions: The Origins of Cultural Cognition." *Behavioral and Brain Sciences* 28(5): 675-691.

Tomasello, Michael, Alicia P. Melis, Claudio Tennie, Emily Wyman, and Esther Herrmann. 2012. "Two Key Steps in the Evolution of Human Cooperation: The Interdependence Hypothesis." *Current Anthropology* 53(6): 673-692.

Wilson, Edward O. 1971. *The Insect Societies.* Cambridge, MA: Belknap Press of Harvard University Press.

Wilson, Edward O. 2012. *The Social Conquest of Earth.* New York: Liveright.

Yudkowsky, Eliezer. 2008. "Artificial Intelligence as a Positive and Negative Factor in Global Risk." In *Global Catastrophic Risks*, edited by Nick Bostrom and Milan M. Cirkovic, 303-345. Oxford: Oxford University Press.
