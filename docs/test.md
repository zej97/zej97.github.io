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

<div id="container"></div>
<link rel="stylesheet" href="https://imsun.github.io/gitment/style/default.css">
<script src="https://imsun.github.io/gitment/dist/gitment.browser.js"></script>
<script>
var gitment = new Gitment({
    id: 'location.href',
    owner: 'zej97',
    repo: 'zej97.github.io',
    oauth: {
        client_id: '790566d6d3d3cea0463a',
        client_secret: 'd1845b571c0254dd0274f2936c3d53f672776ab8',
    },
})
gitment.render('container')
</script>
