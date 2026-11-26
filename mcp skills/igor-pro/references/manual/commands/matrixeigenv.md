---
description: "MatrixEigenV computes the eigenvalues and/or eigenvectors of a square matrix using LAPACK routines."
slug: /commands/matrixeigenv
---

<div className="command-signature">

## <strong>MatrixEigenV</strong>  [ <em>flags</em> ] <em>matrixA</em> [, <em>matrixB</em> ] {#matrixeigenv}

</div>

MatrixEigenV computes the eigenvalues and/or eigenvectors of a square matrix using LAPACK routines. The operation has a number of branches for handling nonsymmetric matrices (both standard and generalized eigenvalue problems), symmetric matrices and generalized eigenvalue problems for symmetric matrices.


### *Flags for Non-Symmetric Matrices* {#flags-for-non-symmetric-matrices}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | Creates complex valued output for real valued input waves. This is equivalent to converting the input matrix from real to complex (with zero imaginary component) prior to computing the eigenvalues and eigenvectors. The main benefit of this format is that the output has simple packing of eigenvalues and eigenvectors. See the example for General Matrices in the Details section below.  Note that this flag does not apply for symmetric or for generalized symmetric problems. |
|  | The /C was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/B = *balance*</span> | Determines how the input matrix should be scaled and or permuted to improve the conditioning of the eigenvalues. |
|  | *balance* =0 (default), 1, 2, or 3, corresponding respectively to N, P, S, or B in the LAPACK routines (see, for example, online documentation for SGEEVX). Applicable only with the /X flag. |
|  |<table class="nested-table"><tbody><tr><td>*balance*&nbsp;=0:</td><td>Do not scale or permute.</td></tr><tr><td>*balance*&nbsp;=1:</td><td>Permute.</td></tr><tr><td>*balance*&nbsp;=2:</td><td>Do diagonal scaling.</td></tr><tr><td>*balance*&nbsp;=3:</td><td>Scale and permute.</td></tr></tbody></table>
|  | Other balancing options may be available under [MatrixBalance](/igorpro/commands/matrixbalance.md). |
| <span class="table-cell-nowrap">/DSTB = *betaWave*</span> |  |
|  | Specifies the destination of the beta wave. If you do not specify this flag, the operation saves the beta array in the wave W_betaValues in the current data folder. This flag is appropriate only when solving the generalized eigenvalue problem (i.e., when both *matrixA* and *matrixB* are specified). |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTE = *eWave*</span> | Specifies the destination of the eigenvalues/alpha wave. If you do not specify this flag, the operation saves the eigenvalues in the wave W_eigenValues in the case of non-symmetric matrices. If you are solving the generalized eigenvalue problem, *ewave* contains the complex alpha values (stored by default in the wave W_alphaValues) and the eigenvalues are the ratio of the alpha to beta values (see /DSTB). |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTL = *leftWave*</span> | This flag specifies the destination of the left eigenvectors wave when left eigenvectors are calculated (/L). If you do not specify /DSTL, the operation saves the left eigenvectors in the wave M_leftEigenVectors in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTR = *rightWave*</span> |  |
|  | When right eigenvectors are calculated (/R), this flag specifies the destination of the right eigenvectors wave. If you do not specify this flag, the operation saves the right eigenvectors in the wave M_rightEigenVectors in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all specified destination waves as a free waves. It does not affect waves saved by default using fixed names. |
|  | /FREE is allowed only in functions and only if the specified destinations consist of a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more details. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/L</span> | Calculates the left eigenvectors. |
| <span class="table-cell-nowrap">/R</span> | Calculates the right eigenvectors. |
| <span class="table-cell-nowrap">/S = *sense*</span> | Determines which reciprocal condition numbers are calculated. |
|  | *sense* =0 (default), 1, 2, or 3, corresponding respectively to N, E, V, or B in the LAPACK routines. Applicable only with the /X flag. |
|  |<table class="nested-table"><tbody><tr><td>*sense*&nbsp;=0:</td><td>None</td></tr><tr><td>*sense*&nbsp;=1:</td><td>Eigenvalues only</td></tr><tr><td>*sense*&nbsp;=2:</td><td>Right eigenvectors</td></tr><tr><td>*sense*&nbsp;=3:</td><td>Eigenvalues and right eigenvectors.</td></tr></tbody></table>
|  | If sense is 1 or 3, you must compute both left and right eigenvectors. |
|  | <div><Admonition type="note"><p>/S is applicable only with the /X flag or for the generalized eigenvalue problem.</p></Admonition></div> |
| <span class="table-cell-nowrap">/X</span> | Uses LAPACK expert routines, which require additional parameters (see /B and /S flags). The operation creates additional waves: |
|  |<table class="nested-table"><tbody><tr><td>W_MatrixOpInfo</td><td>Contains in element 0 the ILO, in element 1 the IHI, and in element 2 the ABNRM from the LAPACK routines.</td></tr><tr><td>W_MatrixRCONDE</td><td>Contains the reciprocal condition numbers for the eigenvalues.</td></tr><tr><td>W_MatrixRCONDV</td><td>Contains the reciprocal condition number for the eigenvectors.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Do not report any errors except for setting V_flag. This flag applies to all branches of the operation. |

