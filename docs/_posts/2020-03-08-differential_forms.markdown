---
layout: post
title:  "Integration of Differential Forms"
date:   2020-03-08 21:55:14 +0800
categories: math
---

标题取自baby rudin第十章，说实话一开始只想看看换元公式的证明的，结果把这章看了一遍，就当学一遍矢量分析了吧。说实话在处理这些性质足够好的函数的时候lebesgue积分好像没多大用。。。


## Change of variable

Suppose T is a $$C^1$$ bijection from an open set E to $$R^k$$ s.t. $$J_T(x)\neq0$$. If f is a continuous function whose support is compact and lies in $$T(E)$$, then we have $$\int_{R^k}f(y)dy=\int_{R^k}f(T(x))\vert J_T(x)\vert dx$$

Outline of Proof: First we need to show that for any x in E, f can be write as a composition of permutation and primitive function in a neighbor of x. Note that both permutation operator and primitive composition satisfy the change of variable formula. Then we need a collection of unit partition functions on E to "write f as a sum of continuous functions with small supports". 

Remark: For a more 'real analysis' version of proof, see [this proof](https://actamath.savbb.sk/pdf/acta1906.pdf)

## Differential Forms

# Definition

k-surface: A k-surface in an open set $$E\subset R^m$$ is a $$C^1$$ map from a compact set $$D\subset R^k$$ to E. e.g. $$I_k:[0,1]^k;Q_k:\{x:\sum x_i\leq 1;0\leq x_i\}$$(identity map)

k-forms: A k-forms(or tuple $$(\omega_i,dX_{I_i})$$) is a map from k-surface $$\Phi$$ to $$\sum\int\omega_i(\Phi)\vert J_\Phi\vert dX_{I_i}$$

We can define addition and multiplication of k-form. $$w_1dX_{I_1}\wedge w_2dX_{I_2}:=w_1w_2dX_{I_1}\wedge dX_{I_2}$$

Simplexes: A affine simplexes is a affine map from $$Q^k$$ to $$R^k$$ with vertices $$\{p_0,\dots,p_k\}$$.(denote by $$[p_0,\dots,p_k]$$) Obvious it's a k-form, moreover it can be oriented if not degenerate. It's positive oriented if the determinate of transform matrix is positive.

Boundary: $$\partial\sigma=\sum (-1)^i[p_0,\dots,\bar{p_i},\dots,p_k]$$

Now we can define a k-surface that can be oriented: $$T\circ\sigma$$. We can divide lots of surface into sum of this form(Triangulation).
# Operator

$$d(\omega dX_I):=\sum D_i\omega dx_i\wedge dx_I$$

$$\omega_T=\omega(T(u_i))dt_{i_1}\wedge\dots\wedge dt_{i_n}=\omega(T(u))J_Td_{u_1}\wedge\dots\wedge d_{u_n}$$ (it's a linear transform for a fixed point)

$$(\omega_T)_S=\omega_{TS}$$

$$d(\omega_1\wedge \omega_2)=d(\omega_1)\wedge \omega_2+(-1)^{k_1}\omega_1\wedge d(\omega_2)$$

# Stokes' Theorem

$$\int_\Phi d\omega=\int_{\partial\Phi} \omega$$


Proof: Only need to prove the case when $$\Phi$$ is affine simplexes. Moreover, we can assume $$\Phi=\sigma_0=[0,e_1,\dots,e_k]$$,$$\omega=\omega dx_1\wedge\dots dx_{r-1}\wedge dx_{r+1} \wedge dx_k$$. The term in $$\partial\Phi$$ are all zero except $$\sigma_1=[e_1,\dots,e_k]=(-1)^{r-1}[e_r,e_1,\dots,e_k]$$ and $$\sigma_2=(-1)^{r}[0,e_1,\dots,e_{r-1},e_{r+1},\dots,e_k]$$. So the right hand equals $$\int\omega(\sigma_1) du_I + \omega(\sigma_2) du_I$$. The left hand equal $$\int_0^{1-\sigma u_i} (-1)^r D_r\omega(\sigma_0)dV$$, evaluate integral with $$x_r$$ and then the proof complete.


## Vector Analysis in $$R^2$$ and $$R^3$$

gradient:$$\nabla u=(D_1u)e_1+(D_2u)e_2+(D_3u)e_3$$

curl:$$\nabla \times F=(D_2F_3-D_3F_2)e_1+(D_3F_1-D_1F_3)e_2+(D_1F_2-D_2F_1)e_3$$

divergence:$$\nabla\cdot F=D_1F_1+D_2F_2+D_3F_3$$

In fact, let $$\lambda_F=F_1dx+F_2dy+F_3dz$$,$$\omega_F=F_1dy \wedge dz+F_2dz \wedge dx+F_3dx \wedge dy$$. We have following conclusion:

$$F=\nabla u \iff \lambda_F=du$$

$$\nabla \times u=0 \iff d\lambda_F=0$$

$$F=\nabla \times G \iff \omega_F=d\lambda_G$$

$$\nabla\cdot F=0 \iff d\omega_F=0$$

unit normal: $$N(u,v)=\frac{\partial(y,z)}{\partial(u,v)}e_1+\frac{\partial(z,x)}{\partial(u,v)}e_2+\frac{\partial(x,y)}{\partial(u,v)}e_3$$. It's the Cross product of two tangent vector. We define $$\int_\Phi fdA:=\int_Df(\Phi(u,v))\vert N(u,v)\vert du dv$$.

Integration in $$R^3$$: For 1-forms, define t to be the unit vector in the direction of $$\gamma'(u)$$. We have $$\int_\gamma\lambda_F=\int_0^1F(\gamma(u))\cdot t(u)\vert\gamma'(u)\vert du$$. We shall denote $$\vert\gamma'(u)\vert du$$ as ds.

For 2-forms, we have $$\int_\Phi\omega_F=\int_DF(\Phi(u,v))\cdot N(u,v)du dv=\int_\Phi (F\cdot n)dA$$

Original form of Stokes' theorem: $$\int_\Phi(\nabla\times F)\cdot ndA=\int_{\partial\Phi}(F\cdot t)ds$$.

The divergence theorem: $$\int_\Omega(\nabla\cdot F)dV=\int_{\partial\Omega}(F\cdot n)dA$$

Moreover, we can use Stokes' Theorem to find a invariant for every homotopy curve in $$R^k-\{0\}$$. e.g. winding number

Let $$F=g\nabla h$$, we have $$\nabla\cdot F=g\nabla^2h+(\nabla g)\cdot(\nabla h)$$. So by the Stokes' theorem, we have$$\int_\Omega[g\nabla^2h+(\nabla g)\cdot(\nabla h)]=\int_{\partial\Omega}g\frac{\partial h}{\partial n}dA$$. Interchange g and h, we obtain Green's identities:
$$\int_\Omega[g\nabla^2h-h\nabla^2g]=\int_{\partial\Omega}g\frac{\partial h}{\partial n}-h\frac{\partial g}{\partial n}dA$$

Some definition of curl and divergence involve limit of integration. We can prove the equivalence of these two definitions by [Lebesgue differentiation theorem in high dimensions](https://terrytao.wordpress.com/2010/10/16/245a-notes-5-differentiation-theorems/).