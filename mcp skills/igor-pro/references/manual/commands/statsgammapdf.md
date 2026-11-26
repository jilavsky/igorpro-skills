---
description: "Returns the gamma probability distribution function (PDF) given by $$ f(x; \\mu, \\sigma, \\gamma)=\\frac{\\displaystyle…"
slug: /commands/statsgammapdf
---

<div className="command-signature">

## <strong>StatsGammaPDF</strong> (<em>x</em>, µ, σ, γ) {#statsgammapdf}

</div>

Returns the gamma probability distribution function (PDF) given by

$$
f(x ; \mu, \sigma, \gamma)=\frac{\displaystyle \left(\frac{x-\mu}{\sigma}\right)^{\gamma-1} \exp \left(-\frac{x-\mu}{\sigma}\right)}{\sigma \Gamma(\gamma)} . \quad \quad \begin{array}{c} x \geq \mu \\ \sigma,\gamma \gt 0  \end{array}
$$

where  *µ* is the location parameter, *σ* is the scale parameter, γ is the shape parameter, and Γ is the [gamma](/igorpro/commands/gamma.md) function.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsGammaCDF](/igorpro/commands/statsgammacdf.md), [StatsInvGammaCDF](/igorpro/commands/statsinvgammacdf.md)