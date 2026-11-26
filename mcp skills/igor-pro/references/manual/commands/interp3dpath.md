---
description: "The Interp3DPath operation computes the trilinear interpolated values of 3dWave for each position specified by a row in tripletPathWave (which is a 3 column…"
slug: /commands/interp3dpath
---

<div className="command-signature">

## <strong>Interp3DPath</strong>  <em>dWave</em> <em>tripletPathWave</em> {#interp3dpath}

</div>

The Interp3DPath operation computes the trilinear interpolated values of *3dWave* for each position specified by a row in *tripletPathWave* (which is a 3 column wave in which the first column represents the X coordinate, the second represents the Y coordinate and the third represents the Z coordinate). Interp3DPath stores the resulting interpolated values in the wave W_Interpolated or in the specified destination wave. Interp3DPath is equivalent to calling the [Interp3D](/igorpro/commands/interp3d.md)() function for each row in *tripletPathWave,* but it is computationally more efficient.

If the position specified by the *tripletPathWave* is outside the definition of the *3dWave,* or if it contains a NaN, the operation stores a NaN in the corresponding output entry.

Both *3dWave* and *tripletPathWave* can be of any numeric type. W_Interpolated or the specified destination wave is always of type NT_FP64.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave created by the operation. It is an error to specify the same wave as *destWave* and *3dWave* or *tripletPathWave*. |
|  | When used in a function, the operation creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* (specified by /DEST) as a free wave. |
|  | /FREE is allowed only in functions, and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | This flag was added in Igor Pro 10.00. |

### *See Also* {#see-also}
[Interpolation](/igorpro/analysis/analysis.md#interpolation), [ImageInterpolate](/igorpro/commands/imageinterpolate.md) operation, [interp](/igorpro/commands/interp.md), [Interp3D](/igorpro/commands/interp3d.md), [Interp4D](/igorpro/commands/interp4d.md).