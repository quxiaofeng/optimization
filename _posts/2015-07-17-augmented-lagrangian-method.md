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

<p> {%math%}  {\bf 0}=\nabla f({\bf x})+\sum^q_{i=1}\lambda_i\nabla g_i({\bf x})  {%endmath%} </p>

holds provided {%m%}\nabla g_i({\bf x}){%em%} are linearly independent

<!--more-->

**Augmented lagrangian**

<p> {%math%}\mathcal{L}_\rho ({\bf x},{\bf \lambda}) = f({\bf x}) + \sum^q_{i=1}\lambda_i g_i({\bf x}) + \frac{\rho}{2}\sum^q_{i=1}g_i({\bf x})^2{%endmath%} </p>

+ The penalty term {%m%}\frac{\rho}{2}\sum^q_{i=1}g_i({\bf x})^2{%em%} punishes violations of the equality constraints {%m%}g_i({\bf \theta}){%em%}

+ Optimize the Augmented Lagrangian and adjust {%m%}{\bf \lambda}{%em%} in the hope of matching the true Lagrange multipliers

+ For {%m%}\rho{%em%} large enough (finite), the unconstrained minimizer of the augmented lagrangian coincides with the constrained solution of the original problem

+ At convergence, the gradient {%m%}\rho g_i({\bf x})\nabla g_i({\bf x}){%em%} vanishes and we recover the standard multiplier rule

## Algorithm

Take {%m%}\rho{%em%} initially large or gradually increase it; iterate

+ Find the unconstrained minimum

<p> {%math%}{\bf x}^{(t+1)}\leftarrow \min_x\mathcal{L}_\rho ({\bf x},{\bf \lambda}^{(t)}){%endmath%} </p>

+ Update the multiplier vector {%m%}{\bf \lambda}{%em%}

<p> {%math%}\lambda^{(t+1)}_i \leftarrow \lambda^{(t)}_i + \rho g_i({\bf x}^{(t)}), \; i = 1, \ldots , q{%endmath%} </p>

### Intuition for updating {%m%}{\bf \lambda}{%em%}

If {%m%}{\bf x}^{(t)}{%em%} is the unconstrained minimum of {%m%}\mathcal{L}({\bf x},{\bf \lambda}){%em%}, then the stationary condition says

<p>
{%math%}
\begin{align}
{\bf 0} & = \nabla f({\bf x}^{(t))} + \sum^q_{i=1} \lambda^{(t)}_i \nabla g_i({\bf x}^{(t)}) + \rho \sum^q_{i=1} g_i({\bf x}^{(t)}) \nabla g_i({\bf x}^{(t)}) \\
& = \nabla f({\bf x}^{(t))} + \sum^q_{i=1} \left[ \lambda^{(t)}_i + \rho g_i({\bf x}^{(t)}) \right] \nabla g_i({\bf x}^{(t)})
\end{align}
{%endmath%}
</p>

### For non-smooth {%m%}f{%em%}, replace gradient {%m%}\nabla f{%em%} by sub-differential {%m%}\partial f{%em%}

## Example: basis pursuit

Basis pursuit problem seeks the sparsest solution subject to linear constraints

<p>
{%math%}
\begin{align}
\text{minimize    } & \|{\bf x}\|_1 \\
\text{subject to    } & {\bf Ax} = {\bf b}
\end{align}
{%endmath%}
</p>

Take {%m%}\rho{%em%} initially large or gradually increase it; iterate according to

<p>
{%math%}
\begin{align}
{\bf x}^{(t+1)}                 & \leftarrow \min \|{\bf x}\| + \langle {\bf \lambda}^{(t)}, {\bf Ax} - {\bf b} \rangle + \frac{\rho}{2} \|{\bf Ax} - {\bf b}\|^2-2 \text{(lasso)} \\
{\bf \lambda}^{(t+1)} & \leftarrow {\bf \lambda}^{(t)} + \rho \left( {\bf Ax}^{(t+1)} - {\bf b} \right) 
\end{align}
{%endmath%}
</p>

Converges in a finite (small) number of steps {% sidenote 1 'Yin, W., Osher, S., Goldfarb, D., and Darbon, J. (2008). Bregman iterative algorithms for l<sub>1</sub>-minimization with applications to compressed sensing. SIAM J. Imaging Sci., 1(1):143-168. Online: [http://www.caam.rice.edu/~wy1/paperfiles/Rice_CAAM_TR07-13.PDF](http://www.caam.rice.edu/~wy1/paperfiles/Rice_CAAM_TR07-13.PDF)' %}

## Remarks

<p>

+ The augmented Lagrangian method dates back to 50s {% sidenote 2 'Hestenes, M.R. (1969). Multiplier and gradient methods. J. Optimization Theory Appl., 4:303-320. <br /> Powell, M. J. D. (1969). A method for nonlinear constraints in minimization problems. In Optimization (Sympos., Univ. Keele, Keele, 1968), pages 283-298. Academic Press, London.'%}
+ Monograph by Bertsekas{% sidenote 3 'Bertsekas, D. P. (1982). Constrained Optimization and Lagrange Multiplier Methods. Computer Science and Applied Mathematics. Academic Press Inc. [Harcourt Brace Jovanovich Publishers], New York.'%} provides a general treatment
+ Same as the Bregman iteration (Yin etal., 2008) proposed for basis pursuit (compressive sensing)
+ Equivalent to proximal print algorithm applied to the dual; can be accelerated (Nesterov)

</p>