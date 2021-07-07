---
title: Mechanism design
weight: 20
draft: false
---

1. [Black-box reductions from algorithms to mechanisms without money]({{< ref "#BlackBox" >}})
2. [Strategic capitation: mechanism design in the "big data" regime]({{< ref "#StrategicCapitation" >}})
3. [Mechanism design for learning agents]({{<ref "#LearningAgents">}})

#### Overview 

**Algorithm design vs. mechanism design.** The starting point of *Algorithm design* is a specified input-output behavior: $L$ is a list of numbers, and $SORT(L)$ is the same list sorted in ascending order; $f$ is boolean formula, and $SAT(f)$ is a satisfying assignment -- if one exists; $D$ is a list of labeled examples, and $Model(D)$ is a trained model for labeling previously unseed examples. Some of these tasks are incredibly complex. Much of computer science (and applied mathematics) is about finding new ways of performing these tasks. No matter how complex the algorithmic task at hand, it is normally assumed that the input $x$ does not depend on algorithm $A$. 

When the inputs to an algorithm $A$ come from outside parties interested in the output of the algorithm, this assumption breaks down. For example, underlying an [auction](https://en.wikipedia.org/wiki/Auction) is typically a simple optimization algorithm (with a single item for sale, the algorithm is just the $max$ function). However, inputs come from bidders who might (and will) optimize their bids to get an improved outcome (for example, get the item for as little money as possible). The field of [mechanism design](https://en.wikipedia.org/wiki/Mechanism_design) studies designing algorithms where the inputs are provided by self-interested (and potentially strategic) agents. Mechanism design draws on [game theory](https://en.wikipedia.org/wiki/Game_theory) for its modeling foundations. *Algorithmic mechanism design* specifically studies settings where both the algorithmic and game-theoreic aspects play an important role. 

Within theoretical computer science, there are several reasons to study algorithmic mechanism design now. Algorithmic mechanism design is becoming more important as algorithms enter more application domains. Even in areas where the "algorithms" involved are fairly simple, the availability of data and cheap compute means that it is easy for participants to be more strategic. This means that systems design needs to incorporate mechanism design thinking. Ideally, a set of transformations and heuristics would make this process automatic or at least routine. On the other hand, algorithms (along with data and hardware) are evolving at a rapid rate, giving rise to exciting new opportunities for making systems better using mechanims that incorporate these algorithmic advances. 

Algorithms are entering more domains. 

Implicit mechanisms become explicit. 

Mechanisms: keeping up with algorithmic advances. 

#### Black-box reductions from algorithms to mechanisms without money {#BlackBox}

Further reading: 

* Preprint: [arXiv](https://arxiv.org/abs/2106.07752)

#### Strategic capitation: mechanism design in the "big data" regime {#StrategicCapitation}

#### Mechanism design for learning agents {#LearningAgents}
