---
description: "Returns the Erlang cumulative distribution function (CDF) given by $$ F(x; b, c)=1-\\frac{\\displaystyle \\Gamma\\left(c, \\frac{x}{b}\\right)}{\\Gamma(c)}."
slug: /commands/statserlangcdf
---

<div className="command-signature">

## <strong>StatsErlangCDF</strong> (<em>x</em>, <em>b</em>, <em>c</em>) {#statserlangcdf}

</div>

Returns the Erlang cumulative distribution function (CDF) given by

$$
F(x ; b, c)=1-\frac{\displaystyle \Gamma\left(c, \frac{x}{b}\right)}{\Gamma(c)} .
$$

where the scale parameter *b* > 0 (sometimes appears as λ=1/b), the shape parameter is *c* > 0, Γ(x) is the [Gamma](/igorpro/commands/gamma.md) function and Γ(a,x) is the incomplete Gamma function [gammaInc](/igorpro/commands/gammainc.md).

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsErlangPDF](/igorpro/commands/statserlangpdf.md)