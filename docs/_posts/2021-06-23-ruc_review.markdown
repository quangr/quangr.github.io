---
layout: post
title:  "人大面试回忆"
date:   2021-06-25 13:54:21 +0800
categories: math
---

== 随机过程 ==

=== 问题叙述 ===

假设$$X_n$$是可数状态空间S上的不可约、非周期、正常反的马尔科夫链$$(\mu,P)$$。试证明该马尔科夫链存在唯一的稳定分布$$\pi$$，并且$$P^n(i,j)\to\pi_j$$（Kolmogorov 极限定理）

===引理1：非周期性的等价条件===

不可约和非周期性意味着对任意x,y存在N，使得$$n\geq N$$有$$P^n(x,y)>0$$。



证明： 因为P不可约，所以存在k使得$$P^k(x,y)>0$$。下面定义集合$$E_i=\{n\vert 0\leq n<k,P^{ik+n}(x,y)>0\}$$

由于$$P^n(x,y)>0$$蕴含$$P^{n+k}(x,y)>0$$。我们有$$E_1\subset E_2\subset E_3\subset\dots$$

即$$E_i$$为单调升链。但$$E_i\subset Z_k$$为有限集，所以存在n使得$$E_n=E_{n+1}=E_{n+2}=\dots$$。令$$E=\cup_i E_i$$。有$$E\subset Z_k$$

下证E为加法子群,若$$x,y\in E$$，存在$$E_n$$使得$$x,y\in E_n$$，这样$$P(2nk+x+y)(x,y)>0$$，即$$x+y\in E_{2n}$$或$$x+y\in E_{2n+1}$$。（这里的加法是$$Z_k$$中的加法）。既然E为$$Z_k$$的加法子群，E有生成元$$x\geq 1$$。但如果$$x\neq 1$$，又有$$x\vert k$$，所以x是一个周期，这与非周期性矛盾，所以x=1。由上面的论证知存在N,使得对$$n\geq N$$，$$E_n=Z_k$$。

===稳定分布的存在性===

任取状态x,定义停时$$T=\inf\{n\geq1:X_n=x\}$$。因为x正常反，所以$$E(T)<\infty$$。$$\pi_y=E_x(\sum\limits_{n=0}^{T-1}1_{X_n=y})$$。定义$$\bar{p}_n(y)=P_x(X_n=y,T>n)$$。我们有$$\pi_y=\sum\limits_{n=1}^\infty\bar{p}_n(y)$$。下面证明$$\pi P=\pi$$。

若$$z\neq x$$
$$(\pi P)_z=\sum\limits_y\pi_yP(y,z)=\sum\limits_{n=0}^\infty\sum\limits_y\bar{p}_n(y)P(y,z)=\sum\limits_{n=0}^\infty P(T>n+1,X_{n+1}=z)=\pi_z$$。

否则
$$(\pi P)_x=\sum\limits_y\pi_yP(y,x)=\sum\limits_{n=0}^\infty\sum\limits_y\bar{p}_n(y)P(y,x)=\sum\limits_{n=0}^\infty P(T=n+1)=1=\pi_x$$。

又有$$\sum\limits_{y\in S}\pi_y=E(T)<\infty$$。所以$$\pi$$可以归一化，即为稳定分布。

===引理2：稳定分布与常反的关系===
不可约马尔可夫链存在稳定分布$$\pi$$意味着常反。

任取$$\pi(y)>0$$，$$\sum\limits_x\pi(x)\sum\limits_{n=1}^\infty P^n(x,y)=\sum\limits_{n}\pi(y)=\infty$$。所以y常反。

反之，如果y常反，对应的$$\pi(y)>0$$。

===稳定分布的唯一性===

已知存在稳定分布$$\pi$$，假设存在另一个稳定分布$$\mu$$。定义转移概率矩阵$$Q(x,y)=P(y,x)\frac{\pi(y)}{\pi(x)}$$

由引理2知Q良定义，容易验证这是一个转移矩阵,且有$$Q^n(x,y)=\pi(y)P^n(y,x)/\pi_x$$。所以Q也不可约并常反。