### *Flags for Symmetric Matrices* {#flags-for-symmetric-matrices}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/SYM</span> | Computes the eigenvalues of an NxN symmetric *matrixA* and stores them in the wave W_eigenValues or as specified by /DSTE. You must use /SYM if you want to use the special routines for symmetric matrices. The number of computed eigenvalues is stored in the variable V_npnts. Because W_eigenValues has N points, only the first V_npnts will contain relevant eigenvalues. |
|  | When using this flag with complex input, the matrix is assumed to be Hermitian. |
| <span class="table-cell-nowrap">/EVEC</span> | Computes eigenvectors in addition to eigenvalues. Eigenvectors will be stored in the wave M_eigenVectors (dimensions NxN) in the current data folder or as specified by /DSTR. The first V_npnts columns of the wave will contain the eigenvectors corresponding to the computed eigenvalues. Note that the flag /EVEC must be preceded by the flag /SYM. |
| <span class="table-cell-nowrap">/RNG = {*method*, *low*, *high*}</span> |  |
|  | Since eigenvalues of symmetric matrices are necessarily real, you can extract only eigenvalues in a specified range [*low*, *high*]. |
|  |<table class="nested-table"><tbody><tr><td>*method*&nbsp;=0:</td><td>Computes all the eigenvalues or eigenvectors (default).</td></tr><tr><td>*method*&nbsp;=1:</td><td>Computes eigenvalues for the interval [*low*, *high*].</td></tr><tr><td>*method*&nbsp;=2:</td><td>Computes eigenvalues for *low* and *high* integer indices (1 based). For example, to compute the first 3 eigenvalues, use: /RNG={2,1,3}.</td></tr></tbody></table>
|  | <div><Admonition type="note"><p>The flag /RNG must be preceded by the flag /SYM.</p></Admonition></div> |

### *Flags for Generalized Eigenvalue Problem* {#flags-for-generalized-eigenvalue-problem}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/GSYM = *gSymMode*</span> |  |
|  | Solves real-valued generalized eigen problem for symmetric *matrixA* and *matrixB*. *matrixB* is also assumed to be positive definite. The operation can solve the following three types of problems: |
|  | *gSymMode=1* is designed for a square matrix input *matrixA*. The operation computes the solution to the problem, |
|  | $$ \displaystyle A \mathrm{x}=\lambda B \mathrm{x}, $$ |
|  | where **x** is an eigenvector and λ is an eigenvalue. |
|  | *gSymMode=2* |
|  | $$ \displaystyle A B \mathrm{x}=\lambda \mathrm{x}, $$ |
|  | where the superscript T denotes a transpose. |
|  | *gSymMode=3* is designed to solve the generalized eigenvalue problem, |
|  | $$ \displaystyle B A \mathrm{x}=\lambda \mathrm{x}, $$ |
|  | where **A** and **B** are square matrices (*matrixA* and *matrixB)*, **x** is an eigenvector and λ is an eigenvalue. |
|  | All modes support input of single or double precision real waves. *matrixA* and *matrixB* must have the same number type. |

### *Details for General (nonsymmetric) Matrices* {#details-for-general-nonsymmetric-matrices}
In this case, the eigenvalues are returned in the 1D complex wave W_eigenvalues (see also /DSTE). The eigenvectors are returned in the 2D waves M_R_eigenVectors or M_L_eigenVectors (see /DSTL and /DSTR).

The calculated eigenvectors are normalized to unit length.

Complex conjugate pairs of eigenvalues appear consecutively with the eigenvalue having the positive imaginary part listed first.

If the j*th* eigenvalue is real, then the corresponding eigenvector u(j)=M[][j] is the j*th* column of M_L_eigenVectors or M_R_eigenVectors. If the j*th* and (j+1)*th* eigenvalues form a complex conjugate pair, then u(j) = M[][j] + i\*M[][j+1] and u(j+1) = M[][j] - i\*M[][j+1].

### *Examples* {#examples}
The following two examples illustrate the eigenvalues and eigenvectors computed using both real and forced complex (via /C flag).  In each case the first eigenvalue and eigenvector are tested.


```igor
Function TestMatrixEigenVReal()
	Make/D/N=(2,2)/O eee={{0,1},{-1,0}}
	MatrixEigenV/R eee
	Wave W_eigenvalues, M_R_eigenVectors
	MatrixOP/O firstEV=cmplx(col(M_R_eigenVectors,0),col(M_R_eigenVectors,1))
	MatrixOP/O aa=eee x firstEV - W_eigenvalues[0]*firstEV
	Print aa
End

Function TestMatrixEigenVComplex()
	Make/D/N=(2,2)/O eee={{0,1},{-1,0}}
	MatrixEigenV/R/C eee
	Wave W_eigenvalues, M_R_eigenVectors
	MatrixOP/O aa=eee x col(M_R_eigenVectors,0) - W_eigenValues[0]*col(M_R_eigenVectors,0)
	Print aa
End
```

