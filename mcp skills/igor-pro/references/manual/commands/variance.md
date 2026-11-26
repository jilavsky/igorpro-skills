---
description: "Returns the variance of the real-valued inWave. The function ignores NaN and INF values in inWave."
slug: /commands/variance
---

<div className="command-signature">

## <strong>Variance</strong>  (<em>inWave</em> [ , <em>x1</em>, <em>x2</em> ] ) {#variance}

</div>

Returns the variance of the real-valued *inWave* . The function ignores NaN and INF values in *inWave* .

### *Parameters* {#parameters}
*inWave*  is expected to be a real-valued numeric wave. If *inWave*  is a complex or text wave, Variance returns NaN.

*x1*  and *x2*  specify a range in *inWave*  over which the variance is to be calculated. They are used only to locate the points nearest to x=*x1*  and x=*x2* . The variance is then calculated over that range of points. The order of *x1*  and *x2*  is immaterial.

If omitted, *x1*  and *x2*  default to -INF and +INF respectively and the variance is calculated for the entire wave.

### *Details* {#details}
The variance is defined by

$$
\displaystyle \operatorname{var}=\frac{\sum_{i=1}^{n}\left(x_{i}-\bar{x}\right)^{2}}{n-1}
$$

where

$$
\displaystyle \bar{x}=\frac{\sum_{i=1}^{n} X_{i}}{n} .
$$

### *Examples* {#examples}

```igor
Make/O/N=5 test = p
SetScale/P x, 0, .1, test

// Print variance of entire wave
Print Variance(test)

// Print variance from x=0 to x=.2
Print Variance(test, 0, .2)

// Print variance for points 1 through 3
Variable x1=pnt2x(test, 1)
Variable x2=pnt2x(test, 3)
Print Variance(test, x1, x2)
```

### *See Also* {#see-also}
[mean](/igorpro/commands/mean.md), [median](/igorpro/commands/median.md), [WaveStats](/igorpro/commands/wavestats.md), [APMath](/igorpro/commands/apmath.md)