令$$Y_n$$为转移矩阵为Q的马尔科夫链，$$F_n=\sigma(Y_1,Y_2,\dots,Y_n)$$。令函数$$F:S\rightarrow R$$为$$F(i)=\frac{\mu_i}{\pi_i}$$

由正常反和不可约性知$$\pi_i>0$$从而F良定义。$$F(Y_n)$$在$$F_n$$下成为鞅，因为$$E(F(Y_{n+1})\vert F_n)=E(F(Y_{n+1})\vert Y_n)=\sum_x Q(Y_n,x)F(x)=\frac{\mu_{Y_n}}{\pi_{Y_n}}=F(Y_n)$$

因为F有界，由鞅的收敛定义知$$F(Y_n)$$几乎处处收敛，但$$Y_n$$常反，所以$$F$$必为常数。即F=1。

===主定理证明===



设$$\pi$$为稳定分布，令X为马尔科夫链$$(\mu,P)$$，Y为马尔科夫链$$(\pi,P)$$。容易验证$$Z_n=(X_n,Y_n)$$是状态空间$$X\otimes Y$$上的马尔科夫链，转移概率为$$\bar{P}=P\otimes P$$，初始分布为$$\mu\otimes \pi$$。

下证$$Z_n$$不可约、非周期、正常反。由P的非周期性知，对任意$$x_1,y_1,x_2,y_2$$，存在N使得对$$n>N$$，$$\bar{P}^n((x_1,y_1),(x_2,y_2))=P^n(x_1,y_1)P^n(x_2,y_2)>0$$。并且$$\bar{P}$$存在稳定分布$$\pi\otimes \pi$$。所以$$\bar{P}$$常反，所以对任意状态x，停时$$T=inf\{Z_n=(x,x)\}$$有限。


下证$$P(X_n=x,T\leq n)=P(Y_n=x,T\leq n)$$。(即相遇后$$X_n,Y_n$$分布相同)


$$\begin{aligned}
P(X_n=x,T\leq n)&=\sum\limits_{m\leq n}P(X_n=x,T=m,X_m=x)=\sum\limits_{m\leq n}P(X_n=x\vert X_m=x)P(X_m=x,T=m)\\
&=\sum\limits_{m\leq n}P(Y_n=x\vert Y_m=x)P(Y_m=x,T=m)=P(Y_n=x,T\leq n)\end{aligned}$$

从而

$$\begin{aligned}
\vert P(X_n=x)-P(Y_n=x)\vert &=\vert P(X_n=x,T\leq n)+P(X_n=x,T>n)+P(Y_n=x,T\leq n)+P(X_n=x,T>n)\vert \\
&\leq\vert P(Y_n=x,T\leq n)+P(X_n=x,T>n)\vert \leq P(T>n)

\end{aligned}$$


令$$\mu=\delta_y$$，n趋于无穷大即可。

===有限情况的其他证明===

对有限状态马尔可夫链，有如下性质

$$\begin{matrix}
  \text{存在稳定分布}  &  &   \text{稳定分布唯一}  &             & P^n\text{收敛} \\
               \Uparrow{\text{Brouwer不动点定理}}         &                                          &     \Uparrow{\text{常反}}                  &             &\Uparrow{\text{Banach不动点定理}} \\
  \text{一般概率矩阵}      &            \Rightarrow           &  \text{不可约}                & \Rightarrow & \text{非周期}
  \end{matrix}$$


在状态空间S有限情况下我们的证明会方便很多，主要原因是S上的概率测度空间$$\mathcal{PM}(S)$$是$$R^n$$一个有界闭集，从而是一个紧集。从不动点的角度来看，是一个凸闭集。我们有一系列定理来对S上的线性映射进行刻画。

因为状态空间有限，我们可以把条件放松到不可约非周期。因为有限空间上必有一个状态常反，从而由不可约性得所有状态常反。不可能所有状态零常反，所以必有一个状态正常反，从而所有状态正常反。

由Brouwer不动点定理知P有稳定分布。（对P没有任何要求！）。如果再有不可约性，由上面的鞅方法得到唯一性。

如果再加上非周期性，$$\mathcal{PM}(S)$$是Banach空间的事实让我们可以用Banach不动点定理来直接得到不动点。

