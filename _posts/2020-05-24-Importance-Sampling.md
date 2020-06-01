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

Suppose we want to calculate a quantity $I = \int h(x) dx$.

## Method 1: Monte Carlo integration
1. Find a probability distribution $f$ which satisfies $I = \int h(x) dx = \int h(x)f(x) dx$.
1. Generate $N$ samples $X_{1}, \ldots, X_{N} \sim f$ independently.
2. $\hat{I} \triangleq \frac{1}{N} \sum_{i=1}^{N} h(X_{i})$. According to the law of large numbers, we have $I \approx \hat{I}$.

$\hat{I}$ is the Monte Carlo approximation of $I$.

**Cons**  

1. When h(x) is near zero outside a region $A$, and f(x) is near zero inside the region A, we might generate zero samples inside the region $A$, result in a inefficient sampling process. How can we generates more samples inside the important region $A$?
2. In some cases, we can not sample directly from f. 

## Method 2: Importance Sampling

To address the issues we mentioned above, we introduce a proposal distribution $g(x)$ which satisfies $g(x)=0 \Longrightarrow f(x) = 0$, then the following equation holds,

$$I=\int h(x) f(x) d x=\int h(x) \frac{f(x)}{g(x)} g(x) d x=\mathbb{E}_{g}(h(x) \frac{f(x)}{g(x)})$$

1. Generate $N$ samples $X_{1}, \ldots, X_{N} \sim g$ independently.
2. $\hat{I} \triangleq\frac{1}{N} \sum_{i} \frac{h(X_{i}) f(X_{i})}{g(X_{i})}$, we have $I \approx \hat{I}$.

This approximation process is called importance sampling.

With importance sampling, we can choose a g(x) which is large inside the important region $A$, therefore, we could generate more samples inside the region $A$.

References:
1. Larry Wasserman, All of Statistics: A Concise Course in Statistical Inference, Corrected second printing, 2005, Springer Texts in Statistics (New York, NY: Springer, 2010). Chapter 24.3
2. [Importance Sampling 1](https://statweb.stanford.edu/~owen/mc/Ch-var-is.pdf)
3. [Importance Sampling 2](http://www.math.chalmers.se/Stat/Grundutb/CTH/tms150/1112/MC.pdf)
4. [Importance Sampling 3](http://ib.berkeley.edu/labs/slatkin/eriq/classes/guest_lect/mc_lecture_notes.pdf)
5. [Importance Sampling 4](http://www.math.chalmers.se/Stat/Grundutb/CTH/tms150/1415/MC_20141008.pdf)