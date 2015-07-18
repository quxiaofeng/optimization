---
layout: post
title:  "Alternating Direction Method of Multipliers (ADMM)"
date:   2015-07-18 13:36:14
categories:
---

Consider minimizing {% m %} f({\bf x}) + g({\bf y}) {% em %} subject to affine constraints {% m %} {\bf Ax} + {\bf By} = {\bf c} {%em%}

The augmented Lagrangian

<p>{% math %} \mathcal{L}_\rho({\bf x}, {\bf y}, {\bf \lambda}) = f({\bf x}) + g({\bf y}) + \langle {\bf \lambda}, {\bf Ax} + {\bf By} - {\bf c} \rangle + \frac{\rho}{2} \| {\bf Ax} + {\bf By} - {\bf c} \|^2_2 {% endmath %}</p>

Idea: perform block descent on {%m%}{\bf x}{%em%} and {%m%}{\bf y}{%em%} and then update multiplier vector {%m%}{\bf \lambda}{%em%} 

<p>{% math %}
\begin{align}
{\bf x}^{(t+1)}       & \leftarrow & \min_{\bf x} f({\bf x}) + \langle {\bf \lambda}, {\bf Ax} + {\bf By}^{(t)} - {\bf c} \rangle + \frac{\rho}{2} \| {\bf Ax} + {\bf By}^{(t)} - {\bf c} \|^2_2 \\
{\bf y}^{(t+1)}       & \leftarrow & \min_{\bf y} g({\bf y}) + \langle {\bf \lambda}, {\bf Ax}^{(t+1)} + {\bf By} - {\bf c} \rangle + \frac{\rho}{2} \| {\bf Ax}^{(t+1)} + {\bf By} - {\bf c} \|^2_2 \\
{\bf \lambda}^{(t+1)} & \leftarrow & {\bf \lambda}^{(t)} + \rho ({\bf Ax}^{(t+1)} + {\bf By}^{(t+1)} - {\bf c})
\end{align}
{% endmath %}</p>

## Example: fused lasso

Fused lasso problem minimizes

<p>{% math %} \frac{1}{2} \| {\bf y - X\beta} \|^2_2 + \mu \sum^{p-1}_{j=1} |\beta_{j+1} - \beta_j |{% endmath %}</p>

Define {%m%}{\bf \gamma = D\beta}{%em%}, where

<p>{% math %}
D = \left(\begin{matrix}
1 & -1 & &      &   & \\
  &    & \cdots &   & \\
  &    &        & 1 & -1 
\end{matrix}
\right)
{% endmath %}</p>

Then we minimize {%m%} \frac{1}{2} \| {\bf y} - {\bf X\beta} \|^2_2 + \mu \| \gamma \|_1 {%em%} subject to {%m%} {\bf D\beta} = \gamma {%em%}

Augmented Lagrangian is

<p>{% math %}
\mathcal{L}_\rho({\bf \beta}, {\bf \gamma}, {\bf \lambda}) = \frac{1}{2} \| {\bf y} - {\bf X\beta} \|^2_2 + \mu \| {\bf \gamma} \|_1 + {\bf \lambda}^T({\bf D\beta} - {\bf \gamma}) + \frac{\rho}{2} \| {\bf D\beta} - {\bf \gamma} \|^2_2
{% endmath %}</p>

ADMM:

Update {%m%}{\bf \beta}{%em%} is a smooth quadratic problem
Update {%m%}{\bf \gamma}{%em%} is a separated lasso problem (elementwise thresholding)
Update multipliers

<p>{% math %}
{\bf \lambda}^{(t+1)} \leftarrow {\bf \lambda}^{(t)} + \rho({\bf D\beta}^{(t)} - {\bf \gamma}^{(t)}) 
{% endmath %}</p>

Same algorithm applies to a general regularization matrix {%m%}{\bf D}{%em%} (generalized lasso)

## Remarks on ADMM

Related algorithms

Split Bregman iteration {% sidenote 1 'Goldstein, T. and Osher, S. (2009). The split Bregman method for l1-regularized problems. SIAM J. Img. Sci., 2:323-343.' %}

Dykstra's alternating projection algorithm {% sidenote 2 'Dykstra, R. L. (1983). An algorithm for restricted least squares regression. J. Amer. Statist. Assoc., 78(384):837-842.' %}

...

Proximal point algorithm applied to the dual

Numerous applications in statistics and machine learning: lasso, gen. lasso, graphical lasso, (overlapping) group lasso, ...

Embraces distributed computing for big data {% sidenote 3 'Boyd, S., Parikh, N., Chu, E., Peleato, B., and Eckstein, J. (2011). Distributed optimization and statistical learning via the alternating direction method of multipliers. Found. Trends Mach. learn., 3(1):1-122.' %}