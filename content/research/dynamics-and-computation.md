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

This evolution, viewed as a dynamical system, raises quesitons of the form _"what will happen to the trajectory eventually?"_ and _"what can be said about the set of trajectories as a whole?"_. 

If $|z_0|$ is sufficiently large, e.g. $|z_0|>|c|+1$, then we will have $|z_1|>|z_0$, and the trajectory will rapidly escape to $\infty$. On the other hand, if $z_0$ is a root of the polynomial $z^2+c=z$, then it will be a *fixed point* of the dynamical system, and its trajectory will not escape to $\infty$. The *filled Julia set* in this case is the set of initial conditions for which the dynamics does not escape to $\infty$:
$$
K_c:=\lbrace z_0: z_t\nrightarrow\infty\rbrace. 
$$
The *Julia set* is the boundary of $K_c$: $J_c:=\partial K_c$. It is the set of points around which the long-term behavior is unstable: if $z\in J_c$, then any neighborhood of $z$ contains both points whose trajectories escape to $\infty$ and those whose trajectories stay bounded. 

#### Dynamical systems as computational devices and the Space-Bounded Church-Turing Thesis {#SBCT}



#### Further reading 

![Book Cover for "Computability of Julia Sets"](/media/BookCover.jpg#float-right)
Book: Computability of Julia Sets  
Mark Braverman, Michael Yampolsky  
Springer, 2009  
[\[Amazon\]](https://www.amazon.com/dp/3540685464) [\[Springer\]](https://www.springer.com/mathematics/computational+science+%26+engineering/book/978-3-540-68546-3)
