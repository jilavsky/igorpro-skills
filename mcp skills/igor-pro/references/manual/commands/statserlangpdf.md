---
description: "Returns the Erlang probability distribution function (PDF) given by $$ f(x; b, c)=\\frac{\\displaystyle \\left(\\frac{x}{b}\\right)^{c-1} \\exp…"
slug: /commands/statserlangpdf
---

<div className="command-signature">

## <strong>StatsErlangPDF</strong> (<em>x</em>, <em>b</em>, <em>c</em>) {#statserlangpdf}

</div>

Returns the Erlang probability distribution function (PDF) given by

$$
f(x ; b, c)=\frac{\displaystyle \left(\frac{x}{b}\right)^{c-1} \exp \left(-\frac{x}{b}\right)}{b(c-1)!} .
$$

where the scale parameter *b* > 0 (sometimes appears as λ=1/b) and the shape parameter is *c* > 0.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsErlangCDF](/igorpro/commands/statserlangcdf.md)