### *Details for Symmetric Matrices* {#details-for-symmetric-matrices}
The LAPACK routines that compute the eigenvalues and eigenvectors of symmetric matrices claim to use the Relatively Robust Representation whenever possible. If your matrix is symmetric, you should use this branch of the operation (/SYM) for improved accuracy.

### *Details for Generalized Eigenvalue Problem (non symmetric matrices)* {#details-for-generalized-eigenvalue-problem-non-symmetric-matrices}
Here the right eigenvectors (/R) are solutions of the equation

$$
\displaystyle \mathbf{A x}=\lambda \mathbf{B x},
$$

and the left eigenvectors (/L) are solutions of the equation

$$
\displaystyle \mathbf{x}^{\mathbf{H}} \mathbf{A}=\lambda \mathbf{x}^{\mathbf{H}} \mathbf{B},
$$

where the superscript H denotes the conjugate transpose.

When both *matrixA* and *matrixB* are real valued, the operation creates the following waves in the current data folder:


|  |  |
| --- | --- |
| W_alphaValues | Contains the complex alpha values (see /DSTE). |
| W_betaValues | Contains the real-valued denominator (see /DSTB) such that the eigenvalues are given by |
|  | $$ \displaystyle \lambda_{j}=\frac{\alpha_{j}}{\beta_{j}} . $$<sub></sub> |
| M_leftEigenVectors | Real valued waves where columns correspond to eigenvectors of the equation. You can use /DSTL to specify an alternate destination. |
| M_rightEigenVectors | Real valued waves where columns correspond to eigenvectors of the equation. You can use /DSTR to specify an alternate destination. |

Every point in the wave W_alphaValues corresponds to an eigenvalue. When the imaginary part of W_alphaValues[j] is zero, the eigenvalue is real and the corresponding eigenvector is also real, e.g., M_rightEigenVectors[][j]. When the imaginary part of the eigenvalue is positive, then there are two eigenvalues that are complex-conjugates of each other with corresponding complex eigenvectors given by


```igor
cmplx(M_rightEigenVectors[][j],M_rightEigenVectors[][j+1])
```

and


```igor
cmplx(M_rightEigenVectors[][j],-M_rightEigenVectors[][j+1])
```

When both *matrixA* and *matrixB* are complex the operation creates the complex waves:


```igor
W_alphaValues, W_betaValues, M_leftEigenVectors, M_rightEigenVectors
```

with the ratio W_alphaValues[j]/W_betaValues[j] expressing the generalized eigenvalue. The corresponding M_leftEigenVectors[][j] and M_rightEigenVectors[][j] are the respective left and right eigenvectors. The simplicity of the complex case suggests that when *matrixA* and *matrixB* are real, it is sometimes easier to convert them to complex waves prior to executing matrixEigenV (see /C above).

Depending on the choice of /S, the operation also calculates the reciprocal condition number for the eigenvalues (stored in W_reciprocalConditionE) and the reciprocal condition number of the eigenvectors (stored in W_reciprocalConditionV). Note that a zero entry in W_reciprocalConditionV implies that the eigenvalues could not be ordered.

### *Example* {#example}

```igor
Function testGeneralizedNonSymmetric()
	Make/D/N=(2,2)/O matA={{0,1},{-1,3}},matB={{1,2},{-1,5}}
	MatrixEigenV/R/C/DSTR=REvec/DSTE=alphaWave/DSTB=betaWave matA,matB
	MatrixOP/O/FREE ev=alphaWave/betaWave
	Variable eval1=ev[0] 	// first eigenvalue
	MatrixOP/O/FREE r1=col(REvec,0)	// first eigenvector
	MatrixOP/O/p=1/FREE aa=(matA x r1) - eval1*(matB x r1)	// expect -> 0
	MatrixOP/O/FREE r2=col(REvec,1)	// second eigenvector
	Variable eval2=ev[1] 	// second eigenvalue
	MatrixOP/O/p=1/FREE aa=(matA x r2) - eval2*(matB x r2)	// expect -> 0
End
```



### *See Also* {#see-also}
[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.

The following LAPACK routines are used by the operations: cggevx, sggevx, zggevx, dggevx, sgeevx, sgeev, dgeevx, dgeev, cgeevx, Sq.

Symmetric matrices can also be decomposed using the [MatrixSchur](/igorpro/commands/matrixschur.md) operation and using [MatrixOp](/igorpro/commands/matrixop.md) chol(). Matrix balancing is also available under [MatrixBalance](/igorpro/commands/matrixbalance.md).