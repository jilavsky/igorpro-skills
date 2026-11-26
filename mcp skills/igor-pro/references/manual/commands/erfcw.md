---
description: "The erfcw is a complex form of the error function defined by $$ \\displaystyle \\operatorname{erfcw}(z)=\\exp \\left[-z^{2}\\right] \\operatorname{erfc}(-i z), $$."
slug: /commands/erfcw
---

<div className="command-signature">

## <strong>erfcw</strong> (<em>z</em> ) {#erfcw}

</div>

The erfcw is a complex form of the error function defined by

$$
\displaystyle \operatorname{erfcw}(z)=\exp \left[-z^{2}\right] \operatorname{erfc}(-i z),
$$

where

$$
\displaystyle \operatorname{erfc}(z)=\frac{2}{\sqrt{\pi}} \int_{z}^{\infty} \exp \left[-t^{2}\right] d t.
$$

The function is computed with accuracy of 0.5e-10. It is particularly useful for large |*z*| where the computation of *erfc(z)* starts encountering numerical instability.

### *References* {#references}

1. [http://en.wikipedia.org/wiki/Error_function](http://en.wikipedia.org/wiki/Error_function)


2. W. Gautschi, "Efficient Computation of the Complex Error Function", SIAM J. Numer. Anal. Vol. 7, No. 1, March 1970.

### *See Also* {#see-also}
[erf](/igorpro/commands/erf.md), [erfc](/igorpro/commands/erfc.md), [erfcx](/igorpro/commands/erfcx.md), [inverseErfc](/igorpro/commands/inverseerfc.md), [dawson](/igorpro/commands/dawson.md)