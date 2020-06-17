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
## From Importance Sampling to Particle Filter
## Goal

Suppose we want to calculate a quantity $I = \int h(x) dx$.

## Method 1: Monte Carlo integration
1. Find a probability distribution $f$ which satisfies $I = \int h(x) dx = \int h(x)f(x) dx$.
1. Generate $N$ samples $X_{1}, \ldots, X_{N} \sim f$ independently.
2. $\hat{I} \triangleq \frac{1}{N} \sum_{i=1}^{N} h(X_{i})$. According to the law of large numbers, we have $I \approx \hat{I}$.

Monte carlo sampling, 

$\hat{I}$ is the Monte Carlo approximation of $I$.

**Cons**  

1. When h(x) is near zero outside a region $A$, and f(x) is near zero inside the region A, we might generate zero samples inside the region $A$, result in a inefficient sampling process. How can we generates more samples inside the important region $A$?
2. In some cases, we can not sample directly from f. 

## Method 2: Importance Sampling

To address the issues we mentioned above, we introduce a proposal distribution $g(x)$ which satisfies $g(x)=0 \Longrightarrow f(x) = 0$, then the following equation holds,

$$I=\int h(x) f(x) d x=\int h(x) \frac{f(x)}{g(x)} g(x) d x=\mathbb{E}_{g}(h(x) \frac{f(x)}{g(x)})$$

1. Generate $N$ samples $X_{1}, \ldots, X_{N} \sim g$ independently.
2. $\hat{I} \triangleq\frac{1}{N} \sum_{i} \frac{h(X_{i}) f(X_{i})}{g(X_{i})}$, we have $I \approx \hat{I}$.

This approximation process is called importance sampling. $\frac{f(x)}{g(x)}$ is called the importance weight.

With importance sampling, we can choose a g(x) which is large inside the important region $A$, therefore, we could generate more samples inside the region $A$.

References:
1. Larry Wasserman, All of Statistics: A Concise Course in Statistical Inference, Corrected second printing, 2005, Springer Texts in Statistics (New York, NY: Springer, 2010). Chapter 24.3
2. [Importance Sampling 1](https://statweb.stanford.edu/~owen/mc/Ch-var-is.pdf)
3. [Importance Sampling 2](http://www.math.chalmers.se/Stat/Grundutb/CTH/tms150/1112/MC.pdf)
4. [Importance Sampling 3](http://ib.berkeley.edu/labs/slatkin/eriq/classes/guest_lect/mc_lecture_notes.pdf)
5. [Importance Sampling 4](http://www.math.chalmers.se/Stat/Grundutb/CTH/tms150/1415/MC_20141008.pdf)

## Applications

### Approximate posterior distribution by importance sampling

We wan to compute some expectations over the posterior distribution: 
$$I = {E}[{g}({x}) | {y}_{1: T}]=\int {g}({x}) p({x} | {y}_{1: T}) {d} {x}$$


$$\begin{aligned}
I &=\int \mathbf{g}(\mathbf{x}) p\left(\mathbf{x} | \mathbf{y}_{1: T}\right) \mathrm{d} \mathbf{x} \\
&=\frac{\int \mathbf{g}(\mathbf{x}) p\left(\mathbf{y}_{1: T} | \mathbf{x}\right) p(\mathbf{x}) \mathrm{d} \mathbf{x}}{\int p\left(\mathbf{y}_{1: T} | \mathbf{x}\right) p(\mathbf{x}) \mathrm{d} \mathbf{x}}\\
&=\frac{\int\left[\frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}\right) p(\mathbf{x})}{\pi\left(\mathbf{x} | \mathbf{y}_{1: T}\right)} \mathbf{g}(\mathbf{x})\right] \pi\left(\mathbf{x} | \mathbf{y}_{1: T}\right) \mathrm{d} \mathbf{x}}{\int\left[\frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}\right) p(\mathbf{x})}{\pi\left(\mathbf{x} | \mathbf{y}_{1: T}\right)}\right] \pi\left(\mathbf{x} | \mathbf{y}_{1: T}\right) \mathrm{d} \mathbf{x}}\\
&\approx \frac{\frac{1}{N} \sum_{i=1}^{N} \frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}^{(i)}\right) p\left(\mathbf{x}^{(i)}\right)}{\pi\left(\mathbf{x}^{(i)} | \mathbf{y}_{1: T}\right)} \mathbf{g}\left(\mathbf{x}^{(i)}\right)}{\frac{1}{N} \sum_{j=1}^{N} \frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}^{(j)}\right) p\left(\mathbf{x}^{(j)}\right)}{\pi\left(\mathbf{x}^{(j)} | \mathbf{y}_{1: T}\right)}} \\
&=\sum_{i=1}^{N}\left[\frac{\frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}^{(i)}\right) p\left(\mathbf{x}^{(i)}\right)}{\pi\left(\mathbf{x}^{(i)} | \mathbf{y}_{1: T}\right)}}{\sum_{j=1}^{N} \frac{p\left(\mathbf{y}_{1: T} | \mathbf{x}^{(j)}\right) p\left(\mathbf{x}^{(j))}\right.}{\pi\left(\mathbf{x}^{(j)} | \mathbf{y}_{1: T}\right)}}\right]
\end{aligned}$$

Then the steps is summerized in the following [picture](https://users.aalto.fi/~ssarkka/pub/cup_book_online_20131111.pdf) (P. 120)

![](./000_imgs/2020-06-01-Sequential-Importance-Sampling_2020-06-01-16-30-33.png =400x)

**Examples:**
We can use the importance sampling to approximate the posterior probability density.

$$p\left(\mathbf{x} | \mathbf{y}_{1: T}\right) =\int \delta(x-x') p(x|y_{1:t})dx
 \approx \sum_{i=1}^{N} w^{(i)} \delta\left(\mathbf{x}-\mathbf{x}^{(i)}\right)$$



## Sequential importance sampling

references: 
[BAYESIAN FILTERING AND SMOOTHING](https://users.aalto.fi/~ssarkka/pub/cup_book_online_20131111.pdf)
[reference 2](https://users.aalto.fi/~ssarkka/course_k2012/handout6.pdf)
[reference 3](http://www.stat.cmu.edu/~larry/=sml/Bayes.pdf)