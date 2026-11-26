---
description: "The MatrixGaussJ operation solves matrix expression A*x=b for column vector x given matrix A and column vector b."
slug: /commands/matrixgaussj
---

<div className="command-signature">

## <strong>MatrixGaussJ</strong>  <em>matrixA</em> , <em>vectorB</em> {#matrixgaussj}

</div>

The MatrixGaussJ operation solves matrix expression A\*x=b for column vector x given matrix A and column vector b. The operation can also be used to calculate the inverse of a matrix.

### *Parameters* {#parameters}
A should be an NxN matrix of coefficients and b contains an NxM set of right-hand side vectors.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSTI = *destInv*</span> | Specifies the output destingation of the inverse matrix.  If this flag is not used, the operation saves the inverse in the wave M_inverse in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTX = *destX*</span> | Specifies the output of the solution vector.  If this flag is not used, the operation saves the solution vector in the wave M_x in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all specified destination waves as free waves. This flag does not affect output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions and only if the destination waves, as specified by /DSTI and /DSTX, are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |

### *Details* {#details}
On output, the array of solution vectors x is placed in M_x and the inverse of A is placed in M_inverse.

If the result is a singular matrix, V_flag is set to 1 to indicate the error. All other errors result in an alert, and abort any calling procedure.

All output objects are created in the current data folder.

An error is generated if the dimensioning of the input arrays is invalid.

This routine is provided for completeness only and is not recommended for general work (use LU decomposition -- see [MatrixLUD](/igorpro/commands/matrixlud.md)). MatrixGaussJ does calculate the inverse matrix but that is not generally needed either.

### *See Also* {#see-also}
[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.