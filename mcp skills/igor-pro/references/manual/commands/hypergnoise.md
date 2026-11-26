---
description: "The hyperGNoise function returns a pseudo-random value from the hypergeometric distribution whose probability distribution function is."
slug: /commands/hypergnoise
---

<div className="command-signature">

## <strong>hyperGNoise</strong> (<em>m</em>, <em>n</em>, <em>k</em>) {#hypergnoise}

</div>

The hyperGNoise function returns a pseudo-random value from the hypergeometric distribution whose probability distribution function is

$$
f(x ; m, n, k)=\frac{\displaystyle \binom{n}{x}\binom{m-n}{k-x}}{\displaystyle \binom{m}{k}},
$$

where *m* is the total number of items, *n* is the number of marked items, and *k* is the number of items in a sample.

The random number generator initializes using the system clock when Igor Pro starts. This almost guarantees that you will never repeat a sequence. For repeatable "random" numbers, use [SetRandomSeed](/igorpro/commands/setrandomseed.md). The algorithm uses the Mersenne Twister random number generator.

### *See Also* {#see-also}
[SetRandomSeed](/igorpro/commands/setrandomseed.md), [StatsHyperGPDF](/igorpro/commands/statshypergpdf.md), [StatsHyperGCDF](/igorpro/commands/statshypergcdf.md), [Noise Functions](/igorpro/analysis/statistics.md#noise-functions), [Statistical Analysis](/igorpro/analysis/statistics.md)