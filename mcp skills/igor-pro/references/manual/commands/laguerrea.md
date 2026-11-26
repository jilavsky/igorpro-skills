---
description: "The LaguerreA function returns the associated Laguerre polynomial of degree n (positive integer), index k (nonnegative integer) and argument x."
slug: /commands/laguerrea
---

<div className="command-signature">

## <strong>laguerreA</strong> (<em>n</em>, <em>k</em>, <em>x</em>) {#laguerrea}

</div>

The LaguerreA function returns the associated Laguerre polynomial of degree *n* (positive integer), index *k* (nonnegative integer) and argument *x*. The associated Laguerre polynomials are defined by

$$
\displaystyle L_{n}^{k}(x)=(-1)^{k} \frac{d^{k}}{d x^{k}}\left[L_{n+k}(x)\right],
$$

where 
$$
\displaystyle L_{n+k}(x)
$$
<sub> </sub>is the Laguerre polynomial.

### *See Also* {#see-also}
[laguerre](/igorpro/commands/laguerre.md), [laguerreGauss](/igorpro/commands/laguerregauss.md)

### *References* {#references}
Arfken, G., *Mathematical Methods for Physicists*, Academic Press, New York, 1985.