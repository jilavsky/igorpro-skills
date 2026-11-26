---
description: "The PCA operation performs principal component analysis. Input data can be in the form of a list of 1D waves, a single 2D wave, or a string containing a list…"
slug: /commands/pca
---

<div className="command-signature">

## <strong>PCA</strong>  [/ALL/COV/CVAR/IE/IND/LEIV/NF/O /Q /RSD[=<em>rsdMode</em> ] /RMS/SCMT /SCR/SDM/SEVC/SL/SQEV/SRMT/U/VAR/WSTR=<em>waveListStr</em> /Z] [<em>wave0</em>, <em>wave1</em>, <em>wave2</em> ... <em>wave99</em> ] {#pca}

</div>

The PCA operation performs principal component analysis. Input data can be in the form of a list of 1D waves, a single 2D wave, or a string containing a list of 1D waves. The operation can produce multiple output waves depending on the specified flags.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALL</span> | Shortcut for the combination of commonly used flags: /CVAR, /SL, /NF, /IND, /IE, and /RMS. |
| <span class="table-cell-nowrap">/COV</span> | Calculates the input wave(s) covariance matrix, which is the input for the remainder of the analysis. The covariance matrix is computed by first creating a matrix copying each input 1D wave into sequential columns and then multiplying that matrix by its transpose. |
| <span class="table-cell-nowrap">/CVAR</span> | Computes the cumulative percent variance defined as 100 * the sum of the first m eigenvalues divided by the sum of all eigenvalues. The results are stored in the wave W_CumulativeVAR in the current data folder. See also /VAR below. |
| <span class="table-cell-nowrap">/DSTC = *cWave*</span> | Specifies the destination wave for the C matrix (see /SCMT). If this flag is not specified, the output is saved in the wave M_C in the current data folder. |
| <span class="table-cell-nowrap">/DSTD = *dWave*</span> | Specifies the destination for the input data matrix (see /SDM). If this flag is not specified, the corresponding output is saved in the wave M_D in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTE = *ieWave*</span> | Specifies the destination wave for the embedded error (see /IE). If this flag is not specified, the output is saved in the wave W_IE in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTG = *ieWave*</span> | Specifies the destination wave for the output eigenvalues (see /SEVC). If this flag is not specified, the output is saved in the wave W_Eigen in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTI = *indWave*</span> | Specifies the destination wave for the factor indicator function (see /IND). If this flag is not specified, the output is saved in the wave W_IND in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTM = *cvWave*</span> | Specifies the destination wave for the cumulative percent variance (see /CVAR). If you do not use this flag, the data are saved in the wave W_CumulativeVAR in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTO = *rWave*</span> | Specifies the destination wave for the row matrix R. If this wave is not specified the operation saves the output in the wave M_R in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTP = *pslWave*</span> | Specifies the destination wave for the percent significance level (see /SL). If this flag is not specified the output is saved in the wave W_PSL in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTR = *rsdWave*</span> | Specifies the destination wave for the Residual Standard Deviation (see /RSD). If this flag is not specified, the output is saved in the wave W_RSD in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTS = *rmsWave*</span> | Specifies the destination wave for the RMS error (see /RMS). If this flag is not specified, the output is saved in the wave W_RMS in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTV = *varWave*</span> | Specifies the destination wave for the variance associated with each eigenvalue (see /VAR). If this flag is not specified, the output is saved in the wave W_VAR in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all destination waves as free waves. This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/IE</span> | Computes the embedded error. Returns errors in the wave W_IE in the current data folder. The wave is scaled using: |
|  | <code class="igor">SetScale/P x 1,1,"", W_IE</code> |
|  | The embedded error is a function of the number of factors, the number of rows and columns and the sum of the eigenvectors not included in the significant factors. The behavior of IE determines the number of significant factors. |
| <span class="table-cell-nowrap">/IND</span> | Computes the factor indicator function. Note that if you specify /IND, the residual standard deviation will also be calculated. Returns results in the wave W_IND in the current data folder. The wave is scaled using: |
|  | <code class="igor">SetScale/P x 1,1,"", W_IND</code> |
| <span class="table-cell-nowrap">/LEIV</span> | Limits eigenvalues so that the SVD calculation does not require too much memory. The limit is set to the minimum of the number of rows or columns of the input. |
| <span class="table-cell-nowrap">/NF</span> | Finds the number of significant factors and stores it in the variable V_npnts. You must use /IND in order to compute the significant factors. |
| <span class="table-cell-nowrap">/O</span> | Overwrites input waves. |
| <span class="table-cell-nowrap">/Q</span> | Quiet; do not print anything in the history. |
| <span class="table-cell-nowrap">/RSD[ = *rsdMode* ]</span> |  |
|  | Computes the Residual Standard Deviation (RSD) and returns the RSD in the wave W_RSD in the current data folder. The first element in W_RSD is NaN, and all remaining wave elements correspond to the number of significant factors. Use *rsdMode* =0 for covariance about the origin. Use *rsdMode* =1 for correlation about the origin. |
| <span class="table-cell-nowrap">/RMS</span> | Computes the RMS error. Returns results in the wave W_RMS in the current data folder. The wave is scaled using SetScale/P x 1,1,"", W_RMS. |
| <span class="table-cell-nowrap">/SCMT</span> | Saves C matrix after the singular value decomposition (SVD) in the wave M_C in the current data folder. |
| <span class="table-cell-nowrap">/SCR</span> | Converts the individual wave input into standard scores. Does not work when the input is a single 2D wave. It is an error to convert to standard scores when one or more entries in the waves are NaN or INF. If you use this feature, make sure to use the appropriate form of the RSD calculation. |
| <span class="table-cell-nowrap">/SDM</span> | Saves a copy of the data matrix at the end of the calculation. This is useful if your input consists of individual waves or if you want to save the computed standard scores. If the input is a 2D matrix, you will get a copy of the input matrix in the wave M_D. |
| <span class="table-cell-nowrap">/SEVC</span> | Saves the eigenvalue vector in the wave W_Eigen, which are the raw eigenvalues generated by the SVD, in the current data folder. Normally, if the SVD was applied to a raw data matrix, i.e., not covariance or correlation matrix, you must square each element of the wave to obtain the PCA eigenvalues. Note that this wave has default wave scaling. |
| <span class="table-cell-nowrap">/SL</span> | Computes percent significance level and stores it in the wave W_PSL in the current data folder. |
| <span class="table-cell-nowrap">/SQEV</span> | Does not square SVD eigenvalues. If you specify /COV there is no need to use this flag. |
|  | Use only if your input is already a covariance matrix. In this case the results of the SVD are the eigenvalues not their square roots. |
| <span class="table-cell-nowrap">/SRMT</span> | Saves R matrix after the SVD. |
| <span class="table-cell-nowrap">/U</span> | Leaves the input waves unchanged only when the input is a 2D wave. Note that covariance calculations will not be made, even if the appropriate flag is used. |
| /VAR | Computes the variance associated with each eigenvalue. The variance is defined as the ratio of the eigenvalue to the sum of all eigenvalues. The results are stored in the wave W_VAR in the current data folder. See also /CVAR above.
| <span class="table-cell-nowrap">/WSTR = *waveListStr*</span> | Specifies a string containing a semicolon-separated list of 1D waves that contain input data. It is better to use wave *waveListStr* instead of listing each wave after the flags. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The input is either via /WSTR=*waveListStr* or a list of up to 100 1D waves or a single 2D wave following the last flag.

