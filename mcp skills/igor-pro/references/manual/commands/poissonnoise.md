---
description: "The poissonNoise function returns a pseudo-random value from the Poisson distribution whose probability distribution function is."
slug: /commands/poissonnoise
---

<div className="command-signature">

## <strong>poissonNoise</strong> (<em>num</em>) {#poissonnoise}

</div>

The poissonNoise function returns a pseudo-random value from the Poisson distribution whose probability distribution function is

$$
\displaystyle f(x ; \lambda)=\frac{e^{-\lambda} \lambda^{x}}{x!}, \quad \begin{array}{c}
\lambda>0 \\
x=0,1,2 \ldots
\end{array}
$$

with mean and variance equal to *num* (= λ).

The random number generator initializes using the system clock when Igor Pro starts. This almost guarantees that you will never repeat a sequence. For repeatable "random" numbers, use [SetRandomSeed](/igorpro/commands/setrandomseed.md). The algorithm uses the Mersenne Twister random number generator.

### *See Also* {#see-also}
[SetRandomSeed](/igorpro/commands/setrandomseed.md), [Noise Functions](/igorpro/analysis/statistics.md#noise-functions), [Statistical Analysis](/igorpro/analysis/statistics.md)