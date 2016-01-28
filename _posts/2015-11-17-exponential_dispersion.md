---
title: Exponential Dispersion Family
layout: post
external: [latex]
comments: true
---

### Parametrization

The Exponential Dispersion Family is a family of probability density/mass functions with many nice properties. Here we will demonstrate how to easily obtain the (central) moments such as mean and variance of a random variable with a distribution in this family. The pdf should have the form

$$\newcommand{\E}{\mathrm{E}}
\newcommand{\Var}{\mathrm{Var}}
f(y) = h(y,\phi)\exp\left[\frac{y\theta-b(\theta)}{\phi}\right]$$

The components of this distribution include the **canonical parameter** $\theta$, which in generalized linear models is connected to the covariates via a link function, the **dispersion parameter** $\phi$ which is treated as a constant with respect to the covariates, and the **cumulant function** $b(\theta)$ which is related to the [log partition function](https://en.wikipedia.org/wiki/Partition_function_%28statistical_mechanics%29). Basically, the partition function is the normalizing constant of the density function.

### Characteristic Function

This can be derived analytically from the PDF

$$\psi(t) = \E[e^{ity}] = \int e^{ity}f(y)dy = \int \exp(ity)h(y,\phi)\exp\left[\frac{y\theta-b(\theta)}{\phi}\right]dy$$

$$ = \exp\left[-\frac{b(\theta)}{\phi}\right]\int h(y,\phi)\exp\left[\frac{y\theta}{\phi} + ity\right]dy$$

$$= \exp\left[-\frac{b(\theta)}{\phi}\right]\int h(y,\phi)\exp\left[\frac{y(\theta + it\phi)}{\phi}\right]dy$$

If we set $\theta^\star=\theta+it\phi$, we can recognize that the integral is now again in the form of an un-normalized exponential dispersion family. Because a normalized PDF must integrate to one, we have the following result:

$$\int h(y,\phi)\exp\left[\frac{y\theta^\star}{\phi}\right]\exp\left[-\frac{b(\theta^\star)}{\phi}\right]dy = 1$$

$$\int h(y,\phi)\exp\left[\frac{y\theta^\star}{\phi}\right]dy = \exp\left[+\frac{b(\theta^\star)}{\phi}\right]$$

Substituting this back into the equation for the characteristic function gives the result

$$\psi(t) = \exp\left[-\frac{b(\theta)}{\phi}\right]\exp\left[+\frac{b(\theta^\star)}{\phi}\right] = \exp\left[\frac{b(\theta^\star) - b(\theta)}{\phi}\right]$$

$$ = \exp\left[\frac{b(\theta+it\phi) - b(\theta)}{\phi}\right]$$

### Calculation of Moments using Characteristic Function

Like all characteristic functions, $\psi(0) = 1$ and the $k^{th}$ moment can be obtained by the formula

$$\mu_k = (-i)^k\frac{d^k}{dt^k}\psi(t)\rvert_{t=0}$$

The mean (first moment) is given by differentiating once using the chain rule:

$$\mu_1 = (-i)\psi'(t)\rvert_{t=0}$$

$$ = (-i)\exp\left[\frac{b(\theta+it\phi) - b(\theta)}{\phi}\right]\frac{1}{\phi}\left(b'(\theta+it\phi)(i\phi)\right)\rvert_{t=0}$$

$$ = (-i)\psi(t)\frac{1}{\phi}\left(b'(\theta+it\phi)(i\phi)\right)\rvert_{t=0}$$

$$ = \psi(t)b'(\theta+it\phi)\rvert_{t=0} $$

$$ = b'(\theta) $$

Note that in the process we had the intermediate result that

$$\psi'(t) = i\psi(t)b'(\theta+it\phi)$$

The second moment is given by differentiating again with respect to t, accomplished via the product rule:

$$\mu_2 = (-i)\psi^{\prime \prime}(t)\rvert_{t=0} = (-i)\frac{d}{dt} \psi(t)b'(\theta+it\phi)\rvert_{t=0} $$

$$= (-i)\left(\psi'(t)b'(\theta+it\phi) + \psi(t)b^{\prime \prime} (\theta+it\phi)(i\phi)\right)\rvert_{t=0}$$

$$= (-i)\left(i\psi(t)\left(b'(\theta+it\phi)\right)^2+\psi(t)b^{\prime \prime} (\theta+it\phi)(i\phi)\right)\rvert_{t=0}$$

$$ = (-i)\psi(t)(i)\left(\left(b'(\theta+it\phi)\right)^2+\phi b^{\prime \prime} (\theta+it\phi)\right)\rvert_{t=0}$$

$$ = \left(b'(\theta)\right)^2 + \phi b^{\prime \prime}(\theta)$$

The variance is given by the second moment minus the square of the first moment

$$\Var[Y] = \mu_2 - \mu_1^2 = \left(b'(\theta)\right)^2 + \phi b^{\prime \prime}(\theta) - \left(b'(\theta)\right)^2$$

$$ = \phi b^{\prime \prime}(\theta)$$

### Moment- and Cumulant- Generating Functions

The moment generating function is just the characteristic function without the $i$:

$$M_y(t) = \exp\left[\frac{b(\theta+t\phi) - b(\theta)}{\phi}\right]$$

Following a similar procedure as before, we could have calculated the moments from the MGF instead. The advantage of using the CF is that it is a general procedure that always works, whereas the MGF may not exist for certain random variables. However, in the case of the exponential dispersion family, the MGF does exist so this approach is satisfactory.

A small inconvenience of the MGF or CF approach to calculating moments is that we are often more interested in the central moments $\E[(Y-\E[Y])^k]$ rather than the moments $\E[Y^k]$. The first three central moments coincide with quantities called the [cumulants](https://en.wikipedia.org/wiki/Cumulant). Since the MGF exists, we can use an even easier generating function called the **cumulant generating function**, which is simply the log of the MGF:

In any case, it ends up that $\E[Y] = b'(\theta)$ and $\Var[Y] = \phi b^{\prime \prime}(\theta)$ which is the main result we are interested in. Note that it is now easy to see why $\phi$ is referred to as the dispersion parameter, since if we are trying to estimate the variance of $Y$ based only on the covariates, we would only be able to do so through functions of $\theta$. Therefore we would try to use $b^{\prime \prime}(\theta)$ as the estimate. This is related to the so-called mean-variance relation of GLMs. But, if $\phi>1$ (overdispersion), we would underestimate the true variance. This is a very common phenomenon in real data. Therefore, one would often attempt to estimate $\phi$ as well using residuals from an initial model fit. Then, this estimate could be incorporated to adjust for the overdispersion before performing inference on the coefficients of the covariates of interest. This procedure is known as quasi-likelihood.

### Conclusion

Moments of random variables from the exponential dispersion family can be quickly and easily calculated by inspection of the functional form of the density/mass function. In particular, attention should be focused on the cumulant function $b(\theta)$.
