---
title: Converging in Probability but not Almost Surely
layout: post
external: [latex]
comments: true
---

Like many people, I find the distinctions between different kinds of convergence to be a tricky topic in probability theory. Convergence in probability deals with **sequences of probabilities** while convergence almost surely (abbreviated a.s.) deals with **sequences of sets**. The following example, which was originally provided by Patrick Staples and Ryan Sun, shows that a sequence of random variables can converge in probability but not a.s. Let $X_n$ be a sequence of independent random variables ($n=1,2,....$) such that

$$\Pr(X_n=1) = 1-\frac{1}{n}$$

$$\Pr(X_n=0) = 1/n$$

We claim that $X_n\to 1$ in probability but does not converge a.s. 

###Proving Convergence in Probability
To prove convergence in probability, we need to show for any $\epsilon>0$,

$$\lim_{n\to\infty} \Pr(\vert X_n-1\vert <\epsilon) = 1$$

Since $\{\vert X_n-1\vert <\epsilon\}=\{X_n=1\}$, this is equivalent to

$$\lim_{n\to\infty} \Pr(X_n=1)=1$$

$$\lim_{n\to\infty} 1-\frac{1}{n} = 1$$

which is clearly satisfied.

###Disproving Convergence Almost Surely
The definition of convergence a.s. applied to the example is:

$$\Pr(\lim_{n\to\infty}\{\vert X_n-1\vert <\epsilon\}) = 1$$

Again we can replace the event $\{\vert X_n-1\vert <\epsilon\}$ with $\{X_n=1\}$  Note that we are dealing here with a sequence of sets. For notational convenience, let $E_n=\{X_n=1\}$ be a sequence of sets. Let's try to prove almost sure convergence, and in the process, we will see why it does not happen. Recall from real analysis that

$$\limsup_{n\to\infty} E_n = \bigcap_{n=1}^\infty \bigcup_{k=n}^\infty E_k$$

$$\liminf_{n\to\infty} E_n = \bigcup_{n=1}^\infty \bigcap_{k=n}^\infty E_k$$

We interpret $\limsup$ as the event occuring "infinitely often" and $\liminf$ as the event occuring "almost always". $\liminf$ is a stronger condition than $\limsup$  In general, it is easier to deal with $\limsup$ or $\liminf$ separately rather than the limit itself. Furthermore, $\lim_{n\to\infty} E_n$ exists if and only if 

$$\limsup_{n\to\infty} E_n = \liminf_{n\to\infty} E_n$$

and therefore,

$$\Pr(\lim_{n\to\infty}E_n) = 1$$

if and only if

$$\Pr(\liminf_{n\to\infty}E_n) = \Pr(\limsup_{n\to\infty}E_n) = 1$$

We always have

$$\liminf_{n\to\infty} E_n \subseteq \limsup_{n\to\infty} E_n$$

Due to the properties of probability measures, this implies

$$\Pr(\liminf_{n\to\infty} E_n)\leq\Pr(\limsup_{n\to\infty} E_n)$$

Therefore an easier way to prove convergence a.s. is just to show

$$\Pr(\liminf_{n\to\infty}E_n) = 1$$

On the other hand, if we have 

$$\Pr(\liminf_{n\to\infty}E_n) < 1$$

This would disprove convergence a.s. Note that this is implied whenever

$$\Pr(\limsup_{n\to\infty}E_n) < 1$$

which suggests a shortcut.

#### The "easy" way with limsup
To disprove converence a.s. it is sufficient (but not necessary) to show

$$\Pr(\limsup_{n\to\infty}E_n) < 1$$

This means that if we can show this to be true, it will disprove convergence a.s., but if we cannot show it to be true, it does not automatically prove convergence a.s. Let's give it a try. 

Anytime we are dealing with $\limsup$ it is useful to apply the **Borell-Canteli Lemmas**. Lemma 1 is

$$\sum_{n=1}^\infty \Pr(E_n) < \infty \implies \Pr(\limsup_{n\to\infty}E_n)=0$$

Lemma 2 requires the assumption that the $E_n$ are independent. Then,

$$\sum_{n=1}^\infty \Pr(E_n) = \infty \implies \Pr(\limsup_{n\to\infty}E_n)=1$$

These are our friends because they help us prove results about sequences of sets using the (easier) sequences of probabilities. In the current example, we have independent $E_n$ and

$$\sum_{n=1}^\infty \Pr(E_n) = \sum_{n=1}^\infty (1-1/n) = \infty-0 = \infty$$

which implies that 

$$\Pr(\limsup_{n\to\infty}E_n) = 1$$

which is not what we wanted to prove. So unfortunately this approach does not give us any clear answer about the convergence, but in other problems it might be useful. We must trudge on and try the more difficult approach with $\liminf$ to get an answer.

#### The slightly harder way with liminf
One useful trick for dealing with $\liminf$ is to simply use **De Morgan's Laws** to convert it into $\limsup$  The essential fact is that the complement of the $\liminf$ is the $\limsup$ of the complements. More formally,

$$\left(\liminf_{n\to\infty} E_n\right)^\complement = \left(\bigcup_{n=1}^\infty 
\bigcap_{k=n}^\infty E_k\right)^\complement = \bigcap_{n=1}^\infty \bigcup_{k=n}^\infty E_k^\complement = \limsup_{n\to\infty} E_n^\complement$$

Recall that we are trying to evaluate 

$$\Pr(\liminf_{n\to\infty}E_n) = 1-\Pr(\limsup_{n\to\infty}E_n^\complement)$$

Since $E_n = \{X_n=1\}$, we have $E_n^\complement = \{X_n=0\}$  Note that 

$$\sum_{n=1}^\infty \Pr(E_n^\complement) = \sum_{n=1}^\infty \Pr(X_n=0) = \sum_{n=1}^\infty (1/n) = \infty$$

and that the $E_n^\complement$ events are mutually indendent. This implies by Borell-Cantelli Lemma 2 that

$$\Pr(\limsup_{n\to\infty}E_n^\complement) = 1$$

and therefore,

$$\Pr(\liminf_{n\to\infty}E_n) = 1-\Pr(\limsup_{n\to\infty}E_n^\complement) = 0$$

As noted previously, this condition disproves convergence a.s. of the sequence of $X_n$ 

To summarize, since we found

$$\Pr(\limsup_{n\to\infty}\vert X_n-1\vert <\epsilon) = 1$$

$$\Pr(\liminf_{n\to\infty}\vert X_n-1\vert <\epsilon) = 0$$

this implies

$$\Pr(\lim_{n\to\infty}\{\vert X_n-1\vert <\epsilon\}) \neq 1$$

which means $X_n$ does not converge a.s. to 1.