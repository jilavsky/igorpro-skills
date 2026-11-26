---
description: "The ImageRestore operation performs the Richardson-Lucy iterative image restoration."
slug: /commands/imagerestore
---

<div className="command-signature">

## <strong>ImageRestore</strong>  [/Z /ITER=<em>iterations</em>  /DEST=<em>destWave</em>] <em>srcWave</em>=<em>wSrc</em> , <em>psfWave</em>=<em>wPSF</em>  [, <em>relaxationGamma</em>=<em>h</em> , <em>startingImage</em>=<em>wRecon</em> ] {#imagerestore}

</div>

The ImageRestore operation performs the Richardson-Lucy iterative image restoration.


### *Parameters* {#parameters}
|  |  |
| --- | --- |
| <span class="table-cell-nowrap">psfWave = *wPSF*</span> | Specifies a known point spread function. *wPSF* must be a 2D (square NxN) wave of the same numeric type as *wSRC* . N must be an odd number greater than 1. |
| <span class="table-cell-nowrap">relaxationGamma = *h*</span> |  |
|  | Specifies positive power gamma of in the relaxation mapping (see Details). |
| <span class="table-cell-nowrap">startingImage = *wRecon*</span> |  |
|  | Use this keyword to specify a starting image that could be for example the output from a previous call to this operation. *wRecon* must have the same dimensions as *wSRC* and the same numeric type. |
|  | You must make sure that *wRecon* is not the user-specified or the default destination wave of the operation. |
| <span class="table-cell-nowrap">srcWave = *wSrc*</span> |  |
|  | Specifies the degraded image which must be a 2D single-precision or double-precision real wave. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> | Specifies the desired output wave. |
|  | If /DEST is omitted, the output from the operation is stored in the wave M_Reconstructed in the current data folder. |
| <span class="table-cell-nowrap">/FREE</span> | Creates destWave as a free wave. |
|  | /FREE is allowed only in functions and only if the destination wave names are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/ITER = *iterations*</span> | Specifies the number of iterations. The default number of iterations is 100. |
| <span class="table-cell-nowrap">/Z</span> | Do not report errors. |

### *Details* {#details}
ImageRestore performs the Richardson-Lucy iteration solution to the deconvolution of an image. The input consists of the degraded image and point spread function as well as the desired number of iterations.

The operation allows you to apply additional iterations by setting the starting image to the restored output wave from a previous call to ImageRestore using the startingImage keyword. If startingImage is omitted, the starting image is created by ImageRestore with each pixel set to the value 1.

In the case of stellar images it may be useful to apply a relaxation step that involves scaling the correction evaluated at each iteration by

$$
\displaystyle \operatorname{factor}(v)=\sin \left(\frac{\pi}{2} \frac{v-v_{\min }}{v_{\max }-v_{\min }}\right)^{\gamma},
$$

where *v* is pixel value, *vmax* and *vmin* are the maximum and minimum level pixels in the image, and gamma is the user-specified *relaxationGamma*.

**References**

W.H. Richardson, "Bayesian-Based Iterative Method of Image Restoration". *JOSA 62 (1)* : 55–59, 1972.

L.B. Lucy, "An iterative technique for the rectification of observed distributions", *Astronomical Journal 79*, *6* : 745–754, 1974.