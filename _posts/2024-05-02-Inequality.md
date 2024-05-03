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

<p style="text-align: center;">
<img src="https://yuehniu.github.io/homepage//assets/fig/dp/convexity.png" alt="Convex Function" width="500"/>
</p>
