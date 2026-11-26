---
description: "The MatrixLinearSolveTD operation solves the linear system TDMatrix \\ X = matrixB."
slug: /commands/matrixlinearsolvetd
---

<div className="command-signature">

## <strong>MatrixLinearSolveTD</strong>  [/Z]  <em>upperW</em>, <em>mainW</em>, <em>lowerW</em>, <em>matrixB</em> {#matrixlinearsolvetd}

</div>

The MatrixLinearSolveTD operation solves the linear system *TDMatrix* \* X = *matrixB*. In the matrix product on the left hand side, *TDMatrix* is a tridiagonal matrix with upper diagonal *upperW*, main diagonal *mainW*, and lower diagonal *lowerW*. It solves for vector(s) X depending on the number of columns (NRHS) in matrixB.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSTA = *aWave*</span> | Use this flag to specify the destination wave for the decomposition of *matrixA*. *aWave* is the matrix product P x L x U, where P is the permutation matrix and L and U are the lower and upper triangular decompositions respectively of *matrixA*. If you do not use this flag, the data is saved in the wave M_A in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTB = *bWave*</span> | Use this flag to specify the destination wave for the solution matrix. If you do not specify this flag, the operation saves the solution in the wave M_B. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTC = *solutionWave*</span> |  |
|  | Specifies the output wave when all input waves are complex. If you omit /DSTC then the output wave is M_TDLinearSolution in the current data folder. /DSTC was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/DSTI = *iWave*</span> | Use this flag to specify the destination of the IPIV wave. If you do not specify this flag, the operation saves the data in the wave W_IPIV in the current data folder. The IPIV array represents the permutation matrix where row i of *matrixA* was interchanged with row IPIV(i). |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTR = *solutionWave*</span> |  |
|  | Specifies the output wave when all input waves are real. If you omit /DSTR then the output wave is M_TDLinearSolution in the current data folder. /DSTR was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified destination waves as free waves. This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/O</span> | Overwrites *matrixA* with the decomposition (otherwise saved in M_A) and *matrixB* with the solution matrix. Note that this flag is not compatible with the destination flags above. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The input waves can be single or double precision (real or complex). Results are returned in the wave M_TDLinearSolution in the current data folder. The wave *mainW* determines the size of the main diagonal (N). All other waves must match it in size with *upperW* and *mainW* containing one less point and *matrixB* consisting of N-by-NRHS elements of the same data type.

MatrixLinearSolveTD should be more efficient than [MatrixLinearSolve](/igorpro/commands/matrixlinearsolve.md) with respect to storage requirements.

MatrixLinearSolveTD creates the variable V_flag, which is zero when it finishes successfully.

### *See Also* {#see-also}

This operation is based on LAPACK routines: sgesv, dgesv, cgesv, zgesv.

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations), [MatrixLinearSolve](/igorpro/commands/matrixlinearsolve.md), [MatrixOp](/igorpro/commands/matrixop.md)