---
description: "The ICA operation performs independent component analysis using the FastICA algorithm."
slug: /commands/ica
---

<div className="command-signature">

## <strong>ICA</strong>  [<em>flags</em>] <em>srcWave</em> {#ica}

</div>

The ICA operation performs independent component analysis using the FastICA algorithm. Input data is in the form of a 2D wave where each column represents the equivalent of a single data acquisition channel. The results of the operation are stored in the waves M_ICAComponents, M_ICAUnMix and M_matrixW in the current data folder.

The ICA operation was added in Igor Pro 7.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *alpha*</span> | *alpha* is a constant used as a factor in the argument of the logCosh function. It is not used with the exp function. |
|  | *alpha*  is in the range [1,2] and its default value is 1. |
|  | You would rarely need to change this value to affect the rate of convergence or the quality of the results. |
| <span class="table-cell-nowrap">/CF = *num*</span> | Specifies the contrast function, also called the non-quadratic function, used by ICA. |
|  |<table class="nested-table"><tbody><tr><td>*num*&nbsp;=0:</td><td>logCosh (default)</td></tr><tr><td>*num*&nbsp;=1:</td><td>exp</td></tr></tbody></table>
| <span class="table-cell-nowrap">/COLS</span> | Preconditions the input by subtracting the mean and then normalizing the input on a column-by-column basis. The algorithm appears to converge and produce better results when this flag is used. |
|  | As of Igor Pro 9.00, the input is preconditioned by default so /COLS is no longer required nor recommended. |
| <span class="table-cell-nowrap">/DCMP = *destICAComp*</span> |  |
|  | Specifies the destination wave for the ICA components. If this flag is not used the operation saves the ICA components in the wave M_ICAComponents in the current data folder. |
| <span class="table-cell-nowrap">/DEVW = *destPCAEV*</span> |  |
|  | Specifies the destination wave for the singular values of the SVD of the input matrix.  If the destination is not specified the operation saves the wave in W_PCAEV in the current data folder. The singular values are real and ordered from large to small.  Note that this flag requires that /PCA flag is also specified. |
| <span class="table-cell-nowrap">/DFLT</span> | Use the deflation/vector method where iterations solve for a single vector of the "unmixing" matrix at a time. By default the operation uses the matrix method which solves for the complete unmixing matrix at one time. |
| <span class="table-cell-nowrap">/DMXW = *destWMat*</span> |  |
|  | Specifies the destination wave for the matrix W. You can use this matrix if you want to run additional iterations (see /WINT below). |
| <span class="table-cell-nowrap">/DUNX = *destUnMix*</span> |  |
|  | Specifies the destination wave for the unmixing matrix.  If this flag is not used the operation saves the data in the wave M_ICAUnMix in the current data folder. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all destination waves as a free waves. This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions and only if *destWave*, as specified by /DEST, is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/PCA[ = *pcaDestWave*]</span> |  |
| Save the output of the "PCA" stage which is also the form of the data before the fastICA iterations. The data are saved in the wave M_PCA in the current data folder or in the user-specified *pcaDestWave*. |  |
| <span class="table-cell-nowrap">/Q</span> | Quiet mode; do not print anything in the history. |
| <span class="table-cell-nowrap">/TOL = *tolerance*</span> | The tolerance value is used to determine when iterations converge. |
|  | In the deflation/vector method the tolerance measures the difference between the values of vectors in consecutive iterations. |
|  | In the matrix method the tolerance measures the average deviation of all components. |
|  | By default *tolerance* = 1e-5 for both methods. |
| <span class="table-cell-nowrap">/WINT = *w*</span> | Provides an initial unmixing matrix W. If you do not provide this matrix the algorithm initializes using [enoise](/igorpro/commands/enoise.md). |
|  | The wave *w*  must be 2D having the same number type as *srcWave*  and having dimensions nCols x nCols, where nCols is the number of columns of *srcWave* . Providing an initial matrix is useful if you have obtained one from a previous set of iterations which may have converged using inadequate tolerance. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
*srcWave*  is a 2D wave of nRows by nCols. It must be a single or double precision real-valued wave containing no NaNs or INFs. Each column of *srcWave*  corresponds to a single data acquisition channel that is assumed to consist of a linear superposition of independent components. This can be expressed as a matrix product

**X=A (S^t)**

where **S** is an nRows by nCols matrix of independent components, **^t** denotes the transpose, **A** is an nCols by nCols mixing matrix and X is the "mixed" input. The ICA operation attempts to find the independent components of **S** from the transformation

**S=W X**

so that the mutual information between the resulting columns of **S** is minimized. Since mutual information is not affected by a multiplication of components by scalar constants, the resulting independent components can be specified up to a scalar factor.

The operation uses the FastICA algorithm to compute the independent components.

The algorithm has two available methods for computation. The default is to attempt to evaluate the full **W** matrix at once. The second method (/DFLT flag) also known as "deflation" computes one row of **W** at a time. The deflation method might have advantages in cases where there are fewer independent components than there are columns in the input.

### *Example* {#example}

```igor
// Create the source
Make/O/N=(1000,3) ddd
ddd[][0]=sin(2*pi*x/13)
ddd[][1]=sin(2*pi*x/17)
ddd[][2]=sin(2*pi*x/23)

// Create mixing matrix
Make/O/N=(3,3) AA
AA[0][0]= {0.291,0.6557,-0.5439}
AA[0][1]= {0.5572,0.3,-0.2}
AA[0][2]= {-0.1,-0.7,0.4}

// Do the mixing
MatrixOp/O xx=ddd x AA

// Try the ICA
ICA/DFLT/COLS xx
Wave ICARes
Display M_ICAComponents[][0]
Display M_ICAComponents[][1]
Display M_ICAComponents[][2]
```

### *References* {#references}
A. Hyvarinen and E. Oja (2000) Independent Component Analysis: Algorithms and Applications, Neural Networks, (13)411-430.

### *See Also* {#see-also}
[PCA](/igorpro/commands/pca.md)