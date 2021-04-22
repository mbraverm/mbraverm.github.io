---
title: Dynamics and computation
weight: 20
draft: false
---

A *[dynamical system](https://en.wikipedia.org/wiki/Dynamical_system)* is a stateful system (often with a continuous state space) evolving over time. Thus, dynamical systems can be (and are being) used to capture the behavior of both natural and articifical systems over time. 
The state space of dynamical systems is typically continuous, which means that one has to look at continuous models of computation. [Here](https://cacm.acm.org/magazines/2013/9/167157-computing-with-real-numbers-from-archimedes-to-turing-and-beyond/fulltext) is a Communications of the ACM article I wrote on computation over the reals in 2013. [There](https://www.ams.org/notices/200603/fea-cook.pdf) is also an older 2006 article with Stephen Cook in the Notices of the AMS. 

There are at least two natural connections between dynamics and computation. In one direction, the question *"which properties of which dynamical systems can be computed and how efficiently?"* is foundational to mapping the limits of applied mathematics. In the opposite direction, *"how powerful a computation can a given dynamical system simulate robustly?"* touches upon the [Church-Turing thesis](https://en.wikipedia.org/wiki/Church%E2%80%93Turing_thesis) and questions of [hypercomputation](https://en.wikipedia.org/wiki/Hypercomputation). 

1. [Which properties of dynamical systems can be computed? The case of Julia sets]({{< ref "#Julia" >}})
2. [Dynamical systems as computational devices and the Space-Bounded Church-Turing Thesis]({{<ref "#SBCT">}})

#### Which properties of dynamical systems can be computed? The case of Julia sets {#Julia}

[Julia sets](https://en.wikipedia.org/wiki/Julia_set) are some of the most visualized objects in Mathematics. They arise in the study of [complex dynamics](https://en.wikipedia.org/wiki/Complex_dynamics) (that is, the state space if the set $\mathbb{C}$ of complex numbers, visualized on the plane), along with the [Mandelbrot set](https://en.wikipedia.org/wiki/Mandelbrot_set). From the scientific perspective, the family of Julia sets and the complex dynamics that gives rise to them, are sufficiently rich to exhibit phenomena one sees in the "wild". At the same time, after 100+ years of deep study, we know a lot about them, making them good "lab models" for more general dynamical systems. Computer programs had been written to visualize Julia sets (by amateur programmers and professional mathematicians alike). Thus questions about computational properties of Julia sets are natural to consider, and may shed light on the broader set of phenomena we should expect in "computablility of dynamical systems". 

Consider the quadratic function $f_c:\mathbb{C}\rightarrow \mathbb{C}$ given by $f_c(z):=z^2+c$. 
For any initial point $z_0$, the mapping $f_c$ induces a (discrete-time) trajectory of the evolution of $z$ under $f_c$: $z_1=f_c(z_0)=z_0^2+c$, $z_2=f_c(z_1)=(z_0^2+c)^2+c$, and more generally $z_{t+1}=f_c(z_t)$. 

This evolution, viewed as a dynamical system, raises quesitons of the form *"what will happen to the trajectory eventually?"* and *"what can be said about the set of trajectories as a whole?"*. 

If $|z_0|$ is sufficiently large, e.g. $|z_0|>|c|+1$, then we will have $|z_1|>|z_0|$, and the trajectory will rapidly escape to $\infty$. On the other hand, if $z_0$ is a root of the polynomial $z^2+c=z$, then it will be a *fixed point* of the dynamical system, and its trajectory will not escape to $\infty$. The *filled Julia set* in this case is the set of initial conditions for which the dynamics does not escape to $\infty$:
$$
K_c:=\lbrace z_0: z_t\nrightarrow\infty\rbrace. 
$$
The *Julia set* is the boundary of $K_c$: $J_c:=\partial K_c$. It is the set of points around which the long-term behavior is unstable: if $z\in J_c$, then any neighborhood of $z$ contains both points whose trajectories escape to $\infty$ and those whose trajectories stay bounded. 

![A Julia set with a Siegel disc and a trajectory](/media/Dynamical-Systems/Julia-J3A1B.gif#float-right)

As it turns out, there exist non-computable quadratic Julia sets:

**Theorem [[BY'06]](https://www.ams.org/journals/jams/2006-19-03/S0894-0347-05-00516-3/):** There exists a parameter $c$ such that no Turing Machine with access to parameter $c$ can compute arbitrarily precise picture of $J_c$. 

Moreover, it turns out that such a $c$ can be computed explicitly [[BR07]](https://arxiv.org/abs/math/0604371). 

When a non-computability result is present, one might expect non-computability to be the rule, and computational tractability to be a lucky exception. Quadratic Julia sets are an interesting case-study, since they are rich enough to support many dynamically interesting behaviors, but are sufficiently well-understood to allow us to answer most questions about their computational properties. Surprisingly, *non-computability sometimes occurs, but it is the exception*. 

In fact, by several measures, we either know that "most" quadratic Julia sets are computable, or strongly suspect that they are. Intuitively, the non-computable examples are constructed by carefully encoding a computationally difficult function into the parameter $c$ at infinitely many scales (more precisely, the encoding uses a [continued fraction](https://en.wikipedia.org/wiki/Continued_fraction) expansion). Perturbing $c$ by even a tiny amount will destroy most of this encoding. 

#### Dynamical systems as computational devices and the Space-Bounded Church-Turing Thesis {#SBCT}



#### Further reading 

![Book Cover for "Computability of Julia Sets"](/media/BookCover.jpg#float-right)
Book: Computability of Julia Sets  
Mark Braverman, Michael Yampolsky  
Springer, 2009  
[\[Amazon\]](https://www.amazon.com/dp/3540685464) [\[Springer\]](https://www.springer.com/mathematics/computational+science+%26+engineering/book/978-3-540-68546-3)
