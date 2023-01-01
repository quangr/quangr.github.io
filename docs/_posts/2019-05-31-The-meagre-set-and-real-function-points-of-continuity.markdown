---
layout: post
title:  "The meagre set and real function's points of continuity"
date:   2019-05-31 19:12:14 +0800
categories: math
---
The question goes like this:

>Find a measure zero set in [a,b],and for any $$f \in R([a,b])$$ E will contained some continuity points of f.

We first find a $$G_ {\delta}$$set Z which satisfied $$Z\subset Q\cap [a,b]$$ and $$m(Z)=0$$. This can be achieved in many ways, like select sets from the open set from $$m^* (Q)$$ or let $$E_ n=\bigcup _ {n=1}^{\infty}(r_ n-2^{2-n-m},r_ n+2^{2-n-m})$$ and let $$Z=\cap E_ n$$.Note that Z is a $$G_ {\delta}$$set and contain all the rational in [a,b]. So the complement of Z is a $$F_ {\sigma}$$set which is a meagre set, for $$E_ n^C$$ is nowhere dense in [a,b].
Now we must argue that Z is the set we want. Let the E denote the set of all continuity points of F.If $$Z\cap E=\emptyset$$, than $$E\subset Z^C$$ which makes E a meagre set(notice that any subset of a meagre set is meagre. ). 


Lemma1:
>For any dense subset E of [a,b], if it is the intersection of countably many open sets then it is a second category set.

Proof: Suppose that $$E=\cap E_ n$$, and each $$E_ n$$ is dense so $$E_ n^C$$ are closed sets and nowhere dense, so $$\cup E_ n^C$$ is a meagre set. $$[a,b]=E\cup E_ n^C$$ and [a,b] can't be a meagre set.


Lemma2:
>If $$f \in R([a,b])$$, then the set of all continuity points of f is a second category set.

Proof:For f is Riemman integrable, we first notice that $$m([a,b]\setminus E)=0$$. And every real function's continuity points set is a $$G_ {delta}$$ set. So we shall see that if $$E=\cap E_ n$$, than the $$E_ n^C$$ will a closed set with zero measure, which means it can't contain any open set. So each $$E_ n^C$$ is dense. By the lemma1 we can immediately deduce the result.


Now we have proved that E is a second category set,which lead to a contradiction.

2020.02.14

无意中在飞跃手册里看到这个问题：[0,1]上的可微函数和连续不可微函数哪个多？ 这正好是一个meagre set有关的问题。


These two sets have same cardinal numbers, since every differentiable function add a nowhere differentiable function is a nowhere differentiable function, and every nowhere differentiable function's integral is a differentiable function.

Now we want to prove the set E of all continuous function in [0,1] that are differentiable at some point is a meagre set in Banach space C[0,1]. Because differentiable function (polynomial) sets is dense in C[0,1] , so does nowhere differentiable functions. We need prove E is a close set. If $$f_n$$ is a sequence of function in E converge to some f in C[0,1]. Let $$f_n$$ be differentiable at point $$x_n$$. Then $$\{x_n\}$$ has a subsequence converge to x in [0,1]. Since the converge is uniform, $$\vert\frac{f(x+h)-f(x)}{h}\vert\leq \vert\frac{f(x+h)-f_n(x+h)}{h}\vert+\vert\frac{f_n(x+h)-f_n(x)}{h}\vert+\vert\frac{f_n(x)-f_n(x)}{h}\vert$$.

# Reference 
[A detailed proof of second question](http://homepages.math.uic.edu/~marker/math414/fs.pdf)