---
description: "Returns the error probability distribution function (PDF) also known as the exponential power distribution. It is given by."
slug: /commands/statserrorpdf
---

<div className="command-signature">

## <strong>StatsErrorPDF</strong> (<em>x</em>, <em>a</em>, <em>b</em>, <em>c</em>) {#statserrorpdf}

</div>

Returns the error probability distribution function (PDF) also known as the exponential power distribution.  It is given by

$$
f(x ; a, b, c)=\frac{\exp \left[-\frac{1}{2}\left(\frac{|x-a|}{b}\right)^{\frac{2}{c}}\right]}{\displaystyle b 2^{\frac{c}{2}+1} \Gamma\left(1+\frac{c}{2}\right)} .
$$

where *a*  is the location parameter,  *b* > 0 is the scale parameter, *c* > 0 is the shape parameter, and Γ(x) is the [Gamma](/igorpro/commands/gamma.md) function.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md)