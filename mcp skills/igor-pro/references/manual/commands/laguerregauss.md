---
description: "The LaguerreGauss function returns the normalized product of the associated Laguerre polynomials and a Gaussian."
slug: /commands/laguerregauss
---

<div className="command-signature">

## <strong>laguerreGauss</strong> (<em>p</em>, <em>m</em>, <em>r</em>) {#laguerregauss}

</div>

The LaguerreGauss function returns the normalized product of the associated Laguerre polynomials and a Gaussian. This function is typically encountered in solutions to physical problems where it represents the radial solution with an additional factor exp(i*m*φ) which is not included in this case. The laguerreGauss is given by

$$
\displaystyle U_{p m}(r)=\sqrt{\frac{2 p!}{\pi(m+p)!}}(r \sqrt{2})^{m} L_{p}^{m}\left(2 r^{2}\right) \exp \left(-r^{2}\right) .
$$

### *See Also* {#see-also}
[laguerre](/igorpro/commands/laguerre.md), [laguerreA](/igorpro/commands/laguerrea.md), [hermiteGauss](/igorpro/commands/hermitegauss.md)