P的不可约和非周期性使得我们可以取$$N_{i,j}$$，使得对$$n>N_{i,j}$$有$$P^n(i,j)>0$$。取$$N=max(N_{i,j})$$。那么$$P^N$$的所有元素大于0。取其元素最小值$$\epsilon>0$$。现在我们证明$$P^N$$是一个压缩映射：

设$$\sum x_i =0 $$

$$\|xP^N\|_1=\vert \sum\limits_{i,j}x_iP^N(i,j)\vert =\vert \sum\limits_{i,j}x_i(P^N(i,j)-\epsilon)\vert \leq\sum\limits_{i,j}\vert x_i\vert \vert P^N(i,j)-\epsilon\vert =(1-\epsilon)\sum\limits_{i,j}\vert x_i\vert =\|x\|$$。

这样对$$x,y\in M(S)$$,$$\sum(x_i-y_i)=0$$。从而$$\|(x-y)P^N\|_1\leq\|x-y\|_1$$

由Banach不动点定理知$$P^N$$存在唯一不动点，记为$$\pi$$。并且对任意$$x\in m(S)$$，有$$xP^{nN}\to\pi$$。 所以对$$x,xP,\dots,xP^{N-1}$$有$$xP^{i+n(N-1)}$$收敛到稳定分布。这意味着$$xP^n\to \pi$$。 更有$$\pi P=\lim\limits_{n\to\infty}\pi P^nP=\lim\limits_{n\to\infty}\pi P^{n+1}=\pi$$。即$$\pi$$为稳定分布。

== 概率论 ==

=== 问题叙述 ===

假设$$X_i$$为独立同分布变量，$$E\vert X_1\vert <\infty$$,令$$S_n=\sum\limits_1^n X_i$$。则$$S_n/n\to EX_1 \,$$，收敛是$$L^1$$和几乎必然(a.s.)的。(强大数定理)



===引理===

对$$n\geq 0$$,定义$$F_{-n}=\sigma(S_n,S_{n+1},\dots)=\sigma(S_n,X_{n+1},X_{n+2},\dots)$$

有$$F_{-1}\supset F_{-2}\supset\dots$$. 

我们下面证明$$E(X_i\vert F_{-n})=E(X_j\vert F_{-n})$$

对$$1\leq i\neq j\leq n$$.由于$$X_i$$与$$F_{-n-1}$$独立。

$$E(X_i\vert F_{-n})=E(X_i\vert S_n)$$. 

只需证明对每个$$E\in\sigma(S_n)$$，有

$$\int_E X_i dP=\int_E X_j dP$$

$$E=S^{-1}(B)$$,B为R中的Borel集。因为$$S_n=F(X_1,X_2,\dots,X_n)$$。对应的有$$R^n$$中的Borel集C使得

$$E=\{(X_1,X_2..X_n)\in C\}$$

注意到若$$(x_1,..x_i,..x_j,..x_n)\in C$$,则$$(x_1,..x_j,..x_i,..x_n)\in C$$.即

$$\int_C X_i dP_{X_1..X_n}=\int_C X_j dP_{X_1..X_j..X_i..X_n}$$

由$$X_i$$独立同分布知$$P_{X_1..X_i..X_j..X_n}$$与$$P_{X_1..X_j..X_i..X_n}$$分布相同。所以$$\int_E X_i dP=\int_C X_i dP_{X_1..X_n}=\int_E X_j dP$$.


推论:$$E(X_1\vert F_{-n})=\frac{S_n}{n}$$


证明：$$nE(X_1\vert F_{-n})=\sum\limits_i E(X_i\vert F_{-n})=E(S_n\vert F_{-n})=S_n$$.

===主定理证明===


令$$Y_{-n}=E(X_1\vert F_{-n})$$.

由$$E(Y_{-n}\vert F_{-n-1})=E(X_1\vert F_{-n-1})=Y_{-n-1}$$知$$Y_n$$是鞅($$n<0$$)。

由Doob不等式知对任意N，$$Y_n$$在[-N,1]内跨越[a,b]的次数几乎处处有界。对(a,b)取遍所有有理数对知$$Y_n$$几乎处处收敛。令

