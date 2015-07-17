---
layout: post
title:  "Augmented Lagrangian Method"
date:   2015-07-17 11:04:01
categories:
---

Consider minimizing {%m%}f({\bf x}){%em%} subject to equality constraints {%m%}g_i({\bf x}){%em%} for {%m%}i=1,\ldots,q{%em%}

+ Inequality constraints are ignored for simplicity
+ Assume {%m%}f{%em%} and {%m%}g_i{%em%} are smooth for simplicity
+ At a constrained minimum, the Lagrange multiplier condition

{%math%} {\bf 0}=\nabla f({\bf x})+\sum^q_{i=1}\lambda_i\nablag_i({\bf x}){%endmath%}

holds provided {%m%}\nabla g_i({\bf x}){%em%} are linearly independent

**Augmented lagrangian**

{%math%}\mathcal{L}({\bf x},{\bf lambda}) = f({\bf x}) + \sum^q_{i=1}\lambda_i g_i({\bf x}) + \frac{\rho}{2}\sum^q_{i=1}g_i({\bf x})^2{%endmath%}

+ The penalty term {%m%}\frac{\rho}{2}\sum^q_{i=1}g_i({\bf x})^2{%em%} punishes violations of the equality constraints {%m%}g_i({\bf \theta}){%em%}
+ Optimize the Augmented Lagrangian and adjust {%m%}{\bf \lambda}{%em%} in the hope of matching the true Lagrange multipliers
+ For {%m%}\rho{%em%} large enough (finite), the unconstrained minimizer of the augmented lagrangian coincides with the constrained solution of the original problem
+ At convergence, the gradient {%m%}\rho g_i({\bf x})\nablagi({\bf x}){%em%} vanishes and we recover the standard multiplier rule

<!--more-->

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

### For non-smooth {%m%}f{%em%}, replace gradient {%m%}\nabla f{%em%} by sub-differential {%m%}\partial f{%em%}

## Example: basis pursuit

Basis pursuit problem seeks the sparsest solution subject to linear constraints

{%math%}
\begin{align}
minimize & \norm({\bf x})_1 \\
subject to & {\bf Ax} = {\bf b}
\end{align}
{%endmath%}

Take {%m%}\rho{%em%} initially large or gradually increase it; iterate according to

{%math%}
\begin{align}
{\bf x}^{(t+1)}                 & \norm({\bf x})_1 \\
{\bf \lambda}^{(t+1)} & {\bf Ax} = {\bf b}
\end{align}
{%endmath%}

Converges in a finite (small) number of steps {% sidenote 1 'Bregman Iterative Algorithms for 1-Minimization with Applications to
Compressed Sensing∗: [http://www.caam.rice.edu/~wy1/paperfiles/Rice_CAAM_TR07-13.PDF](http://www.caam.rice.edu/~wy1/paperfiles/Rice_CAAM_TR07-13.PDF)' %}