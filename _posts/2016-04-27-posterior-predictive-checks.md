---
title: Posterior Predictive Checks
layout: post
comments: true
---

We are learning about evaluating goodness-of-fit for probabilistic graphical models using posterior predictive checks in my [MIT Bayesian modeling class](http://www.tamarabroderick.com/course_6_882.html) this week. I collected a few useful references:

1. Gelman/Shalizi [philosophical argument](http://www.stat.columbia.edu/~gelman/research/published/philosophy.pdf) against "subjective prior" and in favor of model checking. [Blog post version](http://andrewgelman.com/2015/12/17/gathering-of-philosophers-and-physicists-unaware-of-modern-reconciliation-of-bayes-and-popper/).
2. [Blei- Practical notes](http://www.cs.princeton.edu/courses/archive/fall11/cos597C/lectures/ppc.pdf) on how and why to do posterior predictive checks
3. Gelman/Meng/Stern- paper that invented [realized discrepancies](http://www.cs.princeton.edu/courses/archive/fall09/cos597A/papers/GelmanMengStern1996.pdf) for predictive checking. A discrepancy is a quantity calculated from the posterior predictive distribution used to evaluate model fit. A realized discrepancy is allowed to depend on latent variables as well as the data.
3. Mimno & Blei- example of [applying predictive checks to topic modeling](http://www.cs.princeton.edu/~blei/papers/MimnoBlei2011.pdf)

Perusing these articles, I was surprised to learn that many Bayesians don't think it is necessary to check the adequacy of a choice of prior distribution, since it is "subjective". I agree more with the Gelman/Shalizi idea that choosing a prior is just another part of the model and should be checked, just like one would do in the frequentist context by, for example, evaluation on a with-held test set.