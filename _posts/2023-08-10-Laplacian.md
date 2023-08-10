---
layout: post
title: "Laplacian Mechanism"
categories: research
github_comments_issueid: "3"
use_math: true
author:
- Yue (Julien) Niu
---

## Overview
Laplacian mechanism is a standard mechanism that guarantees $(\epsilon)$-DP. It a good and easy study case to if one
need to get a first glance on how DP analysis is done. 
Before formally presenting Laplacian mechanism, we can start from a simple example:

### A Practical Example

<img src="https://yuehniu.github.io/homepage//assets/fig/dp/laplacian.png" alt="Mean with DP" width="800"/>

Suppose *System* in the figure above is a **Mean** function as 

\[ f (D) = \frac{1}{n}\sum_{i=1}^N x^i \] 

If $D$ and $D'$ differ on one record, their means are also different. From an attacker's view, it is easy to decide
if a record $x^k$ comes from $D$ or $D'$:

> The attacker can replace each record in $D$ and $D'$ with $x^k$, and check the output from **Mean** function.
> If there exists one record in $D$ such that output does not change when replaced by $x^k$, then $x^k$ is in $D$.
> Otherwise, $x^k$ is in $D'$

Therefore, we can see that the attacker can success because the **Mean** op is a deterministic function. Any small 
changes in inputs will be observed by the attacker. If we can introduce some randomness in the operation, then
the attacker will not be able decided if changes in outputs comes from inputs or random noise. That is exactly 
where DP comes from. 

---

## Laplacian Mechanism

**L1-sensitivity**: We use L1 distance to measure how *close* $D$ and $D'$ are, which is defined as 

\[ \Delta_1 = \max_{D, D'} \| f(D) - f(D') \| \]

where $D'$ can be any data with only record differs from $D$.

**Laplacian Mechanism**: For a function $f: D \rightarrow R^d$, a Laplace mechanism

\[ M(D) = f(D) + (n^1, \cdots, n^d ) \]

is $(\epsilon)$-DP if $n^i$ are independent $Laplace(\Delta_1/\epsilon)$ random variables.

We provide the proof below.

### Proof

To simplify notations, let $z\in R^d$ denote output from $M$.

The probability density function of $z$ given $D$ and $D'$ are

\[ P(M(D)=z) = P(n=z-f(D)) = \prod_{i=1}^d e^{(-\frac{\epsilon \| f(D)^i -z^i\|}{\Delta_1})} \]

\[ P(M(D')=z) = P(n=z-f(D')) = \prod_{i=1}^d e^{(-\frac{\epsilon \| f(D')^i -z^i\|}{\Delta_1})} \]

Taking the division, we have 

\[ \frac{P(M(D)=z)}{P(M(D')=z)} = \prod_{i=1}^d e^{-\frac{\epsilon (\| f(\mathcal{D})^i -z^i\| -\| f(D')^i -z^i\|)}{\Delta_1}} \]

Applying the triangle inequality, we have

\[ \frac{P(M(D)=z)}{P(M(D')=z)} &\leq \prod_{i=1}^d e^{\frac{\epsilon (\| f(D)^i - f(D')^i\|)}{\Delta_1}} \]

\[ = e^{(\frac{\epsilon\sum_{i=1}^d \|f(D)^i - f(D')^i\| }{\Delta_1})} \] 

\[ = e^{(\frac{\epsilon \|f(D) - f(D')\|_1 }{\Delta_1})} \]

\[ = e^{\epsilon} \]

### Remark

We can easily observe that given the same privacy budget $\epsilon$, 
large noise is needed if $D$ and $D'$ are further different (large $\Delta_1$).