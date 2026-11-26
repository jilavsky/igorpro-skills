---
description: "The MatrixSchur operation computes for an NxN nonsymmetric srcMatrix, the eigenvalues, the real Schur form A and the matrix of Schur vectors V."
slug: /commands/matrixschur
---

<div className="command-signature">

## <strong>MatrixSchur</strong>  [/Z] <em>srcMatrix</em> {#matrixschur}

</div>

The MatrixSchur operation computes for an NxN nonsymmetric *srcMatrix*, the eigenvalues, the real Schur form A and the matrix of Schur vectors V.

The Schur factorization has the form: srcMatrix = M_V x M_A x (M_V^T), where M_V^T is the transpose (use M_V^H if srcMatrix is complex) and x denotes matrix multiplication.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSTA = *aWave*</span> | Specify the output Schur matrix M_A. If you do not use this flag, the operation saves the matrix in the wave M_A in the current data folder. |
|  | This flag was added in Igor Pro 10. |
| <span class="table-cell-nowrap">/DSTE = *eWave*</span> | Specify the complex eigenvalues wave. The eigenvalues are not ordered.  When this flag is used, /DSTI and /DSTR are disabled. |
|  | This flag was added in Igor Pro 10. |
| <span class="table-cell-nowrap">/DSTI = *iWave*</span> | Specify the output wave for the imaginary part of the eigenvalues. If you do not specify this flag (or /DSTE), the operation saves the data in the wave W_IEigenValues in the current data folder. |
|  | This flag was added in Igor Pro 10. |
| <span class="table-cell-nowrap">/DSTR = *rWave*</span> | Specify the output wave for the real part of the eigenvalues.  If you do not specify this flag (or /DSTE) the operation saves the data in the wave W_REigenValues in the current data folder. |
|  | This flag was added in Igor Pro 10. |
| <span class="table-cell-nowrap">/DSTV = *vWave*</span> | Specify the output orthogonal matrix of Schur vectors M_V. If you do not specify this flag, the operation saves the data in the wave M_V in the current data folder. |
|  | This flag was added in Igor Pro 10. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all destination waves as free waves. This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The operation creates:

|  |  |
| --- | --- |
| M_A | Upper triangular matrix containing the Schur form A. |
| M_V | Unitary matrix containing the orthogonal matrix V of the Schur vectors. |
| W_REigenValues |  |
| W_IEigenValues | Waves containing the real and imaginary parts of the eigenvalues when *srcMatrix* is a real wave. If *srcMatrix* is complex, the eigenvalues are stored in W_EigenValues. |
|  | The eigenvalues in both cases are complex. Due to LAPACK, the result is packed in two waves (real and imaginary) when the input wave is real. When srcWave is complex, the eigenvalues are packed in a single wave. |

The variable V_flag is set to 0 when there is no error; otherwise it contains the LAPACK error code.

### *Examples* {#examples}
You can test this operation for an N-by-N source matrix:


```igor
Make/D/C/N=(5,5) M_S=cmplx(enoise(1),enoise(1))
MatrixSchur M_S
MatrixOp/O unitary=(M_V^h) x M_V		// check unitary
MatrixOp/O diff=abs(M_S-M_V x M_A x (M_V^H))	// check decomposition
```

### *See Also* {#see-also}
[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines and for background references with details about the LAPACK libraries.