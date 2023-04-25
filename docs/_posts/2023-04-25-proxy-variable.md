---
layout: post
title: Making Inferences with Proxy Variables
date: 2023-04-25 18:56 +0800
---

# single nondifferential error case

<!-- - what is nondifferential? -->

The process of identifying the probability of an outcome given a certain action, $p(y\mid do(x))$, is a difficult one. In this blog, we will explore how different constraints on proxy variables can lead to identifiability.

Some might expect to estimate $p(y\mid do(x))$ with $\sum p(y\mid x,w)p(w)$, where $w$ acts as a backdoor. However, I would say that this is only possible when $u$ and $w$ are identical.

In the absence of knowledge of the true $p(w\mid u)$, I have proven in the last section that $p(y\mid do(x))$ is unidentifiable. The idea is that we can always modify $P(y,U\mid x)$, $P(U\mid x)$, and $P(U)$ by a matrix A without changing the observed distribution $P(y,x,w)$. However, proving that $p(y\mid do(x))=\sum_j\frac{p(y,u_j\mid x)p(u_j)}{p(u_j\mid x)}$ is changable requires further thought.


Let's say we already kown $p(w\mid u)$ and everything is categorical. Let $W=(w_1,\dots,w_n)$ and $U=(u_1,\dots,u_k)$ where lower case denote scalar, uppercase for matric or vetor. We denote a matrix of conditional probabilities $p(w_i\mid u_j)$ as $P(W\mid U) = \left\{ P(W\mid u_1),\dots,P(W\mid u_k) \right\}$.

Given fixed x and y, We can write down equation 
$$\begin{aligned}
p(y,w_i\mid x)&=\sum_j p(y,w_i,u_j\mid x)=\sum_jp(y,w_i\mid x,u_j)p(u_j\mid x)\\
&=\sum_j p(y\mid x,u_j)p(w_i\mid x,u_j)p(u_j\mid x)\\
&=\sum_j p(y\mid x,u_j)p(u_j\mid x)p(w_i\mid u_j)\\
&=\sum_j p(y,u_j\mid x)p(w_i\mid u_j)
\end{aligned}$$
$$\global\def\ind{\mathrel{\perp\!\!\!\perp}} $$

From the equation above, we can see that since $\{y,x\} \ind w \mid  u$, the information provided to  $w$ through $x$ can be expressed in terms of $u$. 

In matrix form, $P(y,W\mid x)=P(y,U\mid x)P(W\mid U)$. If matrix $P(W\mid U)$ is invertiable, we can easily obtain $$P(y,U\mid x)=P(y,W\mid x)P^{-1}(W\mid U)$$

Similaily, from $p(w_i\mid x)=\sum_j p(w_i\mid u_j)p(u_j\mid x)$ and $p(w_i)=\sum_j p(u_j)p(w_i\mid u_j)$. We can obtain
$$P(U\mid x)=P(W\mid x)P^{-1}(W\mid U)\\P(U)=P(W)P^{-1}(W\mid U)$$

Knowing $p(U\mid x)$ and $p(U)$ and $p(y,U\mid x)$. we can easily obtain $p(y\mid do(x))=\sum_j\frac{p(y,u_j\mid x)p(u_j)}{p(u_j\mid x)}$.


In summary, given the matrix $P(W\mid U)$, we show  three linear constraints that involve the unknown mechanism $p(y,U\mid x),p(x\mid U),p(U)$ in term of linear system of $P(W\mid U)$. Note that the constant term in each constraint is observable(does not contain $U$).

$$\begin{aligned}
P(W\mid U)&P(y,U\mid x)&=&P(y,W\mid x)\\
P(W\mid U)&P(U\mid x)&=&P(W\mid x)\\
P(W\mid U)&P(U)&=&P(W)
\end{aligned}
$$

When $P(W\mid U)$ is not a square matrix, it becomes a linear system of $n$ equations in $k$ variables. If the number of categories in $W$ is smaller than that of $U$, it suggests that $W$ lacks the expressiveness to fully represent $U$. Consequently, the linear system will no longer have a unique solution, and unknown mechanism will become unidentifiable.

