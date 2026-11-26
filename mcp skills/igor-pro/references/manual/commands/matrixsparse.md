---
description: "The MatrixSparse operation provides support for basic matrix operations on sparse matrices. The MatrixSparse operation was added in Igor Pro 9.00."
slug: /commands/matrixsparse
---

<div className="command-signature">

## <strong>MatrixSparse</strong>  [<em>flags</em>] [<em>keyword</em> = <em>value</em>] {#matrixsparse}

</div>

The MatrixSparse operation provides support for basic matrix operations on sparse matrices. The MatrixSparse operation was added in Igor Pro 9.00.

The following sections use terms and concepts explained under [Sparse Matrices](/igorpro/analysis/analysis.md#sparse-matrices). You will need to understand those terms and concepts to understand the following material.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/LM</span> | Limited memory hint. Specifies that the operation can allocate limited memory proportional to vector size. If this flag is omitted, the operation allocates memory aggressively up to the size of the sparse matrix. |
| <span class="table-cell-nowrap">/Q</span> | Quiet - do not print diagnostic information to the history area. |
| <span class="table-cell-nowrap">/Z</span> | Errors are not fatal and do not abort procedure execution. Your procedure can inspect the V_flag variable to see if the operation succeeded. V_flag will be zero if it succeeded or nonzero if it failed. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">alpha = *value*</span> | Specifies the real part of the alpha value for the MM, MV, and TRSV operations. The default value is 1. |
| <span class="table-cell-nowrap">alphai = *value*</span> | Specifies the imaginary part of the alpha value for the MM, MV, and TRSV operations on complex matrices. The default value is 0. |
|  | alphai should be specified only when operating on complex matrices. |
| <span class="table-cell-nowrap">beta = *value*</span> | Specifies the real part of the beta value for the MM and MV operations. The default value is 0. |
| <span class="table-cell-nowrap">betai = *value*</span> | Specifies the imaginary part of the beta value for the MM and MV operations. The default value is 0. |
|  | betai should be specified only when operating on complex matrices. |
| <span class="table-cell-nowrap">colsA = *nCols*</span> | Specifies the number of columns of the sparse matrix A. |
|  | colsA is a required keyword for all MatrixSparse commands even in the rare cases where neither cooA, cscA, nor csrA are used. |
| <span class="table-cell-nowrap">colsG = *nCols*</span> | Specifies the number of columns of the sparse matrix G. |
|  | colsG is a required keyword for operations involving sparse matrix G. |
| <span class="table-cell-nowrap">cooA = {*valuesWave*, *rowsWave*, *colsWave*}</span> |  |
|  | Specifies sparse matrix A in COO format using three 1D waves. See [Sparse Matrix Formats](/igorpro/analysis/analysis.md#sparse-matrix-formats) for background information on cooA format. |
|  | The COO format is used only for conversion operations, not for math operations which always use CSR format. |
|  | *valuesWave* is an wave of length *nnz* (number of non-zero values) containing the non-zero values of A. The wave must be single or double precision real or complex and must not contain any NaNs or INFs. |
|  | *rowsWave* and *colsWave* are 64-bit integer 1D waves created with Make/L that contain *nnz* row and column indices respectively. |
|  | When using cooA, you must also specify the rowsA and colsA keywords. |
| <span class="table-cell-nowrap">cscA = {*valuesWave*, *rowsWave*, *ptrWave*}</span> |  |
|  | Specifies sparse matrix A in CSC format A using three 1D waves. See [Sparse Matrix Formats](/igorpro/analysis/analysis.md#sparse-matrix-formats) for background information on cscA format. |
|  | The CSC format is used only for conversion operations, not for math operations which always use CSR format. |
|  | *valuesWave* is an wave of length *nnz* (number of non-zero values) containing the non-zero values of A. The wave must be single or double precision real or complex and must not contain any NaNs or INFs. |
|  | *rowsWave* and *ptrWave* are 64-bit integer 1D waves created with Make/L. |
|  | *rowsWave* consists of nnz entries that specify the zero-based row index of each entry in *valuesWave*. |
|  | *ptrWave* contains *nCols* or *nCols*+1 entries the first of which must be zero. *ptrWave*[j] gives the index in *valuesWave* of the first non-zero value in column j. The optional longer version of *ptrWave* stores nnz in the last wave point. |
|  | When using cscA, you must also specify the rowsA and colsA keywords. |
| <span class="table-cell-nowrap">csrA = {*valuesWave*, *colsWave*, *ptrWave*}</span> |  |
|  | Specifies sparse matrix A in CSR format using three 1D waves. See [Sparse Matrix Formats](/igorpro/analysis/analysis.md#sparse-matrix-formats) for background information on csrA format. |
|  | The CSR format is used for conversion operations and for math operations. |
|  | *valuesWave* is an wave of length *nnz* (number of non-zero values) containing the non-zero values of A. The wave must be single or double precision real or complex and must not contain any NaNs or INFs. |
|  | *colsWave* and *ptrWave* are 64-bit integer 1D waves created with Make/L. |
|  | *colsWave* consists of nnz entries that specify the zero-based column index of each entry in *valuesWave*. |
|  | *ptrWave* contains *nRows* or *nRows*+1 entries the first of which must be zero. *ptrWave*[i] gives the index in *valuesWave* of the first non-zero value of row i. The optional longer version of *ptrWave* stores nnz in the last wave point. |
|  | When using csrA, you must also specify the rowsA and colsA keywords. |
| <span class="table-cell-nowrap">cooG = {*valuesWave*, *rowsWave*, *colsWave*}</span> |  |
|  | Similar to cooA but applies to sparse matrix G. |
| <span class="table-cell-nowrap">cscG = {*valuesWave*, *rowsWave*, *ptrWave*}</span> |  |
|  | Similar to cscA but applies to sparse matrix G. |
| <span class="table-cell-nowrap">csrG = {*valuesWave*, *colsWave*, *ptrWave*}</span> |  |
|  | Similar to csrA but applies to sparse matrix G. |
| <span class="table-cell-nowrap">matrixB = *wb*</span> | Designates the 2D wave *wb* as matrix B for the MM operation. |
|  | The wave *wb* must be of the same data type as sparse matrix A and must not contain INFs or NaNs. |
| <span class="table-cell-nowrap">matrixC = *wc*</span> | Designates the 2D wave *wc* as matrix C for the MM operation. |
|  | The wave *wc* must be of the same data type as sparse matrix A and must not contain INFs or NaNs. |
| <span class="table-cell-nowrap">opA = *opName*</span> | Specifies a transformation that is applied to sparse matrix A. *opName* is a single letter: |
|  |<table class="nested-table"><tbody><tr><td>T:</td><td>Transpose</td></tr><tr><td>H:</td><td>Hermitian</td></tr><tr><td>N:</td><td>No transformation (default)</td></tr></tbody></table>
|  | See [MatrixSparse Transformations](/igorpro/analysis/analysis.md#matrixsparse-transformations) for details. |
| <span class="table-cell-nowrap">opG = *opName*</span> | Specifies a transformation that is applied to sparse matrix G. *opName* is a single letter: |
|  |<table class="nested-table"><tbody><tr><td>T:</td><td>Transpose</td></tr><tr><td>H:</td><td>Hermitian</td></tr><tr><td>N:</td><td>No transformation (default)</td></tr></tbody></table>
|  | See [MatrixSparse Transformations](/igorpro/analysis/analysis.md#matrixsparse-transformations) for details. |
| <span class="table-cell-nowrap">operation = *opN*</span> | Specifies the operation name. This is a required keyword. |
|  | *opN* is one of the following: |
| ADD | Adds sparse matrices. See [MatrixSparse ADD](/igorpro/analysis/analysis.md#matrixsparse-add) for details. |
| MM | Computes the product of a sparse matrix and a dense matrix. See [MatrixSparse MM](/igorpro/analysis/analysis.md#matrixsparse-mm) for details. |
| MV | Computes the product of a sparse matrix and a vector. See [MatrixSparse MV](/igorpro/analysis/analysis.md#matrixsparse-mv) for details. |
| SMSM | Computes the product of two sparse matrices. See [MatrixSparse SMSM](/igorpro/analysis/analysis.md#matrixsparse-smsm) for details. |
| TOCOO | Creates a sparse matrix in COO format from a sparse matrix or dense matrix. See [MatrixSparse TOCOO](/igorpro/analysis/analysis.md#matrixsparse-tocoo) for details. |
| TOCSC | Creates a sparse matrix in CSC format from a sparse matrix or dense matrix. See [MatrixSparse TOCSC](/igorpro/analysis/analysis.md#matrixsparse-tocsc) for details. |
| TOCSR | Creates a sparse matrix in CSR format from a sparse matrix or dense matrix. See [MatrixSparse TOCSR](/igorpro/analysis/analysis.md#matrixsparse-tocsr) for details. |
| TODENSE | Creates a dense matrix from a sparse matrix. See [MatrixSparse TODENSE](/igorpro/analysis/analysis.md#matrixsparse-todense) for details. |
| TRSV | Solves a system of linear equations for a triangular sparse matrix. See [MatrixSparse TRSV](/igorpro/analysis/analysis.md#matrixsparse-trsv) for details. |
| <span class="table-cell-nowrap">rowsA = *nRows*</span> | Specifies the number of rows of the sparse matrix A. |
|  | rowsA is a required keyword for all MatrixSparse commands even in the rare cases where neither cooA, cscA, nor csrA are used. |
| <span class="table-cell-nowrap">rowsG = *nRows*</span> | Specifies the number of rows of the sparse matrix G. |
|  | rowsG is a required keyword for operations involving sparse matrix G. |
| <span class="table-cell-nowrap">sparseMatrixType = {*smType*,*smMode*,*smDiag*}</span> |  |
|  | Provides optional information to describe both sparse matrix A and sparse matrix G. All of the parameters are keywords. |
|  |<table class="nested-table"><tbody><tr><td>*smType*:</td><td>`GENERAL`, `SYMMETRIC`, `HERMITIAN`, `TRIANGULAR`, `DIAGONAL`, `BLOCK_TRIANGULAR`, or `BLOCK_DIAGONAL`.</td></tr><tr><td>*smMode*:</td><td>`LOWER` or `UPPER`.</td></tr><tr><td>*smDiag*:</td><td>`DIAG` or `NON_DIAG`.</td></tr></tbody></table>
|  | See [Optional Sparse Matrix Information](/igorpro/analysis/analysis.md#optional-sparse-matrix-information) for details. |
| <span class="table-cell-nowrap">vectorX = *wx*</span> | Designates the 1D wave *wx* as vector X for the MV and TRSV operations. |
|  | The wave *wx* must be of the same data type as the sparse matrix data and it must not contain INFs or NaNs. |
| <span class="table-cell-nowrap">vectorY = *wy*</span> | Designates the 1D wave *wy* as vector Y for the MV operation. |
|  | The wave *wy* must be of the same data type as the sparse matrix data and it must not contain INFs or NaNs. |

### *Details* {#details}
MatrixSparse supports data waves with single-precision and double-precision floating point real and complex data types. See [MatrixSparse Operation Data Type](/igorpro/analysis/analysis.md#matrixsparse-operation-data-type) for details.

Index waves must be signed 64-bit integer. See [MatrixSparse Index Data Type](/igorpro/analysis/analysis.md#matrixsparse-index-data-type) for details.

MatrixSparse does not support waves containing NaNs or INFs.

MatrixSparse math operations (ADD, MV, MM, SMSM, TRSV) require that input sparse matrices be in CSR format. The conversion operations (TOCOO, TOCSC, TOCSR, TODENSE) accept inputs in COO, CSC, CSR, or dense formats.

### *Output Variables* {#output-variables}
MatrixSparse sets these automatically created variables:


|  |  |
| --- | --- |
| V_flag | Set to 0 if the operation succeeded or to a non-zero error code. |

### *Examples* {#examples}
You can find examples using MatrixSparse under [MatrixSparse Operations](/igorpro/analysis/analysis.md#matrixsparse-operations).

### *See Also* {#see-also}
[Sparse Matrices](/igorpro/analysis/analysis.md#sparse-matrices) for background information about Igor's sparse matrix support.

[MatrixSparse Operations](/igorpro/analysis/analysis.md#matrixsparse-operations) for details on each supported operation and examples.

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for discussion of non-sparse Igor matrix routines.