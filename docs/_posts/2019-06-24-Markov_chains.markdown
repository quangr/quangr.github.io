---
layout: post
title:  "Markov Chains"
date:   2019-06-24 22:15:14 +0800
categories: math
---
Edited at 2020/6/29


## Discrete Markov Chains


# Definition

Let T=N. A stochastic process $$X_T$$ is a Markov chains $$(\lambda,P)$$ if:

$$P(X_{n+1}=i_{n+1}\vert X_{n}=i_{n},\dots,X_{0}=i_{0})=P_{i_{n+1}i_{n}}$$ and $$P(X_0=i_0)=\lambda_0$$.

Remark: Easy to check this definition is equivalent to $$P(X_{n+1}=i_{n+1},X_{n}=i_{n},\dots,X_{0}=i_{0})=P_{i_{n+1}i_{n}}P_{i_{n}i_{n-1}}\dots P_{i_{1}i_{0}}\lambda_{i_0}$$


# Markov Property

Condition on $$X_m=i_m$$, $$\{X_{m+n}\}$$ is a $$(\sigma_{i_m},P)$$ Markov chains and indepedent with $$X_0,X_1,\dots,X_{m-1}$$.

# Communicting Class 


For the purpose of further analysis, we need to partition state form. We say $x\to y$ if $$\{n:p^n_{ji}\}\neq \emptyset$$ and define a equivalence relationship $$i ~ j$$ if $$i\to j,j\to i$$.

We say a class C is closed if $$i\in C,i \to j\implies j\in C$$. 'Closed' means states can't escape from it. Sometimes it's convinient to treat a closed class as a absorbed point.

We define hitting time for a closed state: $$H^A=inf \{n\geq0:X_n(\omega)\in A\}$$ and $$h_i^A=P_i(H^A<\inf)$$.($$P_i$$ means $$\lambda=\delta_i$$).

By the Markov property, we have following theorem:

$$h_i^A$$ satisfies: $$h^A_i=\begin{cases} h_i^A &i\in A \\\sum_jp_{ij}h^A_j &i\not\in A \end{cases}$$. Moreever $$h_i^A$$ is the minimal non-negative solution to this linear system. (The minimal implies uniqueness).

Similarly $$k_i^A=E_i(H^A)$$ satisfies: $$k^A_i=\begin{cases} 0 &i\in A \\1+\sum_jp_{ij}k_j &i\not\in A \end{cases}$$. Moreever $$k_i$$ is the minimal non-negative solution to this linear system. 

# 

$$V_i=\sum_1^{\infty}1_{\{X_n=i\}}$$ and $$r_i^k=E_k\sum_1^{T_k}1_{\{X_n=i\}}$$

$$P(V_i\geq r)=\sum_{0}^{\infty}P(\sum_{n}^{\infty}1_{\{X_n=i\}}\geq r-1\mid T_i=n)P(T_i=n)=P(V_i\geq r-1)P(T_i<+\infty)$$. With $$P(V_i\geq 0)=1$$ we find out $$P(V_i\geq r)=P(T_i<+\infty)^r$$.

Take expected value of $$V_i$$, $$\sum p_{ii}^n=E(V_i)=\sum_1^{\infty}P(V_i>n)$$. So the if one of these two summation converge or diverge at same time, which allows us to tell the recurrence from $$P^n$$.

The second r.v. actually define a invarient measure for a irreducible and recurrent markov chain P. Because the summation of expected value of $$r_i^k(i \in I)$$ is the mean recurrence time, if P is postive recurrent than we can transform it to a invarient distribution. 
