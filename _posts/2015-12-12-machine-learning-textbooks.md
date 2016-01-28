---
title: Machine Learning Textbooks
layout: post
external: [latex]
comments: true
---

Recently I have been reading through a couple of machine learning textbooks. I thought I would describe my impressions of their pros and cons. One caveat is I obviously have not read any of these books end-to-end, but I feel I have read enough to get a good sense of things.

### _Pattern Recognition_, (Bishop)

**This book is good for learning and understanding**. The major advantage of this book is its careful and thorough exposition. The author does a great job making it possible to follow the derivations and uses an abundance of graphs to help the reader see intuitively what is going on. The disadvantage is it does not cover as wide of a range of topics as some other books. I think this book would be the best introduction for a beginner. Of course, a beginner would need to understand linear algebra, calculus, and basic probability theory. Finally, I appreciate the probabilistic focus of the book (i.e. it is more Bayesian).

### _Machine Learning, a Probabilistic Approach_, (Murphy)

**This book is good as a reference**. This is a newer book and is essentially an encyclopedia of machine learning methods. Like the Bishop book, it has a probabilistic (Bayesian) focus, which is appealing, but it does also present other methods for comparison. However, this book covers a lot more interesting material, such as nonparametric methods like [Dirichlet Processes](https://en.wikipedia.org/wiki/Dirichlet_process) and latent variable methods such as [probabilistic matrix factorization](http://www.wikicoursenote.com/wiki/Probabilistic_Matrix_Factorization) This is the book we used as a textbook for [Computer Science 281](http://www.seas.harvard.edu/courses/cs281/). Usually if I want to see what the menu of possible methods are, I start with the Murphy book. Then, if I need additional details, I find the corresponding papers from the extensive reference list or go to the Bishop book for further explanation.

### _Elements of Statistical Learning_, (Hastie, Tibshirani, Friedman)

**This book is strong on statistical theory**. It is an older book and unlike the other two does not have a Bayesian focus. The authors are statisticians rather than computer scientists and the exposition is more abstract. Overall it is my least favorite of the three, since it's just less fun to read. However, for anyone who needs to see proofs and more rigorous analyses, it is certainly a great choice. Again due to being older it does not cover as wide a range of topics as the Murphy book.
