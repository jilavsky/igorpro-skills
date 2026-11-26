---
description: "The MatrixLUD operation computes the LU factorization of a matrix. The general form of the factorization/decomposition is expressed in terms of matrix products."
slug: /commands/matrixlud
---

<div className="command-signature">

## <strong>MatrixLUD</strong>  [/B /CMF /PMAT /MIND /SUMP] <em>srcWave</em> {#matrixlud}

</div>

The MatrixLUD operation computes the LU factorization of a matrix. The general form of the factorization/decomposition is expressed in terms of matrix products:


```igor
M_Pt x srcWave  = M_Lower x M_Upper
```

M_Pt, M_Lower and M_Upper are outputs created by MatrixLUD.

M_Pt is the transpose of the permutation matrix, M_Lower is a lower triangular matrix with 1's on the main diagonal and M_Upper is an upper triangular (or trapezoidal) matrix.

The MatrixLUD operation was substantially changed in Igor Pro 7.00. See the /B flag for information about backward compatibility.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | This flag is provided for backward compatibility only; it is not compatible with any other flag. /B makes MatrixLUD behave as it did in Igor Pro 6. This flag is deprecated and will be removed in a future version of Igor. |
|  | The input is restricted to a 2D real valued, single or double precision square matrix. The outputs (all double precision) are stored in the waves M_Upper, M_Lower and W_LUPermutation in the current data folder. |
|  | The W_LUPermutation output wave was needed for solving a linear system of equations using the back substitution routine, [MatrixLUBkSub](/igorpro/commands/matrixlubksub.md). For better computation methods see [MatrixLinearSolve](/igorpro/commands/matrixlinearsolve.md), [MatrixLinearSolveTD](/igorpro/commands/matrixlinearsolvetd.md) and [MatrixLLS](/igorpro/commands/matrixlls.md). |
| <span class="table-cell-nowrap">/CMF</span> | Uses Combined Matrix Format where the upper and lower matrix factors are combined into a single matrix saved in the wave M_LUFactors in the current data folder. The upper matrix factor is constructed from the main and from the upper diagonals of M_LUFactors. The lower matrix factor is constructed from the lower diagonals of M_LUFactors and setting the main diagonal to 1. |
| <span class="table-cell-nowrap">/MIND</span> | Finds the minimum magnitude diagonal element of M_Upper and store it in V_min. This is useful for investigating the behavior of the determinant of the matrix when it is close to being singular. |
| <span class="table-cell-nowrap">/PMAT</span> | Saves the transpose of the permutation matrix in a double precision wave M_Pt in the current data folder. Note that the permutation matrix is orthogonal and so the inverse of the matrix is equal to its transpose. |
| <span class="table-cell-nowrap">/SUMP</span> | Computes the sum of the phases of the elements on the main diagonal of M_Upper and store in the variable V_Sum. V_Sum is initialized to NaN and is set only if /SUMP is specified and M_Upper is complex. |

### *Details* {#details}
The input matrix *srcWave* is an MxN real or complex wave of single or double precision. Use [MatrixLUDTD](/igorpro/commands/matrixludtd.md) if your input is tri-diagonal.

The main results of the factorization are stored in the waves M_Lower, M_Upper and M_Pt. Alternatively the lower and upper factors can be combined and stored in the wave M_LUFactors (see /CMF). The waves M_Lower, M_Upper and M_LUFactors have the same data type as the input wave. M_Pt is always double precision.

When the input matrix *srcWave* is square (NxN), the resulting matrices have the same dimensions (NxN). You can reconstruct the input using the MatrixOp expression:


```igor
MatrixOp/O rA=(M_Pt^t) x (M_Lower x M_Upper)
```

If the input matrix is rectangular (NxM) the reconstruction depends on the size of N and M. If N<M:


```igor
MatrixOp/O rA=(M_Pt^t) x (subRange(M_lower,0,N-1,0,N-1) x M_Upper)
```

If N>M:


```igor
MatrixOp/O rA=(M_Pt^t) x M_lower x subRange(M_Upper,0,M-1,0,M-1)
```

The variable V_flag is set to zero if the operation succeeds and to 1 otherwise (e.g., if the input is singular). When you use the /B flag the polarity of the matrix is returned in the variable V_LUPolarity. The variables V_Sum and V_min are also set by some of the flag options above.

### *See Also* {#see-also}
[MatrixLUDTD](/igorpro/commands/matrixludtd.md), [MatrixLUBkSub](/igorpro/commands/matrixlubksub.md), [MatrixLinearSolve](/igorpro/commands/matrixlinearsolve.md), [MatrixLinearSolveTD](/igorpro/commands/matrixlinearsolvetd.md), [MatrixLLS](/igorpro/commands/matrixlls.md), [MatrixOp](/igorpro/commands/matrixop.md), [Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations)