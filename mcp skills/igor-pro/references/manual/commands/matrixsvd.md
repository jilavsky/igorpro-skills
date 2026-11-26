---
description: "The MatrixSVD operation uses the singular value decomposition algorithm to decompose an MxN matrixWave into a product of three matrices."
slug: /commands/matrixsvd
---

<div className="command-signature">

## <strong>MatrixSVD</strong>  [/B][/O/U=<em>UMatrixOptions</em> /V=<em>VMatrixOptions</em> /Z] <em>matrixWave</em> {#matrixsvd}

</div>

The MatrixSVD operation uses the singular value decomposition algorithm to decompose an MxN matrixWave into a product of three matrices. The default decomposition is into MxM wave M_U, min(M,N) wave W_W and NxN wave M_VT.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Use this flag for backwards compatibility with Igor Pro 3. This option applies only to real valued input waves. Note that no other flag can be combined with /B. Here the decomposition is such that: |
|  | U*W*V^T = *matrixWave* |
|  | U: ::MxN column-orthonormal matrix.
|  | W: ::NxN diagonal matrix of positive singular values.
|  | V: ::NxN orthonormal matrix.
| <span class="table-cell-nowrap">/DACA</span> | Replaces the standard LAPACK algorithm with one that is based on a divide and conquer approach. For a typical 1000x1000 matrix this provides a 6x speed improvement. |
|  | Added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/DSTI = *iWave*</span> | When using /INVW, you can use this flag to specify the output wave for the inverse of the singular values. If you do not specify this flag, the operation saves the data in the wave W_InvW in the current data folder. Note that this flag has no effect if /PART is used. |
|  | This flag was added in Igor Pro 10. |
| <span class="table-cell-nowrap">/DSTU = *uWave*</span> | Specify the output wave for the orthogonal/unitary matrix U. If you do not specify this flag the operation saves the data in the wave M_U in the current data folder. |
|  | This flag was added in Igor Pro 10. |
| <span class="table-cell-nowrap">/DSTV = *vWave*</span> | Specify the output wave for the orthogonal/unitary matrix V.  If you do not specify this flag, the operation saves the data in the wave M_V in the current data folder. |
|  | This flag was added in Igor Pro 10. |
| <span class="table-cell-nowrap">/DSTW = *wWave*</span> | Specify the output wave for the singular values. If you do not specify this flag, the operation saves the data in the wave W_W in the current data folder. |
|  | This flag was added in Igor Pro 10. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all destination waves as free waves.  This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/INVW</span> | Saves the inverse of the elements in W_W. The results are then stored in wave W_InvW.  Note that this flag has no effect if /PART is used. |
| <span class="table-cell-nowrap">/O</span> | Overwrites *matrixWave* with the first columns of U. Use this flag to if you need to conserve memory. See also related settings of /U and /V. |
| <span class="table-cell-nowrap">/PART = *nVals*</span> | Performs a partial SVD computing only *nVals* singular values (stored in W_W) and the associated vectors in the matrix M_U and M_V. If you use this flag the operation ignores all other flags except /PDEL. The partial SVD is computed using the Power method of Nash and Shlien. |
|  | The /PART flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/PDEL = *del*</span> | Sets the convergence threshold which defaults to 1e-6. Larger positive values result in faster execution but may lead to less accurate results. |
|  | The /PDEL flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/U = *UMatrixOptions*</span> |  |
|  | *UMatrixOptions* can have the following values: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>All cols of U are returned in the wave M_U (default).</td></tr><tr><td>1:</td><td>The first min(m,n) columns of U are returned in the wave M_U.</td></tr><tr><td>2:</td><td>The first min(m,n) columns of U overwrite *matrixWave* (/O must be specified).</td></tr><tr><td>3:</td><td>No columns of U are computed.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/V = *VMatrixOptions*</span> |  |
|  | *VMatrixOptions* can have the following values: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>All rows of V^T are returned in the wave M_VT (default).</td></tr><tr><td>1:</td><td>The first min(M,N) rows of V^T are returned in the wave M_VT.</td></tr><tr><td>2:</td><td>The first min(m,n) rows of V^T are overwritten on *matrixWave* (/O must be specified).</td></tr><tr><td>3:</td><td>No rows of V^T are computed.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The singular value decomposition is computed using LAPACK routines. The diagonal elements of matrix W are returned as a 1D wave named W_W. If /B is used W_W will have N elements. Otherwise the number of elements in W_W is min(M,N).

The matrix V is returned in a matrix wave named M_V if /B is used otherwise the transpose V^T is returned in the wave M_VT.

All output objects are created in the current data folder.

The variable V_flag is set to zero if the operation succeeds. It is set to 1 if the algorithm fails to converge.

The variable V_SVConditionNumber is set to the condition number of the input matrix. The condition number is the ratio of the largest singular value to the smallest.

### *Example* {#example}

```igor
Make/O/D/N=(10,20) A=gnoise(10)
MatrixSVD A
MatrixOp/O diff=abs(A-(M_U x DiagRC(W_W,10,20) x M_VT))
Print sum(diff,-inf,inf)
```

### *References* {#references}
J.C. Nash and S.Shlien "Simple Algorithms for the Partial Singular Value Decomposition", The Comp. J. (30) No. 3 1987.

### *See Also* {#see-also}
[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines and for background references with details about the LAPACK libraries.