$$Y=\lim\limits_{n\to-\infty} Y_n$$

并且由Fatous引理知$$E(Y^+)\leq\underline\lim\limits_{n\to-\infty} E((Y_n)^+)\leq E(\vert X_1\vert )$$(最后一步是因为$$f(x)=x^+$$是凸的),对$$Y^-$$做同样处理可知Y是$$L^1$$的。

在测度有限的情况下几乎处处收敛蕴含依测度收敛，所以$$Y_n$$在依测度收敛下是Cauthy列。

因为$$E\vert X_1\vert <\infty$$。所以存在M使得$$E(\vert X_1-X_11_{\vert X_1\vert \leq M}\vert )<\epsilon$$

令$$Z_n=E(X_11_{X_1<M}\vert F_n)<M$$

有$$\|Z_n-Y_n\|_1\leq E\vert X_1-X_11_{\vert X_1\vert \leq M}\vert <\epsilon$$

这样$$\|Y_n-Y_m\|_1\leq\|Y_n-Z_n\|_1+\|Y_m-Z_m\|_1+\|Z_n-Z_m\|_1$$.

又因为$$Z_n$$有界且依测度收敛,存在N使得当$$n,m>N$$时

$$\|Z_n-Z_m\|_1<2MP(\vert Z_n-Z_m\vert >\epsilon)+\epsilon<3\epsilon$$

我们证明了$$Y_n$$是$$L^1$$中的Cauthy列。这样每个$$Y_{n_k}$$存在子列收敛，又上面知$$Y_n\to Y$$.所以$$Y_n$$$$L^1$$收敛到Y。

$$\{Y<\alpha\}=\overline\lim\limits_{n\to-\infty}\{Y_n<\alpha\}$$是$$\cap_{n=1}^\infty \sigma(\cup_{k=n}^\infty F_n)$$可测的。但又因为Kolmogorov 0-1律指出，所有tail-event的概率只能为0或1，所以Y几乎处处为常数。

由$$Y_n$$$$L^1$$收敛到Y知$$\vert \int_\Omega X_1 dP-\int_\Omega Y dP\vert =\vert \int_\Omega Y_n dP-\int_\Omega Y dP\vert \leq\int \vert Y_n-Y\vert dP<\epsilon$$

对任何$$\epsilon>0$$成立.所以$$Y=EX_1$$ a.s.

== 实变函数 ==
=== 问题叙述 ===

假设测度空间$$(X,\Sigma)$$上有两个有限正测度$$\mu,\nu$$，满足$$\nu\ll\mu$$。那么存在一个$$f\in L^1(\nu)$$，对所有的$$\Sigma$$-可测集E满足：


$$\nu(E) = \int_E f \, d\mu$$（Radon-Nikondym 定理）


===测度论角度的证明===

定义集合

:$$\mathcal{G}=\{g:\;g\geq0; \int_E g \, d\mu \leq \nu(E),  \;\forall E\in \Sigma\}$$.

注意到$$\mathcal{G}$$对取最大值封闭，即若$$f,g\in\mathcal{G},max(f,g)\in\mathcal{G}$$。这是因为令$$A=\{f>g\}$$,$$B=\{f\leq g\}$$. $$\int_E max(f,g) \, d\mu=\int_{E\cap A} f \, d\mu+\int_{E\cap B} g \, d\mu\leq \nu(E\cap A)+\nu(E\cap B)=\nu(E)$$.

现在取$$\alpha= \sup\{\int_X f \, d\mu, f\in\mathcal{G}\}\leq \nu(X)\leq \infty$$。取一列函数$$f_n$$使得$$\alpha\geq\int_X f_n \, d\mu>\alpha-\frac{1}{n}$$。因为$$\mathcal{G}$$对取最大值封闭，$$\max\limits_{i\leq n}(f_i)\in\mathcal{G}$$，这列函数列可以取成单增的。现在令$$f=\lim\limits_n f_n$$，根据单调收敛定理

:$$\int_X f \, d\mu=lim\int_X f_n \, d\mu=\alpha$$.


下面证明对所有可测集E，f满足

:$$\mu(E) = \int_E f \, \, d\mu$$

