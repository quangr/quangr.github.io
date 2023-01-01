---
layout: post
title:  "Generalized function and bra-ket formalism"
date:   2020-04-13 12:55:14 +0800
categories: math
---

没想到广义函数与Dirac的bar-ket可能是我本科能学到的最近代的东西。Rigged Hilbert Space是1960年左右Gelfand搞出来的东西，而Dirac的bra-ket符号1947年就出来了。(吐槽一下这个名字)。这也说明了理论物理的发现与数学（或者说是数学的学习）并不一样。正如Hilbert所说，哥廷根路上的每一个学生（1924年朱德也在哥廷根。。。）都比Einstein懂四维几何，但还是Einstein第一个发现了相对论。

# Distribution

A distribution or a generalized function is a continuous linear functional in a test function space. Note that the Dirac function is not continuous in $$L^2$$. So we need a smaller test function space. The distribution space we need here is called tempered distributions. The space of tempered distributions is defined as the dual of the Schwartz space. 

# Rigged Hilbert space 

Let H be a Hilbert space, $$\Phi$$ be a dense subspace, $$\Phi^X$$ is the space of antilinear functional over $$\Phi$$, isomorphic to the space of distribution. Loosely speaking, a rigged Hilbert space is a triad of $$\Phi\subset H\subset \Phi^X$$.

# Bra-ket formalism

When we treat continuous spectrum, the foundation of bra-ket formalism is Rigged Hilbert space.
"Claiming that the RHS is the natural setting for Quantum Mechanics is about the same as claiming that, when the Hamiltonian has continuous spectrum, the natural setting for the solutions of the Schrodinger equation is the RHS rather than just the Hilbert space."

The Nuclear Spectral Theorem (Gelfand-Maurin) shows the powerfulness of Rigged Hilbert space. Instead of summation, we use integral to discompose a operator. For every self-adjoint operator A in $$\Phi$$, we extend it to a operator $$A^X$$ in $$\Phi^X$$. Then there exists a set of generalized eigenvectors s.t. $$A^X\vert\lambda>=\lambda\vert\lambda>$$, $$(\phi,\psi)=\int_\Lambda<\phi\vert\lambda><\lambda\vert\psi>d\mu(\lambda)$$, $$(\phi,f(A)\psi)=\int_\Lambda<\phi\vert\lambda><\lambda\vert\psi>f(\lambda)d\mu(\lambda)$$. So $$<\phi\vert\lambda>$$ is a function in on $$L^2(\Lambda,d\mu(\lambda))$$. We have a unitary $$U\phi=<\phi\vert\lambda>$$.

Now we can define $$U^XF$$ s.t. $$<U^XF\vert Uf>=<F\vert f>$$. Explicitly we have: $$U^X\hat{F}=UFU^{-1}$$ since $$UFU^{-1}<\lambda\vert f>=U(Ff)=<\lambda\vert Ff>=U^X\hat{F}<\lambda\vert f>$$. Moreover $$U^XA=UAU^{-1}=\lambda$$.


# Example 

$$\vec{x}f=xf$$. So $$\vec{x}\delta_{x_0}=x_0\delta_{x_0}$$.

$$\vec{p}f=-i\hbar\frac{\partial}{\partial x}f$$. So $$\vec{p}\int exp(ip_0x/\hbar)fdx=\int p_0exp(ip_0x/\hbar)fdx$$. $$\mu(p)=dp/2\pi$$.


$$< p \vert x>=-i\hbar\frac{\partial}{\partial p} $$.

# Reference

[特仑苏陶关于Distribution的文章](https://terrytao.wordpress.com/2009/04/19/245c-notes-3-distributions/)

[mit的关于Dirac函数的note](http://web.mit.edu/8.323/spring08/notes/ft1ln04-08-2up.pdf)

[一篇关于为什么要引进Rigged Hilbert Space的文章](https://arxiv.org/pdf/quant-ph/0502053.pdf)

[Generalized eigenvectors and the nuclear spectral theorem](https://link.springer.com/chapter/10.1007/3-540-51916-5_5#citeas)