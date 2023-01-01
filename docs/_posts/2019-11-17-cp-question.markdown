---
layout: post
title:  "a conditional probability question"
date:   2019-11-17 15:15:14 +0800
categories: math
---

Question:Let $$X_{(1)}=min(X_1,X_2)$$,$$X_{(2)}=max(X_1,X_2)$$,show that the conditional distribution of $$X_{(2)}$$ of given $$X_{(1)}$$ is determined by the Markov kernel $$(P_y)$$,where $$P_y(B)=\frac{\nu(B\cap(y,\infty))}{\nu(y,\infty)}$$.($$X_i$$ idd,and distribution $$\nu$$ has density f with respect to the Lebesgue measure.)

I intend to give a rigorous proof. The intuition is to involve $$\mathbf{1}_{X_1>X_2}$$ to simplify the calculation. $$P(X_{(1)}\in A,X_{(2)}\in B,X_1<X_2)=P(X_1\in A, X_2 \in B,X_1<X_2)=P(X_2\in A, X_1 \in B,X_1>X_2)=P(X_{(1)}\in A,X_{(2)}\in B,X_1>X_2)$$, which indicates that $$P(X_{(1)}\in A,X_{(2)}\in B)=2P(X_1\in A, X_2 \in B,X_1<X_2)=2\int\int\mathbf{1}_{x_1\in A,x_2\in B,x_1<x_2}f(x_1)f(x_2)dx_1dx_2$$. The integral can be write as $$\int_A\int\mathbf{1}_{x_2\in B,x_1<x_2}f(x_1)f(x_2)dx_2dx_1=\int_A\nu(B\cap (y,\infty))f(y)dy$$,so $$P(X_{(1)}\in A)=\int_A\nu(y,\infty)f(y)dy$$. Now let's verify the $$P_y(B)$$.

1.Obviously, $$P_y(B)$$ is a probability measure for any given y

2.$$P_y(B)$$ for given B is $$\mathbf{B}$$-measurable function, and $$X_{(1)}$$ has a density. $$\int_A P_y(B) dX_{(1)}(P)=\int_A P_y(B)\nu(y,\infty)f(y)dy=\int_A \nu(B\cap(y,\infty) f(y)dy=P(X_{(1)}\in A,X_{(2)}\in B)$$