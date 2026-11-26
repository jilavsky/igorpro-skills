---
description: "The FastGaussTransform operation implements an efficient algorithm for evaluating the discrete Gauss transform as given by."
slug: /commands/fastgausstransform
---

<div className="command-signature">

## <strong>FastGaussTransform</strong>  [/AERR=<em>aprxErr</em>, /WDTH=<em>h</em>, /OUTW=<em>locWave</em>, /OUT1={<em>x1</em>,<em>nx</em>,<em>x2</em> },  /OUT2={<em>x1</em>,<em>nx</em>,<em>x2</em>,<em>y1</em>,<em>ny</em>,<em>y2</em> }, /OUT3={<em>x1</em>,<em>nx</em>,<em>x2</em>,<em>y1</em>,<em>ny</em>,<em>y2</em>,<em>z1</em>,<em>nz</em>,<em>z2</em> }, /Q, /RX=<em>rx</em>, /RY=<em>ry</em>, /TET=<em>nTerms</em>, /Z] <em>srcLocationsWave</em>, <em>srcWeightsWave</em> {#fastgausstransform}

</div>

The FastGaussTransform operation implements an efficient algorithm for evaluating the discrete Gauss transform as given by

$$
\displaystyle G\left(y_{j}\right)=\sum_{i=0}^{N-1} q_{i} \exp \left(-\frac{\left\|y_{j}-x_{i}\right\|^{2}}{h}\right),
$$

where **G** is an M-dimensional vector, **y** is an N-dimensional vector representing the observation position, {**q<sub>i</sub>**} are the M-dimensional weights, {**x<sub>i</sub>**} are N-dimensional vectors representing source locations and *h* is the Gaussian width. The wave M_FGT contains the output in the current data folder.

**Flags**


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/AERR = *aprxErr*</span> | Sets the approximate error, which determines how many terms of the Taylor expansion of the Gaussian are used by the calculation. Default value is 1e-5. |
| <span class="table-cell-nowrap">/WDTH = *h*</span> | Sets the Gaussian width. Default value is 1. |
| <span class="table-cell-nowrap">/OUTW = *locWave*</span> | Specifies the locations at which the output is computed. *locWave*  must have the same number of columns as *srcLocationsWave*. The other /OUT flags are mutually exclusive; you should use only one at any time. |
| <span class="table-cell-nowrap">/OUT1 = {*x1*,*nx,x2* }</span> |  |
| <span class="table-cell-nowrap">/OUT2 = {*x1*,*nx*,*x2*,*y1*,*ny*,*y2* }</span> |  |
| <span class="table-cell-nowrap">/OUT3 = {*x1*,*nx*,*x2*,*y1*,*ny*,*y2*,*z1*,*nz*,*z2* }</span> |  |
|  | Specifies gridded output of the required dimension. In each case you set the starting and ending values together with the number of intervals in that dimension. You cannot specify an output that does not match the dimensions of the input source. |
| <span class="table-cell-nowrap">/Q</span> | Does not print results in the history area. |
| <span class="table-cell-nowrap">/RX = *rx*</span> | Sets the maximum radius of any cluster. The clustering algorithm terminates when the maximum radius is less than *rx*. Without /RX, the maximum radius is the same as the maximum radius encountered. |
| <span class="table-cell-nowrap">/RY = *ry*</span> | Sets the upper bound for the distance between an observation point and a cluster center for which the cluster contributes to the transform value. The default value of *ry* is 4 times the Gaussian width as specified by the /WDTH flag. |
| <span class="table-cell-nowrap">/TET = *nTerms*</span> | Sets the number of terms in the Taylor expansion. Use /TET to set the number of terms and bypass the default error estimate, which is estimated from the approximate error value (/AERR). |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The discrete Gauss transform can be computed as a direct sum. An exact calculation is practical only for moderate number of sources and observation points and for low spatial dimensionality. With increasing dimensionality and increasing number of sources it is more efficient to take advantage of some properties of the Gaussian function. The FastGaussianTransform operation does so in two ways: It first arranges the sources in N-dimensional spatial clusters so that it is not necessary to compute the contributions of all source points that belong to remote clusters (see [FPClustering](/igorpro/commands/fpclustering.md)). The second component of the algorithm is an approximation that factorizes the sum into a factor that depends only on source points and a factor that depends only on observation points. The factor that depends only on source points is computed only once while the factor that depends on observation points is evaluated once for each observation point.

The trade-off between computation efficiency and accuracy can be adjusted using multiple parameters. By default, the operation calculates the number of terms it needs to use in the Taylor expansion of the Gaussian. You can modify the default approximate error value using /AERR or you can directly set the number of terms in the expansion using /TET.

FastGaussianTransform supports calculations in dimensions that may exceed the maximum allowed wave dimensionality. Therefore, *srcLocationsWave* must be a 2D, real-valued single- or double-precision wave in which each row corresponds to a single source position and columns represent the components in each dimension (e.g., a triplet wave would represent 3D source locations). *srcWeightsWave* must have the same number of rows as *srcLocationsWave* and it must be a real-valued single- or double-precision wave. In most applications *srcWeightsWave* will have a single column so that the output **G** will be scalar. However, if *srcWeightsWave* has multiple columns than **G** is a vector. This can be handy if you need to test multiple sets of coefficients at one time. If you specify observation points using /OUTW then *locWave* must have the same number of columns as *srcLocationsWave* (the number of rows in the output is arbitrary). The operation does not support wave scaling.

### *See Also* {#see-also}
[CWT](/igorpro/commands/cwt.md) , [FFT](/igorpro/commands/fft.md), [ImageInterpolate](/igorpro/commands/imageinterpolate.md), [Loess](/igorpro/commands/loess.md), [FPClustering](/igorpro/commands/fpclustering.md)

### *References* {#references}
Yang, C., R. Duraiswami, and L. Davis, Efficient Kernel Machines Using the Improved Fast Gauss Transform, *Advances in Neural Information Processing Systems*, *16*, 2004.