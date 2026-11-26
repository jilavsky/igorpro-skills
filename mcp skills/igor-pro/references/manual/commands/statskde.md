---
description: "StatsKDE can be used to estimate a PDF from original data distribution."
slug: /commands/statskde
---

<div className="command-signature">

## <strong>StatsKDE</strong>  [<em>flags</em>] <em>srcWave</em> {#statskde}

</div>

StatsKDE can be used to estimate a PDF from original data distribution. Unlike histograms, this method produces a smooth result as it constructs the PDF from a normalized superposition of kernel functions.

The StatsKDE operation was added in Igor Pro 7.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/BWM = *m*</span> | Sets the bandwidth selection method. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>User-specified via /H flag</td></tr><tr><td>*m*&nbsp;=1:</td><td>Silverman</td></tr><tr><td>*m*&nbsp;=2:</td><td>Scott</td></tr><tr><td>*m*&nbsp;=3:</td><td>Bowmann and Azzalini</td></tr></tbody></table>
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output destination. Creates a real wave reference for the destination wave in a user function. See [Automatic Creation of WAVE References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/FREE</span> | Makes the destination wave (specified by /DEST) a free wave. |
| <span class="table-cell-nowrap">/H = *bw*</span> | Specifies a fixed user-defined bandwidth. |
| <span class="table-cell-nowrap">/KT = *kernel*</span> | Specifies the kernel type. |
|  |<table class="nested-table"><tbody><tr><td>*kernel*&nbsp;=1:</td><td>Epanechnikov</td></tr><tr><td>*kernel*&nbsp;=2:</td><td>Bi-weight</td></tr><tr><td>*kernel*&nbsp;=3:</td><td>Tri-weight</td></tr><tr><td>*kernel*&nbsp;=4:</td><td>Triangular</td></tr><tr><td>*kernel*&nbsp;=5:</td><td>Gaussian</td></tr><tr><td>*kernel*&nbsp;=6:</td><td>Rectangular</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Q</span> | No results printed in the history area. In the case of univariate KDE this flags suppresses the printing of the bandwidth value. |
| <span class="table-cell-nowrap">/S = {*x0,dx,xn*}</span> | Specifies the range of the output starting from x=*x0* to x=*xn* in increments of *dx* . |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag is set to zero if there are no errors. |

### *Details* {#details}
StatsKDE estimates the PDF of a distribution of values using a smoothing kernel and a bandwidth parameter which affects the degree of smoothing.

Theory suggests that the Epanechnikov kernel is the most efficient but many expressions for the optimal bandwidth are derived for the Gaussian kernel. If *srcWave* contains N points and the requested output (/S flag) has M points then the computational complexity is O(NM). For large problems it may be beneficial to use the Gaussian kernel via the [FastGaussTransform](/igorpro/commands/fastgausstransform.md) operation.

### *References* {#references}
Wand M.P. and Jones M.C. (1995) Monographs on Statistics and Applied Probability, London: Chapman and Hall

Bowman, A.W., and Azzalini, A. (1997), Applied Smoothing Techniques for Data Analysis, London: Oxford University Press.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [Histogram](/igorpro/commands/histogram.md), [FastGaussTransform](/igorpro/commands/fastgausstransform.md)