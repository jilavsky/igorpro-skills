---
description: "The binomialNoise function returns a pseudo-random value from the binomial distribution."
slug: /commands/binomialnoise
---

<div className="command-signature">

## <strong>binomialNoise</strong> (<em>n</em>, <em>p</em>) {#binomialnoise}

</div>

The binomialNoise function returns a pseudo-random value from the binomial distribution

$$
\displaystyle f(x)=\binom{n}{x} p^{x}(1-p)^{n-x}, \quad \begin{array}{c} 0 \leq p \leq 1 \\ x=0,1,2 \ldots n \end{array}
$$

whose mean is *np* and variance is 
$$
\displaystyle n p(1-p) .
$$
<sub></sub>

When n is large such that p<sup>n</sup> is zero to machine accuracy the function returns NaN. Note that when n is large such that np(1-p) > 5 and 0.1 < p < 0.9 you can replace the binomial variate with a normal variate with mean np and standard deviation sqrt(n\*p\*(1-p)).

The random number generator  initializes using the system clock when Igor Pro starts. This almost guarantees that you will never repeat the same sequence. For repeatable "random" numbers, use [SetRandomSeed](/igorpro/commands/setrandomseed.md). The algorithm uses the Mersenne Twister random number generator..

### *See Also* {#see-also}
[SetRandomSeed](/igorpro/commands/setrandomseed.md), [Noise Functions](/igorpro/analysis/statistics.md#noise-functions), [Statistical Analysis](/igorpro/analysis/statistics.md)