---
description: "The StatsInvDExpCDF function returns the inverse of the double-exponential cumulative distribution function."
slug: /commands/statsinvdexpcdf
---

<div className="command-signature">

## <strong>StatsInvDExpCDF</strong> (<em>cdf</em>, µ, σ) {#statsinvdexpcdf}

</div>

The StatsInvDExpCDF function returns the inverse of the double-exponential cumulative distribution function

$$
\displaystyle x=\left\{\begin{array}{ll}
\mu+\sigma \ln (2 c d f) & \text { when } c d f<0.5 \\
\\
\mu-\sigma \ln [2(1-c d f)] & \text { when } c d f \geq 0.5
\end{array}\right.
$$

It returns NaN for *cdf* <0 or *cdf* > 1.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsDExpPDF](/igorpro/commands/statsdexppdf.md), [StatsDExpCDF](/igorpro/commands/statsdexpcdf.md)