*waveListStr* is string containing a semicolon-separated list of 1D waves to be used for the data matrix. *waveListStr* can include any legal path to a wave. Liberal names can be quoted or not quoted. It is assumed that all waves are of the same numerical type (either single or double precision) and that all waves have the same number of points.

Regardless of the inputs, the operation expects that the number of rows in the resulting matrix is greater than or equal to the number of columns.

The operation starts by creating the data matrix from the input wave(s). If you provide a list of 1D waves they become the columns of the data matrix. You can choose to use the covariance matrix (/COV) as the data matrix and you can also choose to normalize each column of the data matrix to convert it into standard scores. This involves computing the average and standard deviation of each column and then setting the new values to be:

```igor
newValue=(oldValue-colAverage)/colStdv.
```

You can pre-process the input data using [MatrixOp](/igorpro/commands/matrixop.md) with the SubtractMean, NormalizeRows, and NormalizeCols functions.

After creating the data matrix the operation computes the singular value decomposition (SVD) of the data matrix. Results of the SVD can be saved or processed further. Save the C and R matrices using /SCMT and /SRMT. These are related to the input data matrix through:

```igor
D=R*C.
```

The remainder of the operation lets you compute various statistical quantities defined by Malinowski (see ***References***). Use the flags to determine which ones are computed.

The operation generates a number of output waves. All waves are stored in the current data folder.

You can save the input matrix D in the wave M_D, the optional SVD results are stored in the waves M_C that contains the column matrix C, M_R that contains the row matrix R, and W_Eigen that contains the eigenvalues of the data matrix. Note that these can be the eigenvalues or the square of the eigenvalues depending on the input matrix being a covariance matrix or not (see /SQEV below). Note that M_D contains the covariance if the /COV is used.

The optional 1D output waves (W_RSD, W_RMS, W_IE, W_IND, W_PSL) are saved with wave scaling to make it easier to display the wave as a function of the number of factors.

### *References* {#references}
Kaiser, H., Computer Program for Varimax Rotation in Factor Analysis, *Educational and Psychological Measurement*, *XIX*, 413-420, 1959.

Malinowski, E.R., *Factor Analysis in Chemistry*, 3rd ed., John Wiley, 2002.

### *Demos* {#demos}
[Open PCA Demo](#igor-pxp/Examples/Analysis/PCADemo.pxp)