---
description: "The MatrixCorr operation computes the correlation, covariance or degree of correlation matrix for the input 1D wave(s)."
slug: /commands/matrixcorr
---

<div className="command-signature">

## <strong>MatrixCorr</strong>  [/COV][/DEGC] <em>waveA</em> [, <em>waveB</em> ] {#matrixcorr}

</div>

The MatrixCorr operation computes the correlation, covariance or degree of correlation matrix for the input 1D wave(s).

If we denote elements of *waveA* by {*x*<sub>i</sub><sub> </sub>} and elements of *waveB* by {*y*<sub>i </sub>}, then the correlation matrix for these waves is the vector product of the form:

$$
\displaystyle \left[\begin{array}{l}
x_{1} \\
x_{2} \\
x_{3} \\
\vdots \\
x_{n}
\end{array}\right]\left[\begin{array}{lllll}
y_{1} & y_{2} & y_{3} & \ldots & y_{n}
\end{array}\right]^{*}=\left[\begin{array}{ccccc}
x_{1} y_{1}^{*} & x_{1} y_{2}^{*} & x_{1} y_{3}^{*} & \ldots & x_{1} y_{n}^{*} \\
x_{2} y_{1}^{*} & x_{2} y_{2}^{*} & x_{2} y_{3}^{*} & & x_{2} y_{n}^{*} \\
x_{3} y_{1}^{*} & x_{3} y_{2}^{*} & x_{3} y_{3}^{*} & & x_{3} y_{n}^{*} \\
\vdots & & & & \\
x_{n} y_{1}^{*} & x_{n} y_{2}^{*} & x_{n} y_{3}^{*} & \cdots & x_{n} y_{n}^{*}
\end{array}\right]
$$

where \* denotes complex conjugation. If you use the optional *waveB,* then the matrix is the cross correlation matrix. *waveB* must have the same length of *waveA*, but it does not have to be the same number type.

### *Flags* {#flags}
The flags in this operation are mutually exclusive; only one matrix can be generated at a time.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/COV</span> | Calculates the covariance matrix. |
|  | The covariance matrix for the same input is formed in a similar way after subtracting from each vector its mean value, and then dividing the resulting matrix elements by (*n* -1), where *n* is the number of elements of *waveA*. |
|  | Results are stored in the *M_Corr* or *M_Covar* waves in the current data folder or in *destWave*, if specified. |
| <span class="table-cell-nowrap">/DEGC</span> | Calculates the complex degree of correlation. The degree of correlation is defined by: |
|  | $$ \displaystyle \operatorname{degC} =\frac{M\_Covar}{\sqrt{{Var}({ waveA }) \cdot {Var}({ waveB })}}, $$ |
|  | here *M_Covar* is the covariance matrix and *Var*(*w* ) is the variance of the wave. |
|  | The complex degree of correlation should satisfy: |
|  | $$ \displaystyle 0 \leq\|\operatorname{deg} C\| \leq 1 . $$ |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave created by the operation. |
|  | It is an error to specify the same wave as both *destWave* and *waveA or waveB*. |
|  | When used in a function, this operation creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the wave *destWave* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |

### *Examples* {#examples}
The covariance matrix calculation is equivalent to:


```igor
MatrixOP/O theCov=(subtractMean(waveA,0) x (subtractMean(waveB,0)^t))/(numpoints(waveA)-1)
```

### *References* {#references}
Hayes, M.H., *Statistical Digital Signal Processing And Modeling*, 85 pp., John Wiley, 1996.

**See Also**

[MatrixOP](/igorpro/commands/matrixop.md), [variance](/igorpro/commands/variance.md)