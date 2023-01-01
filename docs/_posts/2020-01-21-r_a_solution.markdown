---
layout: post
title:  "Solution for Measure, Integration & Real Analysis"
date:   2020-01-21 21:09:14 +0800
categories: math
---

2020.01.21


知乎上看到Axler大神出了一本实变函数的新书，趁寒假重新学一遍实变。结果发现讲实变的前几章就是很快的过一遍常规内容，好像没什么特别的(除了强调Borel测度，鄙视Lebesgue测度- -)，导数那章讲的也很浅。复习了一下存在反函数不可测的单调连续可测函数，以及一个奇怪的可测集使得与任何区间的交集长度比例大于0小于1（这个集合和之前构造的那个零测度疏集很像，这个例子好像还来自Rudin的实分析- -）。不过从Product Measure 那章开始还可以，还顺便介绍了一点超球体，后面的内容就当学一遍泛函了。

2020.02.01

终于读完了，感觉这其实就是本泛函书- -，而且有几道习题有点变态，而且完全不知道最后搞一章概率论内容是在干嘛。不过这本书的最大亮点（我乱说的）是用泛函工具处理复测度从而导出Radon-Nikokdym定理，以及最后加了一章傅里叶分析内容来展示泛函工具摧枯拉朽的力量。相比之下Stein丛书先讲傅里叶分析再讲复分析再讲实分析，如果没读过第一本书，就少了很多动机。作为一本泛函入门书，不管是从叙述的流畅性还是习题的角度都可以打满分。感觉是这一年读的最顺的一本，在此怀念那些读Stein复分析、以及[条件概率讲义](http://web.math.ku.dk/noter/filer/beting.pdf)的痛苦岁月。

## Banach and All His Friends: Hahn and Zorn

# 6.A: 

6 (a) Prove that if V is a metric space, $$f\in V$$,and r > 0,then $$B(f,r) \subset B(f,r)$$. 

(b) Give an example of a metric space V, $$f \in V$$, and r > 0 such that $$B(f,r) \neq B(f,r)$$.

A: Consider the trivial metric space.

9.Prove that each open subset of a metric space V is the union of some sequence of closed subsets of V. 

A:Consider the union of  $$\{d(G^C,x) < r \}^C$$.


# 6.C:

7 Show that $$l^1$$ with the norm deﬁned by $$\|(a_1,a_2,\dots )\|_\infty = sup_{k\in Z^+} \vert a_k\vert$$ is not a Banach space.

A: Think about the sequence $$a_i=(1,1/2,\dots,1/i,0,\dots)$$. $$\|a_i-a_j\|\to 0$$ but it don't converge in $$l^1$$.

# 6.D:

18 Suppose V is a normed vector space such that the dual space $$V'$$ is a separable Banach space. Prove that V is separable.

A: [So hard :<](https://math.stackexchange.com/questions/2388541/proving-that-a-banach-space-is-separable-if-its-dual-is-separable)


19 Prove that the dual of the Banach space $$C([0,1])$$ is not separable;here the norm on C([0,1]) is defined by $$\|f\| = sup_{[0,1]}\vert f \vert$$

A: $$X_{[0,s]}$$ is an uncountable collection of points whose distance with each other are lager than 1.

21 Suppose V is an infinite-dimensional normed vector space. Show that there is a convex subset U of V such that $$\bar{U} = V$$ and such that the complement V\U is also a convex subset of V with $$\bar{V\U} = V$$.

????A: Think about the kernel of discontinuous function in this normed vector space.

# 6.E:

6 Give an example of a metric space that is the countable union of closed subsets with empty interior.

A: Q.

9 Prove that there does not exist an inﬁnite-dimensional Banach space with a countable basis.

A: Note that the closure of span of finite basis has empty interior.

10 Give an example of a Banach space V, a normed vector space W, a bounded linear map T of V onto W, and an open subset G of V such that T(G) is not an open subset of W.

A: The identity map from $$l^{\infty}$$ to itself but with different norm.

## $$L^p$$ Space 

# 7.A

15 Show that there exists $$f \in L_2(R)$$ such that $$f \notin L_p(R)$$ for all $$p\neq 2$$.

A:[Pretty tricky, can be obtained by a little modification of this answer](https://math.stackexchange.com/questions/2476124/a-function-that-is-in-l2-but-not-in-lp-for-p-2)

# 7.B

2 (b) Prove that there does not exist a countable subset of $$l^\infty$$ whose closure equals $$l^\infty$$.

A: Think of the collection of all cartesian product of $$\{0,1\}$$.

4 Suppose (X,S,µ) is a σ-ﬁnite measure space and 1 ≤ p ≤ ∞. Prove that if f : X → F is an S-measurable function such that $$fh ∈ L^1(µ)$$ for every $$h∈L^{p'}(µ)$$, then $$f ∈L^p(µ)$$.


A: Since $$fX_{[-k,-k]}$$ in $$L^p$$, use the uniform boundedness principle to show that they are uniformly bounded. Then the monotone converge theorem tell us f in $$L^p$$.

Remark: The condition of $$\sigma$$-finite is necessary. 


## Time for 2, Hilbert Space

# 8.B

12 Give an example of a nonempty closed subset U of the Hilbert space $$l^2 and a∈ l^2$$ such that there does not exist b∈U with $$\|a−b\|$$ = distance(a,U).

A: Haven't found solution yet. Maybe the concrete example relating to some linear programming problem that can't attain optimal value.

# 8.C

15 Suppose V is an infinite-dimensional Hilbert space. Prove that there does not exist a translation invariant measure on the Borel subsets of V that assigns positive but finite measure to each open ball in V.

A: Find a open subset G s.t. Union of  $$G+e_k$$ are disjoint subsets of an open ball


## More measure

# 9.A

7 (a) Suppose B is the collection of Borel subsets of R. Show that the Banach space $$M_F(B)$$ is not separable. 

(b) Give an example of a measurable space (X,S) such that the Banach space $$M_F(S)$$ is infinite-dimensional and separable.

A:(a) Dirac measure

(b)$$l^\infty$$,$$\cup\{(a_1,a_2,\dots,a_i,0,\dots)\}$$


## Besides your operator is pretty compact 

# 10.B

4 Suppose E is a nonempty closed bounded subset of F. Show that there exists $$T ∈B(l^2)$$ such that sp(T) = E.

A: Note that every closed subset is closure of a countable set.

5 Give an example of a bounded operator T on a normed vector space such that for every α ∈F, the operator T−αI is not invertible.

A:$$l^\infty$$->$$l^\infty$$:$$(a_1,a_2,\dots,)$$->$$(a_1,a_2/2,\dots,)$$

7 Prove that if T is an operator on a Hilbert space V such that $$<Tf,g> = < f , Tg >$$for all f,g∈V, then T is a bounded operator.

A: [A corollary of uniform boundedness principle](https://math.stackexchange.com/questions/2602548/is-every-self-adjoint-operator-bounded)

# 10.D

2 Prove that if T is a self-adjoint operator on a nonzero Hilbert space V, then $$\|T\| = sup{\vert <Tf, f> \vert: f ∈ V and \|f\| = 1}.$$

A:$$T^2-\|T\|^2I=(T-\|T\|I)(T+\|T\|I)$$


5 Suppose T is a bounded operator on a nonseparable normed vector space V. Prove that T has a closed invariant subspace other than{0}and V. 


A: closure of $$\{T(f_1),T(f_2),\dots\}$$. $$T(f_k)$$ not in the closure of {...}

## The engineer's god : Fourier 

# 11.A

11 (d) Show that Fourier series of a continuous function on ∂D need not converge pointwise on ∂D. 

A: Because the dirichlet kernel is unbounded in $$L^1$$. Use uniform boundedness principle.

# 11.C

8 Suppose $$f ∈ L^1(R)$$ and $$n∈Z^+$$. Define g: R→C by $$g(x) = x^nf(x)$$. Prove that if $$g∈ L^1(R)$$, then $$\hat{f}$$ is n times continuously differentiable on R and $$(f^{(n)})^\wedge(t) = (−2πi)^n \hat{g}(t)$$ for all t∈R

A: With the condition of continuously differentiable, we can use the high order difference to conclude the results.

12 Suppose p ∈ [1,∞] and $$f ∈ L^p(R)$$. Prove that $$\mathcal{P}_y(\mathcal{P}_{y'}f) = \mathcal{P}_ {y+y'}f$$ for all $$y,y' > 0$$.

A: Use the brilliant idea that treat the $$\mathcal{P}_ {y'}\mathcal{P}_ y$$ as a measure whose norm equal 1, then use Holdier inequality to show the order of integrate can be change. 
	
13 Suppose p∈ [1,∞] and $$f ∈ L^p(R)$$. Prove that if 0 < y < y0, then $$\|\mathcal{P}_yf\|_ p ≥ \|\mathcal{P}_{y'} f\|_ p$$.

A: Treat $$\mathcal{P}_ y$$ as a functor and then use the conclusion of 12.

16 Suppose $$f ∈ L^1(R)$$ and $$\hat{f} ∈ L^1(R)$$. Prove that $$f ∈ L^2(R)$$ and $$\hat{f} ∈ L^2(R)$$.

A:Use the condition that f converge to 0 at infinity.

21 Prove that $$f,g∈ L^2(R)$$, then (fg)ˆ = (Ff)∗(Fg).

A:$$F(\mathcal{P}_{y}f \mathcal{P}_{y'}g)=F(\mathcal{P}_{y}f) * F(\mathcal{P}_{y'}g)$$

## Reference 

[The textbook : "Measure, Integration & Real Analysis"](http://measure.axler.net/)

