---
description: "The centerOfMassXY function returns the 1D center of mass for the pair of waves."
slug: /commands/centerofmassxy
---

<div className="command-signature">

## <strong>centerOfMassXY</strong> (<em>waveX</em>, <em>waveY</em>) {#centerofmassxy}

</div>

The centerOfMassXY function returns the 1D center of mass for the pair of waves.

The centerOfMassXY function was added in Igor Pro 9.00.

You can obtain the center of mass in the orthogonal direction (*y*<sub>c</sub>) by reversing the order of arguments to the function.

### *Details* {#details}
The center of mass is defined as

$$
\displaystyle \text { centerMassXY }=\frac{\sum { waveX }[i] { waveY } [i]}{\sum{ waveY } [i]} .
$$

### *See Also* {#see-also}
[centerOfMass](/igorpro/commands/centerofmass.md), [mean](/igorpro/commands/mean.md), [areaXY](/igorpro/commands/areaxy.md), [SumDimension](/igorpro/commands/sumdimension.md), [ImageAnalyzeParticles](/igorpro/commands/imageanalyzeparticles.md)