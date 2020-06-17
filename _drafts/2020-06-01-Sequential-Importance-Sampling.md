<script>
MathJax = {
  tex: {
    inlineMath: [['$', '$'], ['\\(', '\\)']]
  },
  svg: {
    fontCache: 'global'
  }
};
</script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js">
</script>

## Goal
We wan to compute some expectations over the posterior distribution: 
$$I = {E}[{g}({x}) | {y}_{1: T}]=\int {g}({x}) p({x} | {y}_{1: T}) {d} {x}$$

**Examples**:　　  
The posterior probability density $I = p(x'|y_{1:t})=\int \delta(x-x') p(x|y_{1:t})dx$

## Mathod 1: Sequential Importance Sampling
We can not draw samples directly over p(x), then we want to approximate $I$ with importance sampling.

$$\begin{aligned}
I &=\int \mathbf{g}(\mathbf{x}) p\left(\mathbf{x} | \mathbf{y}_{1: T}\right) \mathrm{d} \mathbf{x} \\
&=\frac{\int \mathbf{g}(\mathbf{x}) p\left(\mathbf{y}_{1: T} | \mathbf{x}\right) p(\mathbf{x}) \mathrm{d} \mathbf{x}}{\int p\left(\mathbf{y}_{1: T} | \mathbf{x}\right) p(\mathbf{x}) \mathrm{d} \mathbf{x}}\\
&=\frac{\int\left[\frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}\right) p(\mathbf{x})}{\pi\left(\mathbf{x} | \mathbf{y}_{1: T}\right)} \mathbf{g}(\mathbf{x})\right] \pi\left(\mathbf{x} | \mathbf{y}_{1: T}\right) \mathrm{d} \mathbf{x}}{\int\left[\frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}\right) p(\mathbf{x})}{\pi\left(\mathbf{x} | \mathbf{y}_{1: T}\right)}\right] \pi\left(\mathbf{x} | \mathbf{y}_{1: T}\right) \mathrm{d} \mathbf{x}}\\
&\approx \frac{\frac{1}{N} \sum_{i=1}^{N} \frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}^{(i)}\right) p\left(\mathbf{x}^{(i)}\right)}{\pi\left(\mathbf{x}^{(i)} | \mathbf{y}_{1: T}\right)} \mathbf{g}\left(\mathbf{x}^{(i)}\right)}{\frac{1}{N} \sum_{j=1}^{N} \frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}^{(j)}\right) p\left(\mathbf{x}^{(j)}\right)}{\pi\left(\mathbf{x}^{(j)} | \mathbf{y}_{1: T}\right)}} \\
&=\sum_{i=1}^{N}\left[\frac{\frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}^{(i)}\right) p\left(\mathbf{x}^{(i)}\right)}{\pi\left(\mathbf{x}^{(i)} | \mathbf{y}_{1: T}\right)}}{\sum_{j=1}^{N} \frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}^{(j)}\right) p\left(\mathbf{x}^{(j))}\right.}{\pi\left(\mathbf{x}^{(j)} | \mathbf{y}_{1: T}\right)}}\right]
\end{aligned}$$