On the other hand, if the number of categories $n$ in $W$ is greater than the number of categories $k$ in $U$, the existence of a solution depends on the matrix and constant. However, in theory, we assume the data generating process and the data will guarantee a solution(as long as the matrix has full column rank). In real-life scenarios, when we can no longer justify the data generating process, this may result in no solution, leading to a conflict between the theory and the actual data.


[Kuroki, et al. (2014)](#Andrychowicz)

# Two independent proxy variables

What happens when we have two proxy variables? In the discrete case, if we have two proxy variables, Z and W, with category sizes n and m, respectively, we can represent them fully using a single variable with category size n * m. Thus, as discussed earlier, increasing the number of variables does not address the core challenge of an unknown error mechanism represented by P(Z,W\mid U). In the case where we have knowledge of the error mechanism, adding a second variable may not provide any additional benefits once m and n exceed k. However, if we introduce independent assumptions to constrain the structure of the joint probability, then the analysis becomes more interesting.


Given $Z\ind W \mid  U$, we can assume that $W\ind (Z,X) \mid  U$ and $Z\ind Y \mid  U$, although this is a weaker assumption than $Z\ind {W,X,Y}\mid U$ and $W\ind {Z,X,Y}\mid U$. Using this assumption, we can derive the following conditional probability distributions:
$$\begin{align*}
P(W\mid Z,x)&=P(W\mid U)P(U\mid Z,x)\\
P(y\mid Z,x)&=P(y\mid U,x)P(U\mid Z,x)
\end{align*}
$$
These equations can be directly derived from the information flow direction in the graph.

Now $$\begin{align*}
P(y\mid U,x)&=P(y\mid Z,x)P^{-1}(U\mid Z,x)\\
&=P(y\mid Z,x)P^{-1}(W\mid Z,x)P(W\mid U)
\end{align*}$$

Therefore, $p(y\mid do(x))=p(y\mid Z,x)P^{-1}(W\mid Z,x)P(W)$. However, $P(y\mid U,x)$ still depends on $P(W\mid U)$ and is generally unidentifiable. Here is a counterexample from Miaowang's supp material, as we have $P(y,W\mid Z,x)=P(y,W\mid U,x)P(U\mid Z,x)=P(y,W\mid U,x)AA^{-1}P(U\mid Z,x)$. Under certain conditions, we can substitute $P(y,W\mid U,x)$ with $P(y,W\mid U,x)A$.But the causal effect $p(y\mid do(x))$ is identifiable.

Can we weaken the independence assumption to conditional dependence? If we have any two variables W and Z with a weak regular condition, we can always write down $P(W\mid Z,U)$. The only constraint is that we observe $P(W\mid Z) = \sum P(W\mid Z,U)P(U)$. Under these conditions, how much flexibility do we have?


Maybe this not true in general. Given $P(Z),P(W\mid Z),P(Y,X\mid W,Z)$ fixed. $P(Y,X\mid W,Z)=P(Y,X\mid U)AA^{-1}P(U\mid W,Z)$, thus $P(Y,X\mid U)$ can always be replaced by $P(Y,X\mid U)A$. So does $P(Y\mid do(X))=P(Y,X\mid U)P(U)/P(X)$.But P(U) is changing with $P(U\mid W,Z)$


Trying linear normal case
Indenpendce means 1-rank


# Three mutually independent variables

Assuming three mutually independent variables, we can make $P(W\mid U)$ identifiable (up to label swapping) by knowing the size $k$ of $U_i$ and at least three independent proxies for the latent factor. This can be achieved through matrix factorizations.


# Proof of Nonidentification of $P(y\mid do(x))$ in Discrete Case

I have written this proof myself, and to the best of my knowledge, it is novel. If anyone finds any mistakes in the proof or knows of another proof, please let me know.


Given $x$, $y$, let $U$, and $W$ be n-category random variables. We shall prove that, for any given observation distributions $P(y,W\mid x)$, $P(W\mid x)$, and $P(W)$, there exist at least two different possible $p(y\mid do(x))$ outcomes.

**Claim 1** $P(y,w\mid x)$ and $P(w)$ can uniquely determine the observed distribution $P(w,x,y)$.

**Fact 2**: For any integer $n>1$, there exists a stochastic matrix $A$ with eigenvalues distributed as follows: $n-1$ of them equal to 1 and one equal to 0.9. 

**Proof**: Let$A=\begin{pmatrix}0.9&0.1\enspace0\enspace\dots\enspace0\\0^{\mathsf {T}}&E_{n-1}\end{pmatrix}$. Then, $A-I$ has rank 1, so $A$ has $n-1$ eigenvalues equal to 1. Furthermore, $tr(A)=0.9+n-1$, so $A$ has an eigenvalue of 0.9.

The outline of proof is: since we have 
$$\begin{aligned}
P(W\mid U)&P(y,U\mid x)&=&P(y,W\mid x)\\
P(W\mid U)&P(U\mid x)&=&P(W\mid x)\\
P(W\mid U)&P(U)&=&P(W)
\end{aligned}
$$
It is always possible to construct a data generation process where $P(W \mid U) = I$ and it will correspond to an outcome $p(y \mid do(x))$. If $P(W \mid U)$ is perturbed slightly (but remains a stochastic matrix), what will happen to $p(y \mid do(x))$? 

In the following text, it will be shown that when $P(W \mid U) = (1-\lambda)I + \lambda A$, there exists an $A$ such that $\frac{\partial p(y \mid do(x))}{\partial \lambda}\Bigr|_{\lambda = 0} \neq 0$, leading to a different $p(y \mid do(x))$.
Denote $A(\lambda)=(1-\lambda)I + \lambda A$

**Claim 3** If $P(y,w\mid x)>0$,$P(w\mid x)>0$ and $P(w)>0$, exist a region of $\lambda$ where $A^{-1}(\lambda)P(y,w\mid x)\ge0$, $A^{-1}(\lambda)P(w\mid x)\ge0$, $A^{-1}(\lambda)P(w)\ge0$, 


**Claim 4** Let $M=A^{-1}(\lambda)$,$\frac{\partial p(y\mid do(x))}{\partial M_{ij}}=\frac{p(y,w_i\mid x)p(u_j)+p(y,u_j\mid x)p(w_i)}{p(u_j\mid x)}-\frac{p(w_i\mid x)p(u_j)p(y,u_j\mid x)}{p^2(u_j\mid x)}$. It has rank at most 3, trace of 1

**Claim 5a**: $\frac{\partial p(y\mid do(x))}{\partial \lambda}=\sum_{ij}\frac{\partial p(y\mid do(x))}{\partial M_{ij}}\frac{\partial M_{ij}}{\partial \lambda}$. 

**Claim 5b**: $\frac{\partial M_{ij}}{\partial \lambda}=A^{-1}(\lambda)\frac{\partial A(\lambda)}{\partial \lambda}A^{-1}(\lambda)$. 

**Claim 5c**: $\frac{\partial M_{ij}}{\partial \lambda}\mid _{\lambda=0}=A-I$. 

**Claim 5d**: $\frac{\partial p(y\mid do(x))}{\partial \lambda}\mid _{\lambda=0}=tr(\frac{\partial p(y\mid do(x))}{\partial M}(A-I)^T)$

**Claim 6**: Since $tr(\frac{\partial p(y\mid do(x))}{\partial M})=1\neq 0$, there exists at least one stochastic matric A s.t. $tr(\frac{\partial p(y\mid do(x))}{\partial M}A^T)\neq tr(\frac{\partial p(y\mid do(x))}{\partial M})$. That is $\frac{\partial p(y\mid do(x))}{\partial \lambda}\mid _{\lambda=0}\neq 0$. 