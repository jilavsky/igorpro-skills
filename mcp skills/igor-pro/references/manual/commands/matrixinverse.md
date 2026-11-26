---
description: "The MatrixInverse operation calculates the inverse or the pseudo-inverse of a matrix. srcWave may be real or complex.."
slug: /commands/matrixinverse
---

<div className="command-signature">

## <strong>MatrixInverse</strong>  [[/D]/P][/G][/O] <em>srcWave</em> {#matrixinverse}

</div>

The MatrixInverse operation calculates the inverse or the pseudo-inverse of a matrix. *srcWave*  may be real or complex..

MatrixInverse saves the result in the wave M_Inverse in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | Creates the wave W_W that contains eigenvalues of the singular value decomposition (SVD) for the pseudo-inverse calculation. If one or more of the eigenvalues are small, the matrix may be close to singular. |
| <span class="table-cell-nowrap">/DEST = *invWave*</span> | Specify the destination of the resulting inverse matrix. If you don't use this flag, the operation saves the inverse in the wave M_Inverse in the current data folder. |
|  | The /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTW = *wWave*</span> | Specify the destination of the SVD eigenvalues wave. If you don't use this flag, the operation saves the eigenvalues in the wave W_W in the current data folder. |
|  | The /DSTW flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all specified destination waves as free waves. This flag does not affect  output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions and only if the destination, as specified by /DEST or /DSTW, is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/G</span> | Calculates only the direct inverse; does not affect calculation of pseudo-inverse. By default, it calculates the inverse of the matrix using LU decomposition. The inverse is calculated using Gauss-Jordan method. The only advantage in using the Gauss-Jordan method is that it is more likely to flag singular matrices than the LU method. |
| <span class="table-cell-nowrap">/O</span> | Overwrites the source with the result. |
| <span class="table-cell-nowrap">/P</span> | Calculates the pseudo-inverse of a matrix using the SVD algorithm. The calculated pseudo-inverse is a unique minimal solution to the problem: |
|  | $$ \displaystyle \min _{\mathbf{X} \in \mathbb{R}^{n \times m}}\left\|\mathbf{A} \mathbf{X}-I_{m}\right\| . $$ |

### *Example* {#example}

```igor
Make/O/N=(2,2) mat0 = {{2,3},{1,7}}
MatrixInverse mat0                      // Creates wave M_inverse
MatrixOp/O/T=1 mat1 = M_inverse x mat0  // Check result
Make/O/D/N=(4,6) mat1 = enoise(4)
MatrixInverse/P mat1
MatrixOP/O/T=1 aa = mat1 x M_Inverse
MatrixOP/O/P=1 avgAbsErr = sum(abs(mat1 x M_Inverse - identity(4)))/12
```

### *See Also* {#see-also}
The [MatrixOp](/igorpro/commands/matrixop.md) operation for more efficient matrix operations.

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.

### *References* {#references}
Golub, G.H., and C.F. Van Loan, *Matrix Computations*, 2nd ed., Johns Hopkins University Press, 1986. See  sec. 5.5.4.