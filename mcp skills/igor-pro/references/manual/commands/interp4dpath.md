---
description: "The Interp4DPath operation computes the (4D) linearly interpolated values of 4dWave for each position specified by a row of pathWave."
slug: /commands/interp4dpath
---

<div className="command-signature">

## <strong>Interp4DPath</strong>  <em>dWave</em>, <em>pathWave</em> {#interp4dpath}

</div>

The Interp4DPath operation computes the (4D) linearly interpolated values of *4dWave* for each position specified by a row of p*athWave*. Here *pathWave* is a 4 column numeric wave in which the first column contains the X coordinate, the second column contains the Y coordinate, the third column contains the Z coordinate and the fourth contains the T coordinate. Interp4DPath stores the resulting interpolated values in the wave W_Interpolated4DPath or as specified by the /DEST flag.  Interp4DPath is equivalent to calling the [Interp4D](/igorpro/commands/interp4d.md)() function for each row in *pathWave,* but it is computationally more efficient.

If the position specified by the *pathWave* is outside the domain of *4dWave*, or if it contains a NaN, the operation stores a NaN in the corresponding output entry.

Both *4dWave* and *pathWave* can be of any numeric type, but the output W_Interpolated4DPath is always of type NT_FP64.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *dWave*</span> | Specify the destination wave for the interpolation.  If you do not use this flag, the operation saves the output in the wave W_Interpolated4DPath in the current data folder. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |

### *See Also* {#see-also}
[Interpolation](/igorpro/analysis/analysis.md#interpolation) overview.  The [ImageInterpolate](/igorpro/commands/imageinterpolate.md), [Interpolate2](/igorpro/commands/interpolate2.md), [Interp3DPath](/igorpro/commands/interp3dpath.md), [Interpolate3D](/igorpro/commands/interpolate3d.md), [SphericalInterpolate](/igorpro/commands/sphericalinterpolate.md), operations and the [interp](/igorpro/commands/interp.md), [Interp2D](/igorpro/commands/interp2d.md), [Interp3D](/igorpro/commands/interp3d.md), and [Interp4D](/igorpro/commands/interp4d.md) functions.