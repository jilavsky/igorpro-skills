---
description: "The MatrixGLM operation solves the general Gauss-Markov Linear Model problem (GLM) which minimizes the 2-norm of a vector y."
slug: /commands/matrixglm
---

<div className="command-signature">

## <strong>MatrixGLM</strong>   [/Z] <em>matrixA</em>, <em>matrixB</em>, <em>waveD</em> {#matrixglm}

</div>

The MatrixGLM operation solves the general Gauss-Markov Linear Model problem (GLM) which minimizes the 2-norm of a vector y

$$
\displaystyle \min \|y\|_{2} \quad \text { subject to } \quad d=A x+B y .
$$

A is *matrixA* (an NxM wave), B is *matrixB* (an NxP wave), and d is provided by *waveD* which is a 1D wave of N rows. The vectors x and y are the results of the calculation; they are stored in output waves Mat_X and Mat_Y in the current data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSTX = *xWave*</span> | Specify the destination of the x-wave. If you don't use this flag, the operation saves the x-wave in Mat_x in the current data folder. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTY = *yWave*</span> | Specify the destination of the y-wave. If you don't use this flag, the operation saves the y-wave in Mat_y in the current data folder. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all specified destination waves as free waves. This flag does not affect output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions and only if the destination wave, as specified by /DSTX and /DSTY, is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Z</span> | In the event of an error, MatrixGLM will not return the error to Igor, which would cause procedure execute to abort. Your code should use the V_flag output variable to detect and handle errors. |

### *Details* {#details}
All input waves must have the same numeric type. Supported types are single-precision and double-precision floating point, both real and complex. The output waves Mat_X and Mat_Y have the same numeric type as the input.

The LAPACK algorithm assumes that M <= N <= M+P and

$$
\displaystyle \begin{array}{l}
\operatorname{rank}(A)=M, \\
\\
\operatorname{rank}(A B)=N .
\end{array}
$$

Under these assumptions there is a unique solution x and a minimal 2-norm solution y, which are obtained using a generalized QR factorization of A and B. If the operation completes successfully the variable V_Flag is set to zero. Otherwise it contains a LAPACK error code.

### *Output Variables* {#output-variables}

|  |  |
| --- | --- |
| V_flag | Set to 0 if MatrixGLM succeeds or to a LAPACK error code. |

### *See Also* {#see-also}
[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines and for background references with details about the LAPACK libraries.