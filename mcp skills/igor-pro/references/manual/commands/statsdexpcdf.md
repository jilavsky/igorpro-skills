---
description: "The StatsDExpCDF function returns the double-exponential cumulative distribution function."
slug: /commands/statsdexpcdf
---

<div className="command-signature">

## <strong>StatsDExpCDF</strong> (<em>x</em>, µ, σ) {#statsdexpcdf}

</div>

The StatsDExpCDF function returns the double-exponential cumulative distribution function

$$
F(x ; \mu, \sigma)=\left\{\begin{array}{ll}
\displaystyle \exp \left(\frac{x-\mu}{\sigma}\right) & \text { when } x<\mu \\
\\
\displaystyle 1-\frac{1}{2} \exp \left(-\left|\frac{x-\mu}{\sigma}\right|\right) & \text { when } x \geq \mu
\end{array}\right.
$$

where σ>0. It returns NaN if σ=0.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsDExpPDF](/igorpro/commands/statsdexppdf.md), [StatsInvDExpCDF](/igorpro/commands/statsinvdexpcdf.md)