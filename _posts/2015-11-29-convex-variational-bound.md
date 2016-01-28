---
title: Variational Lower Bounds for Convex Functions
layout: post
external: [latex]
comments: true
---

Suppose we have a (scalar) function $f(x)$ that is convex, where $x$ can be a vector. This means every tangent line (or tangent hyperplane in the vector case) to the function lies below the function. Therefore, the family of all tangent lines is a family of lower bounds to the function. This basic idea can be used to replace a difficult function with a simpler one that is a bound by adding in additional parameters. The procedure is as follows:

1. If $f$ is convex, it can be expressed as $f(x) = \max_\eta [x^T\eta - g(\eta)]$. 
$\eta$ is the **variational parameter** and $g(\eta)$ is the **dual function**, which is defined as $g(\eta)=\max_x [x^T\eta - f(x)]$. The intuition is that for every $\eta$, $x^T\eta - g(\eta)$ is a linear function of $x$ lying below $f(x)$. $\eta$ indexes all of these lines according to their slopes. For a particular $x$, there is exactly one such line that coincides with $f(x)$. The dual function is the intercept term of the line which is defined so as to make the line become tangent to $f(x)$.
2. We need to derive $g(\eta)$. Let $\nabla_x$ be the (sub)gradient operator with respect to $x$. This is a generalization of the derivative to the case of non-differentiable $f$. Fix $\eta=\eta^\star$ and let $h(\xi) = \xi^T\eta^\star - f(\xi)$. Here, we are replacing $x$ with $\xi$ to emphasize that when $\eta$ is fixed at $\eta^\star$, the maximum of $h$ occurs when $x=\xi$. In other words, $g(\eta^\star)=max_\xi h(\xi)$. Then a necessary condition for $h(\xi)$ to be at a maximum is: 
$$\nabla_\xi[\xi^T\eta^\star - f(\xi)] = 0$$
, which is equivalent to
$$\eta^\star = \nabla_\xi f(\xi) = \lambda(\xi)$$ .
3. We now have a function $\lambda$ which relates the variational parameter $\eta$ to a different parameter $\xi$ which represents the maximizing argument of $x$ for that particular value of $\eta$. Therefore, for any $\eta$,
$$g(\eta) = \xi^T \eta - f(\xi) = \xi^T (\lambda(\xi)) - f(\xi) = g(\lambda(\xi))$$
. This implies that we can change the parameterization of $g$ to use $\xi$ as the variational parameter instead of $\eta$. Alternatively, if the $\lambda$ function is invertible, we could write 
$$g(\eta) = (\lambda^{-1}(\eta))^T \eta - f(\lambda^{-1}(\eta))$$
. In any case, we now have a closed form expression for $g$ as a function of some variational parameter (either $\xi$ or $\eta$).
4. We now substitute back into the expression for the original function: 
$$f(x) = \max_\eta [\eta^T x - g(\eta)] = \max_\xi [\lambda(\xi)^T x - g(\lambda(\xi))]$$
Let $Q(x,\xi) = \lambda(\xi)^T x - g(\lambda(\xi))$. Then clearly $f(x) = \max_\xi Q(x,\xi)$ which means that $f(x)\geq Q(x,\xi)$ for all $x$ and for all $\xi$. We therefore have obtained a family of lower bounds on $f(x)$.

### Application to Integration
Note that $Q$ is a linear function of $x$. Hence, if we needed to compute some intractable integral (a common occurrence in probability and statistics) such as 

$$\int f(x)p(x)dx$$

Where $p(x)$ is non-negative. For example, $p$ might be a probability density function (PDF). If $f$ is convex, we can bound $f$ below with $Q(x,\xi)$ and, assuming $f$ and $p$ are integrable, by monotonicity of integral,

$$\int f(x)p(x)dx \geq \int Q(x,\xi)p(x)dx = \int (\lambda(\xi)^T x - g(\lambda(\xi)))p(x) dx$$

$$\int f(x)p(x)dx \geq \lambda(\xi)^T \int x p(x)dx - g(\lambda(\xi))\int p(x) dx$$

It is likely the case that $\int x p(x)dx$ and $\int p(x) dx$ are easier to compute than $\int f(x)p(x)dx$. For example, if $p(x)$ is a PDF, the entire expression is equivalent to

$$\mathbb{E}[f(X)] \geq \lambda(\xi)^T \mathbb{E}[X] - g(\lambda(\xi))$$

Once we have this lower bound as a function of the variational parameter $\xi$, we can then obtain the "best" bound within the approximating family by taking a maximum over $\xi$. In other words, 

$$H(\xi) = \lambda(\xi)^T \int x p(x)dx - g(\lambda(\xi))\int p(x) dx$$

$$\int f(x)p(x)dx \geq max_\xi H(\xi)$$

Returning to the PDF example, we can recover Jensen's Inequality:

$$\mathbb{E}[f(X)] \geq max_\xi [\lambda(\xi)^T \mathbb{E}[X] - g(\lambda(\xi))] = max_\eta [\eta^T \mathbb{E}[X] - g(\eta)] = f(\mathbb{E}[X])$$

In summary, we followed these steps to get around the tricky integration

1. Rewrite the convex part of the integrand as the maximum of a family of variational lower bounds
2. A lower bound on the integral is obtained by integrating over one of the (easier) variational lower bound functions instead of the original function
3. The resulting quantity is still a function of the variational parameter
4. Maximize with respect to this variational parameter to get the best lower bound for the integral

### Tips and Tricks
* **Concave function**: Sometimes $f(x)$ is not convex in $x$. If it is concave, then the above procedure can be applied to $-f(x)$ to obtain a family of upper bounds on $f$. 
* **Transforming the function**: If $f(x)$ is neither concave nor convex, another trick is to transform $f$ by some monotone function like $log$ and then see if it is convex or concave on this alternative scale. Due to the monotonicity of the transformation, maxima and minima of the transformed function can be converted to maxima and minima of the original function by applying the reverse transformation.
* **Transforming the argument**: Suppose we have a concave function but we are intent on obtaining a lower bound. We can sometimes convert the function to a convex function by transforming the argument. For example, if $f(x)$ is concave, we could try setting $u=x^2$ and  $f(\sqrt(u))$ might be convex in $u$. We could procede to obtain a lower bound using $u$, then transform back to the original scale. In this case, we would obtain a family of quadratic lower bounds for the original function.
