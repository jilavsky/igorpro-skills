---
description: "The centerOfMass function returns the 1D center of mass for srcWave X values from x=x1 to x=x2."
slug: /commands/centerofmass
---

<div className="command-signature">

## <strong>centerOfMass</strong> (<em>srcWave</em> [, <em>x1</em>, <em>x2</em>] ) {#centerofmass}

</div>

The centerOfMass function returns the 1D center of mass for *srcWave* X values from x=*x1* to x=*x2*.

The centerOfMass function was added in Igor Pro 9.00.

Center of mass and center of gravity in a uniform gravity field are different terms for the same calculation. When the masses are of uniform density, the center of mass is also identical to the geometric centroid.

### *Details* {#details}
The center of mass is defined as

$$
\displaystyle \text { centerMass }=\frac{\sum x_{i} y_{i}}{\sum y_{i}},
$$

where the summation is over all the points in *srcWave* or over the X range specified by the optional parameters *x1* and *x2*.

Each term in the numerator above can be written as

$$
\displaystyle x_{i} y_{i}=[\operatorname{DimOffset}(\operatorname{srcWave}, 0)+i \cdot \operatorname{DimDelta}(\operatorname{srcWave}, 0)] \operatorname{srcWave}[i] .
$$

In this notation, *y*<sub>i</sub> represents an individual mass at x = *x*<sub>i</sub>, and the returned value *x*<sub>c</sub> is the X location of the center of the aggregate mass.

### *See Also* {#see-also}
[centerOfMassXY](/igorpro/commands/centerofmassxy.md), [mean](/igorpro/commands/mean.md), [area](/igorpro/commands/area.md), [SumDimension](/igorpro/commands/sumdimension.md), [ImageAnalyzeParticles](/igorpro/commands/imageanalyzeparticles.md)