---
title: Exponential Dispersion Family
layout: post
external: [latex]
---

### Parametrization

The Exponential Dispersion Family is a family of probability density/mass functions with many nice properties. Here we will demonstrate how to easily obtain the central moments such as mean and variance of a random variable with a distribution in this family. The pdf should have the form

$$\newcommand{\E}{\mathrm{E}}
\newcommand{\Var}{\mathrm{Var}}
f(y) = h(y,\phi)\exp\left\\{\frac{y\theta-b(\theta)}{\phi}\right\\}$$

The components of this distribution include the **canonical parameter** $\theta$, which in generalized linear models is connected to the covariates via a link function, the **dispersion parameter** $\phi$ which is treated as a constant with respect to the covariates, and the **cumulant generating function** $b(\theta)$ which is also known as the [log partition function](https://en.wikipedia.org/wiki/Partition_function_%28statistical_mechanics%29). 

### Characteristic Function

This can be derived analytically from the PDF

$$\psi(t) = \E[e^{ity}] = \int e^{ity}f(y)dy = \int \exp(ity)h(y,\phi)\exp\left\\{\frac{y\theta-b(\theta)}{\phi}\right\\}dy$$

$$ = \exp\left\\{-\frac{b(\theta)}{\phi}\right\\}\int h(y,\phi)\exp\left\\{\frac{y\theta}{\phi} + ity\right\\}dy$$
$$= \exp\left\\{-\frac{b(\theta)}{\phi}\right\\}\int h(y,\phi)\exp\left\\{\frac{y(\theta + it\phi)}{\phi}\right\\}dy$$

If we set $\theta^\star=\theta+it\phi$, we can recognize that the integral is now again in the form of an un-normalized exponential dispersion family. Because a normalized PDF must integrate to one, we have the following result:

$$\int h(y,\phi)\exp\left\\{\frac{y\theta^\star}{\phi}\right\\}\exp\left\\{-\frac{b(\theta^\star)}{\phi}\right\\}dy = 1$$
$$\int h(y,\phi)\exp\left\\{\frac{y\theta^\star}{\phi}\right\\}dy = \exp\left\\{+\frac{b(\theta^\star)}{\phi}\right\\}$$

Substituting this back into the equation for the characteristic function gives the result

$$\psi(t) = \exp\left\\{-\frac{b(\theta)}{\phi}\right\\}\exp\left\\{+\frac{b(\theta^\star)}{\phi}\right\\} = \exp\left\\{\frac{b(\theta^\star) - b(\theta)}{\phi}\right\\}$$
$$ = \exp\left\\{\frac{b(\theta+it\phi) - b(\theta)}{\phi}\right\\}$$
