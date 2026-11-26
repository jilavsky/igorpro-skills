---
description: "The MatrixFactor operation computes two real-valued output matrices, conceptually called matA and matB, whose matrix product minimizes the Frobenius norm of."
slug: /commands/matrixfactor
---

<div className="command-signature">

## <strong>MatrixFactor</strong>  [ <em>flags</em> ] <em>srcWave</em> {#matrixfactor}

</div>

The MatrixFactor operation computes two real-valued output matrices, conceptually called matA and matB, whose matrix product minimizes the Frobenius norm of:


```igor
| srcWave - (matA x matB) |
```

The MatrixFactor operation was added in Igor Pro 9.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/COMC = *cCols*</span> | Sets the common dimension in the factorization so that, for *srcWave* with m rows and n columns, the factorization will be (m x *cCols*) matA and (*cCols* x n) matB. If you omit /COMC, *cCols* defaults to m/2. |
| <span class="table-cell-nowrap">/CORR = *cRate*</span> | Sets the correction factor for the learning rate. The default value is 0.9. |
| <span class="table-cell-nowrap">/DSTA = *wA*</span> | Specifies the output wave representing matA. |
| <span class="table-cell-nowrap">/DSTB = *wB*</span> | Specifies the output wave representing matB. |
| <span class="table-cell-nowrap">/FREE</span> | Creates output waves as free waves. |
| <span class="table-cell-nowrap">/INIA = *iwA*</span> | Specifies an initial solution matrix for matA. The wave must have the same dimensions as matA and the same numeric type as *srcWave*. |
| <span class="table-cell-nowrap">/INIB = *iwB*</span> | Specifies an initial solution matrix for matB. The wave must have the same dimensions as matB and the same numeric type as *srcWave*. |
| <span class="table-cell-nowrap">/ITER = *nIters*</span> | Sets the maximum number of iterations. By default *nIters* is 1E7. |
| <span class="table-cell-nowrap">/LRNR = *lRate*</span> | Sets the initial learning rate of the algorithm. The default value of *lRate* is 0.01. |
| <span class="table-cell-nowrap">/MITR = *minIter*</span> | When using /OUT=3 this flag sets the minimum number of iterations that will be performed skipping the computation of the average error.  This is useful when it is assumed that a minimum number of iterations (minIter) is required and there is no point in testing for convergence before *minIter* have been completed.  By default *minIter*=1.  If *minIter* is greater than the number of specified iterations, the average error is not computed. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/OUT = *type*</span> | Sets the algorithm and restrictions on the output factors. Type values 0, 1 and 2 apply a gradient-based algorithm.  By default, *type* is 0 and there are no restrictions on the elements of the output. Set *type*=1 for non-negative output elements or *type*=2 for positive output elements.  Set *type*=3 for non-negative factorization using multiplicative updates algorithm (see Lee and Seung reference below). |
|  | Support for type=3 was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/TOL = *tolerance*</span> | Use /TOL to terminate iterations when the average Frobenius norm per input point falls below the tolerance value. By default *tolerance* is 1E-9 for single precision floating point input wave and 1E-15 for double precision input. |
| <span class="table-cell-nowrap">/Q</span> | Quiet - do not print diagnostic information to the history area and do not display progress bar. |
| <span class="table-cell-nowrap">/Z</span> | Errors are not fatal and do not abort procedure execution. Your procedure can inspect the V_flag variable to see if the operation succeeded. V_flag will be zero if it succeeded or nonzero if it failed. |

### *Details* {#details}
*srcWave* must be a single or double precision real wave.

If you specify the factorization output waves using /DSTA and /DSTB, they must have the same numeric type.

If you omit /DSTA or /DSTB, MatrixFactor produces output waves named factorAMat and factorBMat with the same numeric type as *srcWave*.

Gradient-based algorithm:

The algorithm produces a non-unique solution that may depend on the initialization of the two factors. The default initialization, used if you omit /INIA and /INIB, uses Igor's random number generator. If you want to investigate convergence you can generate your own initial values and specify them using the /INIA and /INIB flags. If you want to provide your own initial values you must provide them for both matA and matB via both /INIA and /INIB. You can run MatrixFactor once and use the outputs as initial values for a second run.

We recommend using double precision waves because the algorithm involves iterations where the Frobenius norm is computed. For large matrices or for a large number of iterations the calculation is strongly susceptible to roundoff errors which may cause it to fail to converge.

The algorithm iterates until either the tolerance is met or the number of iterations, specified by /ITER or the default value of 1E7, is exceeded. The algorithm also terminates if the the computed norm remains relatively constant:


```igor
(prevIterationNorm-curIterationNorm)/prevIterationNorm < 1e-16.
```

Multiplicative algorithm:

Here the initialization of the two factors is to random non-negative matrix elements and sequential iterations maintain non-negative values as long as *srcWave* consists of non-negative entries.  In most situations the resulting factors converge to some value that does not reduce the computed error above a certain number of iterations.  For very small tolerances where convergence before reaching *nIter* (the maximum number of iterations) is not expected, you can set /MITR=nIter-1 for optimal performance.

### *Output Variables* {#output-variables}
MatrixFactor sets these automatically created variables:


|  |  |
| --- | --- |
| V_flag | Set to 0 if the operation succeeded or to a non-zero error code. |
| V_avg | The last average Frobenius norm (Frobenius sum divided by the number of points in *srcWave*). |
| V_iterations | The number of iterations executed before the algorithm terminated. |

### *Example* {#example}

```igor
Function DemoMatrixFactor()
	Make/O/N=(10,8)/D matA0 = 1+abs(enoise(3))
	Make/O/N=(8,12)/D matB0 = 1+abs(enoise(3))
	MatrixOP/O matX0=matA0 x matB0
	MatrixFactor/COMC=8/DSTA = biMatA/DSTB=biMatB matX0
	MatrixOP/O/P=1 aa = sum(sq(matX0- biMatA x biMatB))/120	// Check norm
End
```

### *References* {#references}
Nikulin, V., Tian-Hsiang Huang, S. Ng, S. Rathnayake and G. J. McLachlan. "A Very Fast Algorithm for Matrix Factorization." *ArXiv* abs/1011.0506 (2010).


|  |
| --- |
| D. Lee and H. S. Seung. "Algorithms for non-negative matrix factorization."  Advances in Neural Information Processing Systems, 2000. |