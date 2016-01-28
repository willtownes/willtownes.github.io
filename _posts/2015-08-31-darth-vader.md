---
title: Darth Vader Theorem
layout: post
external: [latex]
comments: true
---

Let $\newcommand{\E}{\mathrm{E}}
\newcommand{\Var}{\mathrm{Var}}
\newcommand{\Cov}{\mathrm{Cov}} X$ be a non-negative random variable. Let $F(x)$ be the cumulative distribution function and $f(x)$ the corresponding density function (assume it exists) and $S(x)=1-F(x) = \int_x^\infty f(t)dt$ the survival function. Then assuming we can interchange order of integration,

$$\E[X] = \int_{0}^\infty S(x) dx$$

Proof:

$$\int_{0}^\infty S(x) dx = \int_{x=0}^\infty \int_{t=x}^\infty f(t) dt dx$$

$$ = \int_{x=0}^\infty \int_{t=0}^\infty f(t)I(t\geq x)dtdx$$

$$ = \int_{t=0}^\infty f(t) \int_{x=0}^t dx dt = \int_0^\infty f(t) (t-0) dt = \int_0^\infty f(x)x dx = \E[X]$$

(since f(t) is the PDF of the random variable $X$)

My study partners refer to this as the "Darth Vader Theorem" but I'm not sure where it comes from. Maybe because it is an evil trick that shows up in a lot of qualifying exam questions? 