---
title: Recent projects
weight: 20
draft: false
---

## Information complexity

[Information theory](https://en.wikipedia.org/wiki/Information_theory) is a vastly successful theory underpinning much of our communication technology. In many important communication scenarios it allows one to calculate the precise amount of resources needed to perform a cetrain task. For example, the number of bits Alice needs to communicate to send a string $x_1 x_2 \ldots x_n$ of $n$ random trits (elements from $\{1,2,3\}$) to Bob is given by $(\log_2 3) \cdot n \pm o(n)$. The number of bits Alice needs to communicate to send $n$ random trits to Bob if Bob already knows half of the $x$'s (regarless of whether Alice knows which locations are known to Bob) is  $\frac{\log_2 3}{2}\cdot n \pm o(n)$ etc. These quantities can be written as expressions in terms of things like Shannon's entorpy, mutual information, and conditional mutual information. 

Notions of entropy and mutual information allow to precisely (and losslessly!) describe the flow of information in a variety of settings. They also allow to one to write "common sense" statements about information in precise mathematical terms which can then be manipulated. This turns out to be extremely useful in reasoning about communication. For example entropy $H(M)$ represents the amount of uncertainty in a message $M$. Mutual information $I(M;X)$ represents the amount of information the message $M$ reveals about a piece of data $X$. Conditional mutual information $I(M; X|Y)$ represents the amount of information a message $M$ reveals about $X$ to someone who already knows a piece of data $Y$. 

The *chain rule*
$$
I(M_1 M_2; X) = I(M_1; X) + I(M_2; X|M_1)
$$
is just a precise way to formalize the intuitive fact that what one learns from two messages $M_1 M_2$ about $X$ can be decomposed into what we learned from the first message plus what we learned from the second message when we already knew the first one. The *data processing inequality*
$$
I(X;F(Y)) \le I(X;Y)
$$
formalizes the intuition that a function computed on $Y$ cannot reveal more about $X$ than $Y$ itself. 

The goal of information complexity is to learn to apply information-theoretic formalism to computational settings. As of now (2021), these tend to work beautifully in models of computation that are simple enough to not support information-theoretically [secure computation](https://en.wikipedia.org/wiki/Secure_multi-party_computation). Understanding why exactly this happens is an interesting direction for future work. Below we give some examples of results based on information complexity from the 2010-2020 period. In some cases the results are new, while in others they give conceptually simpler proofs or more general statements of existing theorems.  

#### Two party communication 

![A randomized two-party protocol](/media/Protocol1.PNG#float-right)

In the two-party [communication complexity](https://en.wikipedia.org/wiki/Communication_complexity) setting, two players (Alice and Bob) are given inputs $X$ and $Y$. They are also allowed to use a randomness source $R$. A *protocol* $\pi$ is just a formalization of a conversation: each message in $\pi$ is allowed to depend on the speaker's input, on the conversation so far, and on the public randomness. The *communication cost* of a protocol is the number of bits communicated during its execution. The *communication complexity* of a task $T$ is the smallest communication cost of a protocol $\pi$ solving $T$. In the context of communication complexity, $T$ is typically the task of "computing a given function $F(X,Y)$ with error probability $<\varepsilon$. 

An instructive example is the *Equality* problem. Alice is given an $n$-bit string $X$, Bob is given an $n$-bit string $Y$, and they would like to determine whether $X=Y$. It can be shown that this can be accomplished with error $<\varepsilon$ using $k \sim \log (1/\varepsilon)$ bits of communication. Alice will compute a random hash $h(X)$ of lenght $k$ on her input $X$ and send the value to Bob. Bob will compare $h(X)$ to $h(Y)$, and will return 'equal' if they match. There is a $2^{-k}$ probability of hash collision, which means that 'equal' is returned with probability $\approx 2^{-k}$ even when $X\neq Y$. Interestingly, a zero-error protocol for equality requires $n+1$ bits of communication. 

*Further reading*: a survey can be found here. 
