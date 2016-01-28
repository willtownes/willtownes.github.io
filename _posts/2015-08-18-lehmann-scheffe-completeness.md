---
title: Why does Lehmann-Scheffe Theorem need Completeness?
layout: post
external: [latex]
comments: true
---

The [Lehmann-Scheffe theorem](https://en.wikipedia.org/wiki/Lehmann%E2%80%93Scheff%C3%A9_theorem) says that if we have an unbiased estimator $\newcommand{\E}{\mathrm{E}}
\newcommand{\Var}{\mathrm{Var}}
\newcommand{\Cov}{\mathrm{Cov}} Z$
and a complete sufficient statistic $T$, then the estimator $\phi(T) = \E[Z\vert T]$ is a uniform minimum variance unbiased estimator (UMVUE). In most sane scenarios, complete sufficient statistics are minimal sufficient. But proving completeness can be a pain sometimes, while proving minimal sufficiency is relatively easy. I wonder what would happen if we took a minimal sufficient statistic, say $S$, that is not necessarily complete, and tried to base estimators on it. Note that an example where minimal, but not complete, sufficient statistics can arise is in curved exponential families.

Suppose as in the Lehmann-Scheffe proof, we have an unbiased estimator $Z_1$ of the parameter $\theta$ and the minimal sufficient statistic (MSS) $S$. Consider the estimator given by $W_1(S) = \E[Z_1\vert S]$ . By the [Rao-Blackwell Theorem](https://en.wikipedia.org/wiki/Rao%E2%80%93Blackwell_theorem), since $S$ is sufficient, we have that $\Var[W_1]\leq\Var[Z_1]$. Now, since $S$ is MSS, it is a function of every other sufficient statistic. This implies that for any other sufficient statistic $R$, 

$$\E[W_1\vert R] = \E[W_1(S(R))\vert R] = W_1(S(R)) = W_1(S)$$

In other words, the Rao Blackwell process cannot improve the estimator any further, so that $W_1$ is the optimal estimator derived from $Z_1$. By a similar argument, if there is some other unbiased estimator $Z_2$, we can obtain the optimal estimator $W_2 = \E[Z_2\vert S]$. Now, if $S$ were complete, we could show that $W_1$ and $W_2$ are necessarily the same estimator. But if $S$ is not complete, what happens?

Let $v_1 = \Var[W_1]$, $v_2 = \Var[W_2]$, and without loss of generality, assume $v_1\leq v_2$. At this point, we would consider $W_1$ to be the optimal estimator between the two. So we want to find an estimator that beats it by having lower variance. Consider the estimator

$$U = \frac{W_1+W_2}{2}$$

Its variance is given by

$$\Var[U] = \frac{1}{4}\left(v_1+v_2+2\Cov[W_1,W_2]\right) = (1/2)\frac{v_1+v_2}{2} + (1/2)\Cov[W_1,W_2]$$

By the Cauchy-Schwartz Inequality, 

$$-\sqrt{v_1v_2}\leq \Cov[W_1,W_2]\leq\sqrt{v_1v_2}$$

We can therefore establish upper and lower bounds on $\Var[U]$. The upper bound is:

$$\Var[U]\leq (1/2)\frac{v_1+v_2}{2}+(1/2)\sqrt{v_1v_2}$$

This is a convex combination of the arithmetic and geometric means of $v_1$ and $v_2$, and therefore must be strictly greater than $v_1$ unless $v_1=v_2$, in which case it is equal to $v_1$. The bound is attained only when $W_1$ and $W_2$ are perfectly correlated, which only can occur if one is a linear combination of the other, such that we could write $W_1=aW_2+b$. But since $\theta=\E[W_1]=\E[aW_2+b]=a\E[W_2]+b=a\theta+b$, this means that they must be the same estimator with $a=1,b=0$. Even in this degenerate situation, we note that $\Var[U] = v_1$, showing that the construction of $U$ does no worse than the previous optimal estimator $W_1$.

Now suppose more realistically that $\Cov[W_1,W_2]<\sqrt{v_1v_2}$. Then in this case it may be possible that $\Var[U]< v_1$. We can find values of $v_1,v_2$ to satisfy this requirement. For convenience let the correlation coefficient $\rho = \Cov[W_1,W_2]/\sqrt{v_1v_2}$. We are interested in finding combinations of $\rho,v_1,v_2$ which satisfy

$$\Var[U]  = (1/2)\frac{v_1+v_2}{2}+(1/2)\rho\sqrt{v_1v_2} < v_1$$

The inequality can be reduced to the form

$$3v_1-v_2-2\rho\sqrt{v_1v_2} > 0$$

Using [Wolfram Alpha](http://www.wolframalpha.com/input/?i=3u-v-2psqrt%28u*v%29+%3E+0%3B+-1%3Cp%3C1%3B+u%3E0%3B+v%3E0) we see that solutions to this inequality exist and are of the form

$$v_2 < 3v_1 + 2\rho^2 v_1 \pm 2v_1\rho\sqrt{\rho^2+3}$$

Clearly, we have failed to obtain any general result by conditioning on the minimal sufficient statistic since we cannot eliminate the possibility of improving on two "optimal" statistics by just averaging them.

Based on the above discussion, we conclude that minimal sufficiency is not enough to guarantee any estimator resulting from application of the Rao-Blackwell Theorem has optimal (smallest) variance. This reinforces the importance of the completeness property in proving an unbiased estimator has optimal variance using Lehmann-Scheffe.
