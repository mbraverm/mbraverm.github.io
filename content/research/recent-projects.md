---
title: Recent projects
weight: 20
draft: true
---

## Information complexity

[Information theory](https://en.wikipedia.org/wiki/Information_theory) is a vastly successful theory underpinning much of our communication technology. In many important communication scenarios it allows one to calculate the precise amount of resources needed to perform a cetrain task. For example, the number of bits Alice needs to communicate to send a string $x_1 x_2 \ldots x_n$ of $n$ random trits (elements from $\lbrace 1,2,3\rbrace$) to Bob is given by $(\log_2 3) \cdot n \pm o(n)$. The number of bits Alice needs to communicate to send $n$ random trits to Bob if Bob already knows half of the $x$'s (regarless of whether Alice knows which locations are known to Bob) is  $\frac{\log_2 3}{2}\cdot n \pm o(n)$ etc. These quantities can be written as expressions in terms of things like Shannon's entorpy, mutual information, and conditional mutual information. 

Notions of entropy and mutual information allow to precisely (and losslessly!) describe the flow of information in a variety of settings. They also allow to one to write "common sense" statements about information in precise mathematical terms which can then be manipulated. This turns out to be extremely useful in reasoning about communication. For example entropy $H(M)$ represents the amount of uncertainty in a message $M$. Mutual information $I(M;X)$ represents the amount of information the message $M$ reveals about a piece of data $X$. Conditional mutual information $I(M; X|Y)$ represents the amount of information a message $M$ reveals about $X$ to someone who already knows a piece of data $Y$. 

The *chain rule*
$$
I(M_1 M_2; X) = I(M_1; X) + I(M_2; X|M_1)
$$
is just a precise way to formalize the intuitive fact that what one learned from two messages $M_1 M_2$ about $X$ can be decomposed into what one learned from the first message plus what one learned from the second message when we already knew the first one. The *data processing inequality*
$$
I(X;F(Y)) \le I(X;Y)
$$
formalizes the intuition that a function computed on $Y$ cannot reveal more about $X$ than $Y$ itself. 

The goal of information complexity is to learn to apply information-theoretic formalism to computational settings. As of now (2021), these tend to work beautifully in models of computation that are simple enough to not support information-theoretically [secure computation](https://en.wikipedia.org/wiki/Secure_multi-party_computation). Understanding why exactly this happens is an interesting direction for future work. Below we give some examples of results based on information complexity from the 2010-2020 period. In some cases the results are new, while in others they give conceptually simpler proofs or more general statements of existing theorems.  

#### Two party communication 

![A randomized two-party protocol](/media/Protocol1.PNG#float-right)

In the two-party [communication complexity](https://en.wikipedia.org/wiki/Communication_complexity) setting, two players (Alice and Bob) are given inputs $X$ and $Y$. They are also allowed to use a randomness source $R$. A *protocol* $\pi$ is just a formalization of a conversation: each message in $\pi$ is allowed to depend on the speaker's input, on the conversation so far, and on the public randomness. The *communication cost* of a protocol is the number of bits communicated during its execution. The *communication complexity* $CC(T)$ of a task $T$ is the smallest communication cost of a protocol $\pi$ solving $T$. In the context of communication complexity, $T$ is typically the task of "computing a given function $F(X,Y)$ with error probability $<\varepsilon$". 

An instructive example is the *Equality* problem. Alice is given an $n$-bit string $X$, Bob is given an $n$-bit string $Y$, and they would like to determine whether $X=Y$. It can be shown that this can be accomplished with error $<\varepsilon$ using $k \sim \log (1/\varepsilon)$ bits of communication. Alice will compute a random hash $h(X)$ of lenght $k$ on her input $X$ and send the value to Bob. Bob will compare $h(X)$ to $h(Y)$, and will return 'equal' if they match. There is a $2^{-k}$ probability of hash collision, which means that 'equal' is returned with probability $\approx 2^{-k}$ even when $X\neq Y$. Interestingly, a zero-error protocol for equality requires $n+1$ bits of communication. 

Another function with many applications in lower bounds is *Disjointness*. Alice and Bob are given subsets $X,Y\subset \lbrace 1,\ldots,n\rbrace$ (wich can be represented as length-$n$ bit-strings), and need to determine whether they have an element in common. $Disj_n(X,Y)=1$ if the sets are disjoint, and $0$ if they intersect. 

#### Direct sum and information complexity

The *direct sum* problem (in any model of computation) asks whether it costs $k$ times as much to perform $k$ independent copies of a task $T$ as it costs to perform one copy, or whether one gets a "volume discount". When direct sum holds, one gets a powerful lower bounds tool --- a lower bound $L$ on $T$ gets amplified into a lower bound of $k\cdot L$ on the task $T^k$ of performing $k$ copies of $T$. When direct sum fails, new interesting algorithms follow. A famous example of such a failure is matrix-vector multiplication. A counting argument shows that one needs $>n^2$ operations to mutiply an $n\times n$ matrix $A$ by a vector $v$. At the same time, multiplying $A$ by $n$ different vectors $v_1,\ldots,v_n$ is just the problem of multiplying two $n\times n$ matrices, which can be done faster than $n\cdot n^2=n^3$ via [fast matrix multiplication](https://en.wikipedia.org/wiki/Matrix_multiplication_algorithm#Sub-cubic_algorithms). 

The *Direct Sum Problem* for randomized communication complexity asked whether the direct sum property holds for randomized communication complexity. That is, whether $CC(T^k)\gtrsim k\cdot CC(T)$? It turns out that trying to answer this question is closely related to understanding the *information complexity* of $F$. 

Information complexity is defined similarly to communication complexity, with information cost replacing communication cost. The (two-party) *information cost* of a protocol $\Pi$ on inputs $(X,Y)$ is defined to be the amount of information the participants learn about each other's inputs during the execution of the protocol. Fortunately, the information-theoretic notation makes this quantity easy to formalize:
$$
IC(\Pi):= I(X;\Pi|Y) + I(Y;\Pi|X). 
$$
The first term corresponds to what Bob (who knows $Y$) learns about Alice's input ($X$) from the protocol $\Pi$. The second term corresponds to what Alice learns. 
The information complexity of a task $T$ over inputs $(X,Y)$ is defined as the smallest possible information cost of a protocol solving $T$. 
$$
IC(T):= \inf_{\text{$\Pi$ solves $T$}} IC(\Pi). 
$$
The infimum here is necessary, since it is possible that there is a sequence of successful protocols $\Pi_1,\Pi_2,\ldots$ that get ever longer while revealing an ever smaller amount of information (in fact, this happens for the simple task of computing the two-bit AND function). 

It turns out that the amortized (per-copy) communication complexity of a task $T$ is equal to its information complexity, at least when a vanishing amount of error is allowed. Let $T(X,Y)$ be a task that allows for a small amount of error $\ve=o(1)$. Let $CC(T^k)$ be the communication complexity of $k$ copies of $T$, and let $IC(T)$ be its information complexity. Then information is equal to amortized communication:

**Theorem [[BR'11]](https://arxiv.org/abs/1106.3595):** $\displaystyle{\lim_{k\rightarrow\infty} \frac{CC(T^k)}{k} = IC(T)}$. 

#### Interactive compression

This theorem gives an immediate blueprint for proving direct sum theorems for (randomized) communication complexity. To show (for example) that $CC(T^k) \gtrsim k\cdot CC(T^k)$, one can show that $IC(T)\gtrsim CC(T)$. This inequality, more commonly written as $CC(T)\lesssim IC(T)$ is known as the [*interactive compression*](https://arxiv.org/abs/1504.06830) question. It asks whether a protocol $\pi$ that solves $T$ while revealing little information can be "compressed" into a protocol $\pi'$ that uses little communication. 

In the context of one-way communication near-perfect compression is generally possibly. For example [Huffman coding](https://en.wikipedia.org/wiki/Huffman_coding) allows one to encode a message with entropy $H(M)$ using at most $H(M)+1$ bits in expectation. It is generally the case that a protocol with $r$ rounds of communication can be compressed into $O(IC(\Pi)+r)$ bits of communication. Unfortunately, the protocol achieving $IC(T)$ may have an unbounded number of rounds, making such a compression useless in the general interactive setting. 

It turns out that it is possible to compress a general protocol $\pi$ whose information cost is $I$ and whose communication cost is $C$ into a protocol $\pi'$ whose communication cost is $\tilde{O}(\sqrt{I\cdot C})$. This leads to a partial direct sum theorem for randomized communication:

**Theorem [[BBCR'10]](/files/directsum.pdf):** $\displaystyle{CC(T^k)}=\tilde{\Omega}(\sqrt{k}\cdot CC(T))$. 

At the same time, Ganor, Kol, and Raz showed a separation between information and communication complexity:

**Theorem [[GKR'15]](https://eccc.weizmann.ac.il/report/2014/113/):** There is a family of functions whose information complexity is $n$ and whose communication complexity is $2^{\Omega(n)}$. 

Moreover, it can be shown that this separation is tight - communication complexity is always at most exponential in information complexity. The *GKR'15* theorem rules out a tight direct sum theorem for communication complexity. It still remains open whether the $\sqrt{k}$ in *BBCR'10* can be improved, e.g. to $k^{1-\varepsilon}$. 

#### Direct product and parallel repetition: using information formalism

#### The two-bit AND function and Disjointness

#### Does one need memory to approximately count?

*Further reading*: a survey can be found here. 
Quantum information complexity. 
Parallel repetition. 
