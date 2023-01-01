---
layout: post
title:  "A note on Riemman integral and Darboux Integral"
date:   2019-06-21 16:55:14 +0800
categories: math
---
In Rudin's book Principles of Mathematical Analysis, he only gives the definition of the Darboux Integral. But when we try to build a connection between Riemman integral and Lebesgue integral, both definition can be important, so I will show the equivalent of these two definitions.

>dicing lemma:Let $$f :[a, b] \rightarrow \mathbb{R}$$be bounded. For all $$\epsilon>0$$,there exists $$\delta>0$$ such that for all partitions P of [a, b] with $$\mid \mathcal{P}\mid <\delta$$


$$\underline{\int_{a}}^{b} f-L(f, \mathcal{P})<\epsilon, U(f, \mathcal{P})-\overline{\int_{a}^{b}} f<\epsilon$$


Proof idea: Choose the partition $$P_{\epsilon}$$ close to the upper Darboux integral, then choose $$\delta$$ such that $$2 M N \delta<\frac{\epsilon}{2}$$, N is the number of subintevals of $$P_{\epsilon}$$. Let $$P$$ be any partition with $$\mid \mathcal{P}\mid <\delta$$, we compare the Darboux sums of $$P$$ and $$P'=P\cup P_{\epsilon}$$. For P' contains at most N-1 more different points than P, we found the differece will less than $$2 M N \delta$$.


The final conclusion lists as follow:

For a function $$f :[a, b] \rightarrow \mathbb{R}$$, the following are equivalent:


(i) f is Darboux integrable.


(ii) There exists a number I such that for all $$\epsilon>0$$, there exists $$\delta>0$$ such that for all partitions P of [a, b] of mesh at most $$\delta$$ and all taggings $$\tau$$ of P,
$$\mid R(f, \mathcal{P}, \tau)-I\mid <\epsilon$$.


(iii) For every sequence $$\left(\mathcal{P}_{n}, \tau_{n}\right)$$ of tagged partitions of [a, b] such that $$\mid \mathcal{P}_{n}\mid  \rightarrow 0$$,the sequence of Riemann sums $$R\left(f, \mathcal{P}_{n}, \tau_{n}\right)$$ is convergent.