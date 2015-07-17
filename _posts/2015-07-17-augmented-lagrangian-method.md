---
layout: post
title:  "Augmented Lagrangian Method"
date:   2015-07-17 11:04:01
categories:
---

Consider minimizing {%m%} f({\bf x}) {%em%} subject to equality constraints {%m%} g_i({\bf x}) = 0 {%em%} for {%m%}i=1, \ldots ,q{%em%}

+ Inequality constraints are ignored for simplicity

+ Assume {%m%}f{%em%} and {%m%}g_i{%em%} are smooth for simplicity

+ At a constrained minimum, the Lagrange multiplier condition

{%math%}  {\bf 0}=\nabla f({\bf x})+\sum^q_{i=1}\lambda_i\nabla g_i({\bf x})  {%endmath%}

holds provided {%m%}\nabla g_i({\bf x}){%em%} are linearly independent

<!--more-->

**Augmented lagrangian**

{%math%}\mathcal{L}_\rho ({\bf x},{\bf \lambda}) = f({\bf x}) + \sum^q_{i=1}\lambda_i g_i({\bf x}) + \frac{\rho}{2}\sum^q_{i=1}g_i({\bf x})^2{%endmath%}

+ The penalty term {%m%}\frac{\rho}{2}\sum^q_{i=1}g_i({\bf x})^2{%em%} punishes violations of the equality constraints {%m%}g_i({\bf \theta}){%em%}

+ Optimize the Augmented Lagrangian and adjust {%m%}{\bf \lambda}{%em%} in the hope of matching the true Lagrange multipliers

+ For {%m%}\rho{%em%} large enough (finite), the unconstrained minimizer of the augmented lagrangian coincides with the constrained solution of the original problem

+ At convergence, the gradient {%m%}\rho g_i({\bf x})\nabla g_i({\bf x}){%em%} vanishes and we recover the standard multiplier rule

## Algorithm

Take {%m%}\rho{%em%} initially large or gradually increase it; iterate

+ Find the unconstrained minimum

{%math%}{\bf x}^{(t+1)}\leftarrow \min_x\mathcal{L}_\rho ({\bf x},{\bf \lambda}^{(t)}){%endmath%}

+ Update the multiplier vector {%m%}{\bf \lambda}{%em%}

{%math%}\lambda^{(t+1)}_i \leftarrow \lambda^{(t)}_i + \rho g_i({\bf x}^{(t)}), \; i = 1, \ldots , q{%endmath%}

### Intuition for updating {%m%}{\bf \lambda}{%em%}

If {%m%}{\bf x}^{(t)}{%em%} is the unconstrained minimum of {%m%}\mathcal{L}({\bf x},{\bf lambda}){%em%}, then the stationary condition says

{%math%}
\begin{align}
{\bf 0} & = \nabla f({\bf x}^{(t))} + \sum^q_{i=1} \lambda^{(t)}_i \nabla g_i({\bf x}^{(t)}) + \rho \sum^q_{i=1} g_i({\bf x}^{(t)}) \nabla g_i({\bf x}^{(t)}) \\
& = \nabla f({\bf x}^{(t))} + \sum^q_{i=1} \left[ \lambda^{(t)}_i  \rho g_i({\bf x}^{(t)}) \right] \nabla g_i({\bf x}^{(t)})
\end{align}
{%endmath%}