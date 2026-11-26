---
description: "The sphericalHarmonics function returns the complex-valued spherical harmonics."
slug: /commands/sphericalharmonics
---

<div className="command-signature">

## <strong>sphericalHarmonics</strong> (<em>L</em>, <em>M</em>, θ, φ) {#sphericalharmonics}

</div>

The sphericalHarmonics function returns the complex-valued spherical harmonics

$$
\displaystyle Y_{L}^{M}(\theta, \phi)=(-1)^{M} \sqrt{\frac{2 L+1}{4 \pi} \frac{(L-M)!}{(L+M)!}} P_{L}^{M}(\cos (\theta)) e^{i M \phi},
$$

where 
$$
\displaystyle P_{L}^{M}(\cos (\theta))
$$
 is the associated Legendre function.

### *See Also* {#see-also}
[legendreA](/igorpro/commands/legendrea.md)

### *Demos* {#demos}
[Open Spherical Harmonics Demo](#igor-pxp/Examples/Visualization/SphericalHarmonicsDemo.pxp)

[Open Numerical Integation Demo](#igor-pxp/Examples/Analysis/NumericalIntegrationDemo.pxp)

### *References* {#references}
Arfken, G., *Mathematical Methods for Physicists*, Academic Press, New York, 1985.