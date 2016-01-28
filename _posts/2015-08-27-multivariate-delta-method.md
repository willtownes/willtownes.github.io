---
title: Multivariate Delta Method
layout: post
external: [latex]
comments: true
---

### Case 1- Scalar Valued Function

Suppose we are interested in obtaining the asymptotic sampling distribution of a scalar function $g$ of a parameter vector $\theta$ of dimension $q$, and we have an estimator $\newcommand{\E}{\mathrm{E}}
\newcommand{\Var}{\mathrm{Var}}
\newcommand{\Cov}{\mathrm{Cov}} T_n$ such that 

$$\lim_{n\to\infty} \sqrt{n}(T_n-\theta) \,{\buildrel d \over =}\, X$$

Where $X\sim\mathcal{N_q}(\vec{0},\Sigma)$, which is a multivariate normal distribution. This situation would typically arise when $T_n$ is a sample mean estimating a population mean, and the Central Limit Theorem has been used. Assume $g$ satisfies [regularity conditions](https://en.wikipedia.org/wiki/Delta_method) such as having bounded, continuous second partial derivatives. We are interested in finding the distribution of 

$$\lim_{n\to\infty} \sqrt{n}(g(T_n)-g(\theta))$$

First, create a Taylor Expansion of the function around $\theta$:

$$g(T_n) = g(\theta) + \nabla g(\theta)^\intercal (T_n-\theta) + \frac{1}{2}(T_n-\theta)^\intercal \mathbb{H}(T^\star_n)(T_n-\theta)$$

Where $\nabla g(\theta)$ is the gradient (vector of first partial derivatives) evaluated at $\theta$ and $\mathbb{H}(T^\star_n)$ is the Hessian matrix (of all second partial derivatives) evaluated at the point $T^\star_n$ which from Taylor's Theorem (and the Intermediate Value Theorem) has the property that $\vert\vert T^\star_n - \theta \vert\vert \leq \vert\vert T_n - \theta \vert\vert$ for all $n$. Intuitively, $T^\star_n$ is "closer" to $\theta$ than $T_n$ according to some norm. Now, rearrange terms and multiply both sides by $\sqrt{n}$

$$\sqrt{n}\left(g(T_n) - g(\theta)\right) =  \nabla g(\theta)^\intercal \left(\sqrt{n}(T_n-\theta)\right) + \frac{\sqrt{n}}{2}(T_n-\theta)^\intercal \mathbb{H}(T^\star_n)(T_n-\theta)$$

#### Case 1a- Nonzero Gradient as $n\to\infty$

If $\nabla g(\theta) \neq \vec{0}$, then we can evaluate the limit term-by-term. We already know that $\sqrt{n}(T_n-\theta) \,{\buildrel d \over \to}\, X$. Since $\nabla g(\theta)$ is a constant, then we have

$$\nabla g(\theta)^\intercal \left(\sqrt{n}(T_n-\theta)\right) \,{\buildrel d \over \to}\, \nabla g(\theta)^\intercal  X \sim \mathcal{N}\left(0,\nabla g(\theta)^\intercal \Sigma \nabla g(\theta)\right)$$

Furthermore, the second term involving the Hessian matrix converges to zero. To show this, first note that since $\sqrt{n}\left(T_n-\theta\right) \,{\buildrel d \over \to}\, X$ this implies $(T_n-\theta) \,{\buildrel p \over \to}\, \vec{0}$. Furthermore, by the Squeeze Theorem, since $\vert\vert T^\star_n - \theta \vert\vert \leq \vert\vert T_n - \theta \vert\vert$ for all $n$, then $(T^\star_n - \theta) \,{\buildrel p \over \to}\, \vec{0}$ also, or equivalently, $T^\star_n \,{\buildrel p \over \to}\, \theta$. Since we also are assuming continuous second-order derivatives of $g$, the matrix-valued Hessian function $\mathbb{H}$ is a continuous mapping, such that by the continuous mapping theorem $\mathbb{H}(T^\star_n) \,{\buildrel p \over \to}\, \mathbb{H}(\theta)$. Combining all of these results by Slutsky's Theorem shows that

$$\frac{1}{2}\sqrt{n}(T_n-\theta)^\intercal \mathbb{H}(T^\star_n)(T_n-\theta) \,{\buildrel d \over \to}\, \frac{1}{2}X^\intercal\mathbb{H}g(\theta)\vec{0} \,{\buildrel d \over =}\,
\vec{0}$$

Again invoking Slutsky's Theorem this shows that

$$\sqrt{n}\left(g(T_n)-g(\theta)\right) \,{\buildrel d \over \to}\, \nabla g(\theta)^\intercal  X \sim \mathcal{N}\left(0,\nabla g(\theta)^\intercal \Sigma \nabla g(\theta)\right)$$

Note that the normal distribution is now a univariate normal rather than a multivariate one, since $g$ is a scalar-valued function.

#### Case 1b- Zero Gradient as $n\to\infty$

If $\nabla g(\theta) = \vec{0}$ and we follow the argument above, then we would have a situation where $\sqrt{n}\left(g(T_n)-g(\theta)\right) \,{\buildrel d \over \to}\, \vec{0}^\intercal X \,{\buildrel d \over =}\, \vec{0}$, which is not very interesting. So instead, consider multiplying by $n$ instead of $\sqrt{n}$. We have

$$n\left(g(T_n)-g(\theta)\right) = n\nabla g(\theta)^\intercal (T_n-\theta) + \frac{1}{2}\sqrt{n}(T_n-\theta)^\intercal \mathbb{H}g(T^\star_n) \sqrt{n}(T_n-\theta)$$

Notice the "trick" of splitting up the $n$ term into two $\sqrt{n}$ terms, which helps make it obvious that, using a similar (Slutsky) argument as above, 

$$ \frac{1}{2}\sqrt{n}(T_n-\theta)^\intercal \mathbb{H}g(T^\star_n) \sqrt{n}(T_n-\theta) \,{\buildrel d \over \to}\, \frac{1}{2}X^\intercal \mathbb{H}g(\theta) X$$

Furthermore, since $n\nabla g(\theta) = \vec{0}$ for all $n$, it follows that $n\nabla g(\theta)^\intercal (T_n-\theta) \,{\buildrel d \over \to}\, \vec{0}$ so that by Slutsky's Theorem,

$$n\left(g(T_n)-g(\theta)\right) \,{\buildrel d \over \to}\, \frac{1}{2}X^\intercal \mathbb{H}g(\theta) X$$

But what is the distribution of this limit? First, note that since we assumed continuous second derivatives, by [Young's Theorem](https://en.wikipedia.org/wiki/Symmetry_of_second_derivatives) the Hessian matrix $\mathbb{H}g(\theta)$ is symmetric. In addition, since for any multivariate normal distribution, the covariance matrix is non-negative definite (aka positive semi-definite), we can write $X \,{\buildrel d \over =}\, AZ$ where $Z\sim\mathcal{N_q}(\vec{0},\mathbf{I})$ (i.e. that each element of Z is an independent standard normal random variable), and $\Sigma=AA^\intercal$. Therefore, we have that

$$n\left(g(T_n)-g(\theta)\right) \,{\buildrel d \over \to}\, \frac{1}{2}Z^\intercal A^\intercal \mathbb{H}g(\theta) AZ$$

Now, since $\mathbb{H}g(\theta)$ is symmetric, this implies $A^\intercal \mathbb{H}g(\theta) A$ is also symmetric, so that we can use the spectral decomposition to write

$$A^\intercal \mathbb{H}g(\theta) A = U\Lambda U^\intercal$$

Where $U$ is an orthogonal matrix of eigenvectors and $\Lambda$ is a diagonal matrix of eigenvalues. Now, note that $UZ \,{\buildrel d \over =}\, Z$ because the multivariate standard normal is invariant under orthogonal transformation (which is geometrically a rotation). More formally, $UZ \sim \mathcal{N_q}(U\vec{0},U\mathbf{I}U^\intercal)$, but $U\vec{0}=\vec{0}$ and $U\mathbf{I}U^\intercal = UU^\intercal = \mathbf{I}$ since for any orthogonal matrix, $U^\intercal = U^{-1}$. Therefore, we have

$$\frac{1}{2}Z^\intercal A^\intercal \mathbb{H}g(\theta) AZ \,{\buildrel d \over =}\, \frac{1}{2}Z^\intercal U^\intercal \Lambda UZ \,{\buildrel d \over =}\, \frac{1}{2} Z^\intercal \Lambda Z \,{\buildrel d \over =}\, \frac{1}{2}\sum_{i=1}^q \lambda_i Z_i^2$$

Where $\lambda_i$ is the $i^{th}$ diagonal element (eigenvalue) of $\Lambda$, and $Z_i\sim \mathcal{N}(0,1)$ are independent standard normal random variables. Therefore, $Z_i^2\sim \mathcal{\chi^2_{(1)}}$ are independent chi-squared random variables with one degree of freedom each. In conclusion, this shows that $n\left(g(T_n)-g(\theta)\right)$ converges to a [linear combination of chi-squared random variables](https://en.wikipedia.org/wiki/Chi-squared_distribution#Linear_combination), which does not have a closed form.

$$\lim_{n\to\infty} n\left(g(T_n)-g(\theta)\right) \,{\buildrel d \over =}\, \frac{1}{2}\sum_{i=1}^q \lambda_i Z_i^2$$

### Case 2- Vector Valued Function (incomplete)
Consider a function $\vec{g}(\vec{t})\colon \mathbb{R}^n\to\mathbb{R}^m$. Define $\mathbf{J}(\vec{t})$ as the $m\times n$ [Jacobian Matrix](https://en.wikipedia.org/wiki/Jacobian_matrix_and_determinant) of all first derivatives of $\vec{g}$ such that the element in the $i^{th}$ row and the $j^{th}$ column is given by:

$$\mathbf{J}_{ij}(\vec{t}) = \frac{\partial g_i}{\partial t_j}$$

Now, intuitively, we would like to show something like

$$\sqrt{n}\left(\vec{g}(T_n)-\vec{g}(\theta)\right)  = \sqrt{n} \mathbf{J} (T_n^\star)(T_n-\theta) \,{\buildrel d \over \to}\, \mathbf{J}(\theta)X \sim \mathcal{N_m}(\vec{0},\mathbf{J}(\theta)\Sigma \mathbf{J}(\theta)^\intercal)$$

But there is a problem. We cannot directly assert the existence of the point $T^\star_n$ since there is no [Mean Value Theorem for vector-valued functions](https://en.wikipedia.org/wiki/Mean_value_theorem#Mean_value_theorem_for_vector-valued_functions)

At this point, my guess is that we need to write out the vector-valued Taylor Expansion using the "remainder" form rather than the "intermediate value" form. Then, perhaps we can show that the remainder diminishes to zero more rapidly than everything else. Or perhaps more simply we could just treat each of the $m$ component functions of $\vec{g}$ as scalar-valued functions and show that each one converges using the theory from Case 2b above. But this would only give the individual marginal distributions, not the joint distribution that we seek. 

Let me know if you have any suggestions about how to proceed!
