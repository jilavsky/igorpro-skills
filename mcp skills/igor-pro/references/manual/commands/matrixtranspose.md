---
description: "The MatrixTranspose operation swaps rows and columns in the matrix. Does not take complex conj if complex data. You can do that as a follow-on step."
slug: /commands/matrixtranspose
---

<div className="command-signature">

## <strong>MatrixTranspose</strong>  [/H] <em>matrix</em> {#matrixtranspose}

</div>

The MatrixTranspose operation swaps rows and columns in the matrix.

Does not take complex conj if complex data. You can do that as a follow-on step.

Swaps row and column labels, units and scaling.

This works with text as well as numeric waves. If the matrix has zero data points, it just swaps the row and column scaling.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *tWave*</span> | Saves the transpose in *tWave*. If this flag is not specified, the operation overwrites the input matrix with the computed transpose. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination wave is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/H</span> | Computes the Hermitian conjugate of a complex wave. |

### *See Also* {#see-also}
The [MatrixOp](/igorpro/commands/matrixop.md) operation for more efficient matrix operations.

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.