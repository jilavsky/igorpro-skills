---
description: "The MatrixLLS operation solves overdetermined or underdetermined linear systems involving MxN matrixA, using either QR/LQ or SV decompositions."
slug: /commands/matrixlls
---

<div className="command-signature">

## <strong>MatrixLLS</strong>  [/M=<em>method</em>  /O/Z] <em>matrixA</em>  <em>matrixB</em> {#matrixlls}

</div>

The MatrixLLS operation solves overdetermined or underdetermined linear systems involving MxN *matrixA,* using either QR/LQ or SV decompositions. Both *matrixA* and *matrixB* must have the same number type. Supported types are real or complex single precision and double precision numbers.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSTA = *destA*</span> | Specifies the output destination wave for the matrix decomposition. If you do not use this flag, the operation saves the corresponding data in the wave M_A in the current data folder. When used in a function, operation creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTB = *destB*</span> | Specifies the output destination wave for the solution matrix. If you do not use this flag, the operation saves the corresponding data in the wave M_B in the current data folder. When used in a function, operation creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTS = *destS*</span> | When using method=1, this flag specifies the 1D singular values wave. If you do not use this flag, the operation saves the corresponding data in the wave M_SV in the current data folder. When used in a function, operation creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all the specified destination waves as free waves. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/M = *method*</span> | Specifies the decomposition method. |
|  |<table class="nested-table"><tbody><tr><td>*method*&nbsp;=0:</td><td>Decomposition is to QR or LQ (default). Creates the 2D wave M_A, which contains details of the QR/LQ factorization.</td></tr><tr><td>*method*&nbsp;=1:</td><td>Singular value decomposition (SVD). Creates the 2D wave MA, which contains the right singular vectors stored row-wise in the first min(*m*,*n*) rows. Creates the 1D wave M_SV, which contains the singular values of *matrixA* arranged in decreasing order.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/O</span> | Overwrites *matrixA* with its decomposition and *matrixB* with the solution vectors. This uses less memory. Note that this flag is not compatible with the various destination flags. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
When the /O flag is not specified, the solution vectors are stored in the wave M_B, otherwise the solution vectors are stored in *matrixB*. Let *matrixA* be m rows by n columns and *matrixB* be an m by NRHS (if NRHS=1 it can be omitted). When m>=n, MatrixLLS solves the least squares solution to an overdetermined system:

$$
\displaystyle { Minimize } \| { matrix } B-{ matrix } A \times \mathbf{X} \| {. }
$$

Here the first n rows of M_B contain the least squares solution vectors while the remaining rows can be squared and summed to obtain the residual sum of the squares.  If you are not interested in the residual you can resize the wave using, for example:


```igor
Redimension/N=(n,NRHS) M_B
```

If m<n, MatrixLLS finds the minimum norm solution of the underdetermined system:

$$
\displaystyle { matrix } A \times \mathbf{X}= { matrix } B .
$$

In this case, the first m rows of M_B contain the minimum norm solution vectors while the remaining rows can be squared and summed to obtain the residual sum of the squares for the solution. If you are not interested in the residual you can resize the wave using, for example:


```igor
Redimension/N=(m,NRHS) M_B
```

:::note
Here *matrixB* consists of one or more column vectors B corresponding to one or more solution vectors X which are computed simultaneously. If *matrixB* consists of a single column, M_B is a 2D matrix wave that contains a single solution column.
:::

The variable V_flag is set to 0 when there is no error; otherwise it contains the LAPACK error code.

### *Examples* {#examples}

```igor
// Construct matrixA as a 4x4 matrix
Make/O/D/N=(4,4) matrixA
matrixA[0][0]= {-54,-27,-9,-38}
matrixA[0][1]= {13,60,-42,-26}
matrixA[0][2]= {-80,17,44,-35}
matrixA[0][3]= {98,-8,-72,7}

// Construct matrixB as a single column (1D wave)
Make/O/D/N=4 matrixB={-20,77,-79,-33}

// Solve for matrixA x vectorX = matrixB
MatrixLLS matrixA, matrixB	// Output stored in M_B

// Verify the solution
MatrixOP/O/P=1 aa=sum(abs(matrixA x col(M_B,0) - matrixB)) aa={9.947598300641403e-14}

// Compute multiple solutions at once
// Construct matrixB as two columns (2D wave)
Redimension/N=(4,2) matrixB
matrixB[0][0]= {-20,77,-79,-33}
matrixB[0][1]= {-94,61,29,68}

// Perform the calculation
MatrixLLS matrixA, matrixB

// Verify the solutions
MatrixOP/O/P=1 aa=sum(abs(matrixA x col(M_B,0) - col(matrixB,0))) aa={9.947598300641403e-14}
MatrixOP/O/P=1 aa=sum(abs(matrixA x col(M_B,1) - col(matrixB,1))) aa={1.989519660128281e-13}

// See if we have an overdetermined system ...
Make/D/N=(5,4) matrixA
matrixA[0][0] = {-7,-62,-47,-54,-80}
matrixA[0][1] = {43,15,-9,-94,57}
matrixA[0][2] = {22,61,-95,-95,51}
matrixA[0][3] = {-54,68,81,-51,54}
Make/O/D/N=(5) matrixB
matrixB[0] = {-28,-75,-74,35,86}

// Perform the calculation
MatrixLLS matrixA, matrixB

// Remove the extra rows from M_B
Redimension/N=4 M_B

// M_B is only the least squares solution so there is no point in attempting
// to verify the solution as in the example above.
```

### *See Also* {#see-also}
[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines and for background references with details about the LAPACK libraries.