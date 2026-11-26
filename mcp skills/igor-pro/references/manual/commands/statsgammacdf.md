---
description: "Returns the gamma cumulative distribution function (CDF) given by $$ \\displaystyle F(x; \\mu, \\sigma, \\gamma)=\\frac{\\Gamma_{\\text {inc }}\\left(\\gamma…"
slug: /commands/statsgammacdf
---

<div className="command-signature">

## <strong>StatsGammaCDF</strong> (<em>x</em>, µ, σ, γ) {#statsgammacdf}

</div>

Returns the gamma cumulative distribution function (CDF) given by

$$
\displaystyle F(x ; \mu, \sigma, \gamma)=\frac{\Gamma_{\text {inc }}\left(\gamma, \frac{x-\mu}{\sigma}\right)}{\Gamma(\gamma)} . \quad \begin{array}{c} x \geq \mu \\ \sigma,\gamma > 0 \end{array}
$$

where Γ is the [gamma](/igorpro/commands/gamma.md) function and Γ<sub>inc</sub> is the incomplete gamma function [gammaInc](/igorpro/commands/gammainc.md)(γ,(x-*µ*)/*σ,* 0).

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsGammaPDF](/igorpro/commands/statsgammapdf.md), [StatsInvGammaCDF](/igorpro/commands/statsinvgammacdf.md)