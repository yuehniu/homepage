---
layout: post
title: "Basic Inequalities"
categories: research
use_math: true
author:
- Yue (Julien) Niu
---

Inequalities are a fundamental tool in many analysis. In this blog, I summarize several basic inequality in math analysis:
Cauchy-Schwarz inequality, Jensen's inequality, Holder's inequality, and importantly their relations.

---

## Cauchy-Schwarz inequality

## Jensen's inequality

Jensen's inequality arises from convex function analysis, which states that a secant line of a convex function lies above
the graph of the function. As shown in the figure below, given a **convex** function $f$ two points $x_1, x_2$, and a point between them $\alpha x_1 + (1-\alpha)x_2$,
the following inequality always holds

\[ f(\alpha x_1 + (1-\alpha)x_2) \leq \alpha f(x_1) + (1-\alpha)f(x_2) \]

That is, the secant line defined by $(x_1, f(x_1))$ and $(x_2, f(x_2))$ is always above the graph of the function. 

<p style="text-align: center;">
<img src="https://yuehniu.github.io/homepage//assets/fig/dp/convexity.png" alt="Convex Function" width="500"/>
</p>

Jensen's inequality generalize the above inequality between two points. For numbers $x_1, x_2, \cdots, x_n$, and **positive** values $\alpha_1, \alpha_2, \cdots, \alpha_n$.
With $\alpha_1 + \alpha_2 + \cdots + \alpha_n = 1$, then

\[ f(\alpha_1 x_1 + \alpha_2 x_2 + \cdots + \alpha_n x_n) \leq alpha_1 f(x_1) + \alpha_2 f(x_2) + \cdots + \alpha_n f(x_n)\]