由f为$$f_n$$的极限知$$\int_E f \, d\mu=\lim \int_E f_n \, d\mu\leq \nu(E)$$。 只需证明$$\int_E f \, d\mu\geq\nu(E)$$。

令

:$$\nu_r(E)=\int_Ef\, d\mu$$

:$$\nu_s=\nu-\nu_r$$

由上述论论证知它们都是正测度。对任意$$\epsilon>0$$，存在$$\nu_s-\epsilon\mu$$的Hahn分解。即存在$$A_\epsilon,B_\epsilon$$使得：$$A_\epsilon\cap B_\epsilon=\emptyset$$，$$A_\epsilon$$的任何可测子集在$$\nu-\epsilon\mu$$上非负,$$B_\epsilon$$的任何可测子集在$$\nu-\epsilon\mu$$上非正。

于是$$\int_E f+\epsilon 1_{A_\epsilon}\, d\mu = \nu_r(E)+\epsilon\nu_s(A_\epsilon\cap E)\leq \nu_r(E)+\nu_s(E)=\nu(E)$$对任意可测集E成立。所以$$f+\epsilon 1_{A_\epsilon}\in \mathcal{G}$$。这说明$$\mu(A_\epsilon)=0$$。否则与$$\int_X f \, d\mu=\alpha$$矛盾。令$$A=\cup_{n=1}^\infty A_{\frac 1 n}$$。 知$$\mu(A)=0$$。 由A的定义知若$$E\cap A=\emptyset$$， 对任何k有

:$$(\nu_s-k\mu)(E)\leq0$$


假设存在可测集E使得$$\nu_r(E) < \nu(E)$$。 这样$$\nu(E)>0$$。由绝对连续性知$$\mu(E)>0$$。从而$$F=E\cap A^C\neq\emptyset$$。由$$\mu(E/F)=0$$知:$$\nu(E/F)=0$$，所以$$\nu(F)=\nu(E)>0$$。但存在$$k$$，使得$$(\nu_s-\frac1k)(F)>0$$。矛盾！即对任意可测集E有$$\mu(E) = \int_E f \, \, d\mu$$。

===利用Riesz表示定理的证明===

上面的证明只使用了一些测度分解中的手法，略显冗长。如果使用$$L^2$$空间上的Riesz表示定理可以给出一个短的多的证明：

令$$\lambda=\mu+\nu$$,对$$g\in L^2(\lambda)$$,定义两个线性泛函：

:$$E_\mu(g)=\int g \, d\mu$$

:$$E_\nu(g)=\int g \, d\nu$$

由Cauthy不等式知$$\vert E_\mu(g)\vert \leq\vert E_\mu(\vert g\vert )\vert \leq(\int g^2 \, d\mu)^{1/2}\leq\|g\|_2$$。从而这两个泛函都良定义，并且都是有界泛函。

由Riesz表示定理知，存在$$h_1,h_2$$使得

:$$E_\mu(g)=\int gh_1 \, d\lambda$$

:$$E_\nu(g)=\int gh_2 \, d\lambda$$

令$$g=1_E$$，可知$$h_1,h_2$$几乎处处非负，并且都是$$L^1$$可积的。注意到$$\mu(E)=0$$当且仅当$$\lambda(E)=0$$.所以$$h_1$$是几乎处处正的。（这里都是指对$$\lambda$$测度）

定义$$f=h_2/h_1$$.可以看到f是对$$\lambda$$测度良定义,从而是对$$\mu$$测度良定义的。所以$$\nu(E)=E_\nu(1_E)=\int_E h_2 \, d\lambda=\int_E f h_1 \, d\lambda$$。由于f几乎处处非负，由单调收敛定理知$$\int_E f h_1 \, d\lambda=\lim\limits_n\int_E f 1_{f\leq n} h_1 \, d\lambda=\lim\limits_n\int_E f1_{f\leq n} \, d\mu=\int_E f \, d\mu$$.

====注记====
利用Hilbert空间是冯诺依曼的想法，不过他的证明和这个证明是不同的。将f写成两个函数的商能使我们直观看到为什么也有人将f写成$$\frac{d\nu}{d\mu}$$
