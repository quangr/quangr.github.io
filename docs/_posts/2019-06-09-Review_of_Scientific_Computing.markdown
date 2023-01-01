---
layout: post
title:  "Review of Scientific Computing"
date:   2019-06-09 18:55:14 +0800
categories: math
---
1.The continuity of the $$\xi$$ in the error estimation

If$$f(x)\in C^2_{[a,b]}$$. When we use a linear function to replace it, the error function can be write as$$R(x)=f(x)-P(x)=\frac{f''(\xi)}{2}(x-x_0)(x-x_1)$$. And $$f''(\xi)$$ is a continuous function of x, for it can be written as $$\frac{f(x)-P(x)}{(x-x_0)(x-x_1)}$$.Due to this property, we can take the f'' out of integral to estimate the error function of Trapezoidal rule.


2.Legendre Polynomial

1.$$\int_{-1}^{1} P_{m}(x) P_{n}(x) d x=0 \quad \text { if } n \neq m$$ and $$\int_{-1}^{1} \mathrm{P}_{n}^{2} \mathrm{d} x=\frac{2}{2 n+1}$$
    Proof: Use the integration by parts.

2.$$(n+1) \mathrm{P}_{n+1}-(2 n+1) x \mathrm{P}_{n}+n \mathrm{P}_{n-1}=0$$
    Proof: Use the generating function $$G(x, t)=\frac{1}{\sqrt{1-2 x t+t^{2}}}=\sum_{n=0}^{\infty} t^{n} \mathrm{P}_{n}(x)$$

3.Diagonally dominant matrix

A strictly diagonally dominant matrix is non-singular. To prove this we can use the Gershgorin circle theorem to show that these circles don't contain the zero. 


4.Discrete Orthogonal Polynomialson Equidistant Nodes

Write it with the matirx form, and article "Vandermonde matrices on integer nodes: the rectangular case" give a magic LU factors of a Vandermonde matrix.(COMPLICATED!)

