---
title: KaTeX
layout: default
nav_order: 1
math: katex
---
# $$\KaTeX$$

You can customise Just the Docs sites to support [$$\KaTeX$$],
as explained in the [configuration suggestions]. 
Pages then render $$\LaTeX$$ code in [kramdown math blocks] using $$\KaTeX$$.

For example:

$$
\begin{aligned}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{aligned}
$$

But, since \(\varphi_{i, k}(x^{\ast})\)’s are all $\geq 0$ and $x^{\ast}_i > 0$, this means $\varphi_{i, k}(x^{\ast}) = 0$ for all $k = 1, \cdots, m_i$.  Thus, for all Player $i$, and for $j = 1, \cdots, m_i$,

$$
U_i(x^{\ast}_{-i}; \pi_{i, j}) \leq U_i(x^{\ast})
$$
