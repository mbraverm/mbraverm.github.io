---
title: Recent projects
weight: 20
draft: true
---

#### Information complexity

[Information theory](https://en.wikipedia.org/wiki/Information_theory) is a vastly successful theory underpinning much of our communication technology. In many important communication scenarios it allows one to calculate the precise amount of resources needed to perform a cetrain task. For example, the number of bits Alice needs to communicate to send a string $x_1 x_2 \ldots x_n$ of $n$ random trits (elements from $\{1,2,3\}$) to Bob is given by $(\log_2 3) \cdot n \pm o(n)$. The number of bits Alice needs to communicate to send $n$ random trits to Bob if Bob already knows half of the $x$'s (regarless of whether Alice knows which locations are known to Bob) is  $\frac{\log_2 3}{2}\cdot n \pm o(n)$ etc. These quantities can be written as expressions in terms of things like Shannon's entorpy, mutual information, and conditional mutual information. 

Notions of entropy and mutual information allow to precisely (and losslessly!) describe the flow of information in a variety of settings. They also allow to one to write "common sense" statements about information in precise mathematical terms which can then be manipulated. This turns out to be extremely useful in reasoning about communication. For example entropy $H(M)$ represents the amount of uncertainty in a message $M$. Mutual information $I(M;X)$ represents the amount of information the message $M$ reveals about a piece of data $X$. Conditional mutual information $I(M; X|Y)$ represents the amount of information a message $M$ reveals about $X$ to someone who already knows a piece of data $Y$. 

The chain rule 
$$
I(M_1 M_2; X) = I(M_1; X) + I(M_2; X|M_1)
$$
is just a precise way to formalize the intuitive fact that what one lears from two messages $M_1 M_2$ about $X$ can be decomposed into what we learned from the first message plus what we learned from the second message when we already knew the first one. 

