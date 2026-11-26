---
description: "The MatrixLinearSolve operation solves the linear system matrixA X=matrixB where matrixA is an N-by-N matrix and matrixB* is an N-by-NRHS matrix of the same…"
slug: /commands/matrixlinearsolve
---

<div className="command-signature">

## <strong>MatrixLinearSolve</strong>  [/D={<em>subDiagonals</em>,<em>superDiagonals</em> }/M=<em>method</em> /O/Z] [/L][/U] <em>matrixA</em>  <em>matrixB</em> {#matrixlinearsolve}

</div>

The MatrixLinearSolve operation solves the linear system *matrixA* *X=*matrixB* where *matrixA* is an N-by-N matrix and *matrixB* is an N-by-NRHS matrix of the same data type.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/M = *method*</span> | Determine the solution method which best suites input *matrixA*. |
|  |<table class="nested-table"><tbody><tr><td>*method*&nbsp;=1:</td><td>Uses simple LU decomposition (default). See also LAPACK documentation for SGESV, CGESV, DGESV, and ZGESV.</td></tr><tr><td></td><td>Creates the wave W_IPIV that contains the pivot indices that define the permutation matrix P. Row (i) if the matrix was interchanged with row ipiv(i).</td></tr><tr><td>*method*&nbsp;=2:</td><td>If *matrixA* is band diagonal, you also have to specify /D. See also LAPACK documentation for SGBSV, CGBSV, DGBSV, and ZGBSV.</td></tr><tr><td></td><td>Creates the wave W_IPIV that contains the pivot indices that define the permutation matrix P. Row (i) if the matrix was interchanged with row ipiv(*i*).  Also note that if you are using the /O flag, the overwritten waves may have a different dimensions.</td></tr><tr><td>*method*&nbsp;=4:</td><td>For tridiagonal matrix; still expecting full matrix in *matrixA,* but it will ignore the data in the elements outside the 3 diagonals. See also LAPACK documentation for SGTSV, CGTSV, DGTSV, and ZGTSV.</td></tr><tr><td>*method*&nbsp;=8:</td><td>Symmetric/hermitian. See also LAPACK documentation for SPOSV, CPOSV, DPOSV, and ZPOSV.</td></tr><tr><td>*method*&nbsp;=16:</td><td>Complex symmetric (complex only). See also LAPACK documentation for CSYSV and ZSYSV.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/D = {*sub*,*super*}</span> | Specifies a band diagonal matrix. The subdiagonal (*sub*) and superdiagonal (*super*) size must be positive integers. |
| <span class="table-cell-nowrap">/L</span> | Uses the lower triangle of *matrixA*. /L and /U are mutually exclusive flags. |
| <span class="table-cell-nowrap">/U</span> | Uses the upper triangle of *matrixA*. /U is the default. |
| <span class="table-cell-nowrap">/O</span> | Overwrites *matrixA* and *matrixB* with the results of the operation. This will save on the amount of memory needed. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
If /O is not specified, the operation also creates the n-by-n wave M_A and the n-by-nrhs solution wave M_B.

The variable V_flag is created by the operation. If the operation completes successfully, V_flag is set to zero, otherwise it is set to the LAPACK error code.

### *See Also* {#see-also}
[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines and for background references with details about the LAPACK libraries.