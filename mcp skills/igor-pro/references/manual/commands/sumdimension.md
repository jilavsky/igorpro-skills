---
description: "The SumDimension operation sums values in srcWave along the specified dimension."
slug: /commands/sumdimension
---

<div className="command-signature">

## <strong>SumDimension</strong>  [/D=<em>dimension</em>  /DEST=<em>destWave</em>  /Y=<em>numType</em> ] <em>srcWave</em> {#sumdimension}

</div>

The SumDimension operation sums values in *srcWave* along the specified dimension.

The SumDimension operation was added in Igor Pro 7.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D = *dimension*</span> | Specifies a zero-based dimension number. |
|  |<table class="nested-table"><tbody><tr><td>*dimension*&nbsp;=0:</td><td>Rows</td></tr><tr><td>*dimension*&nbsp;=1:</td><td>Columns</td></tr><tr><td>*dimension*&nbsp;=2:</td><td>Layers</td></tr><tr><td>*dimension*&nbsp;=3:</td><td>Chunks</td></tr></tbody></table>
|  | If you omit /D the operation sums the highest dimension in the wave. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave created by the operation. If *destWave* already exists it is overwritten by the new results. |
|  | If you omit /DEST the operation saves the data in W_SumDimension if the output wave is 1D or M_SumDimension otherwise. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Y = *type*</span> | Specifies the data type of the output wave. See [WaveType](/igorpro/commands/wavetype.md) for the supported values of *type*. |
|  | If you omit /Y, the output wave is double precision. |
|  | Pass -1 for *type* to force the output wave to have the same data type as *srcWave*. |

### *Details* {#details}
The operation sums one dimension of an N dimensional wave producing an output wave with N-1 dimensions except if *srcWave* is 1D wave in which case SumDimension produces a single point 1D output wave. For example, given a 4D wave of dimensions dim0 x dim1 x dim2 x dim3 and the command:


```igor
SumDimension/D=1/DEST=wout wave4d
```

creates a wave wout that satisfies

$$
\displaystyle { wout }[i][k][l]=\sum_{j=0}^{\operatorname{dim} 1-1} { wave4d }[i][j][k][l],
$$

and wout has dimensions dim0 x dim2 x dim3.

If any values in *srcWave* are NaN, the corresponding sum element will be NaN.

### *See Also* {#see-also}
[sum](/igorpro/commands/sum.md)

[MatrixOp](/igorpro/commands/matrixop.md) keywords sumRows, sumCols, sumBeams

[ImageTransform](/igorpro/commands/imagetransform.md) keywords sumAllCols, sumAllRows, sumPlane, sumPlanes