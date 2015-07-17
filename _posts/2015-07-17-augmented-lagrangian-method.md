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

<!--more-->
