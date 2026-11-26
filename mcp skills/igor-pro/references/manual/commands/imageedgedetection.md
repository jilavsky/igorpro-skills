---
description: "The ImageEdgeDetection operation performs one of several standard image edge detection operations on the source wave ImageMatrix."
slug: /commands/imageedgedetection
---

<div className="command-signature">

## <strong>ImageEdgeDetection</strong>  [<em>flags</em>] <em>Method</em>  <em>ImageMatrix</em> {#imageedgedetection}

</div>

The ImageEdgeDetection operation performs one of several standard image edge detection operations on the source wave *ImageMatrix*.

Unless the /O flag is specified, the resulting image is saved in the wave M_ImageEdges or in the wave specified by the /DEST flag.

The edge detection operations below produce binary images on output; the background is set to 0 and the edges to 255. This is due, in most cases to a thresholding performed in the final stage.

Except for the case of marr and shen detectors, you can use the /M flag to specify a method for automatic thresholding; see the [ImageThreshold](/igorpro/commands/imagethreshold.md) /M flag.

### *Parameters* {#parameters}
*Method*  selects type of edge detection. *Method*  is one of the following names:


|  |  |
| --- | --- |
| canny | Canny edge detector uses smoothing before edge detection and thresholding. You can optionally specify the threshold using the /T flag and the smoothing factor using /S. |
| frei | Calculates the Frei-Chen edge operator (see Pratt p. 503) using only the row and column filters. |
| kirsch | Kirsch edge detector (see Pratt p. 509). Performs convolution with 8 masks calculating gradients. |
| marr | Marr-Hildreth edge detector. Performs two convolutions with Laplacian of Gaussian and then detects zero crossings. Use the /S flag to define the width of the convolution kernel. |
| prewitt | Calculates the Prewitt compass gradient filters. Returns the result for the largest filter response. |
| roberts | Calculates the square root of the magnitude squared of the convolution with the Robert's row and column edge detectors. |
| shen | Shen-Castan optimized edge detector. Supposed to be effective in the presence of noise. The flags that modify this operation are: /F for the threshold ratio (0.9 by default), /S for smoothness factor (0.9 by default), /W for window width (default is 10 ), /H for thinning factor which by default is 1. |
| sobel | Sobel edge detector using convolutions with row and column edge gradient masks (see Pratt p. 501). |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave. |
|  | It is an error to specify the same wave as both *ImageMatrix* and *destWave*. |
|  | When used in a function, ImageBlend creates a real wave reference for the *destWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/F = *fraction*</span> | Determines the threshold value for the shen algorithm by starting from the histogram of the image and choosing a threshold such that *fraction*  specifies the portion of the image pixels whose values are below the threshold. Valid values are in the interval (0 < *fraction* < 1). |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave. Note that /FREE does not affect the default output wave M_ImageEdges. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/H = *thinning*</span> | Ued in shen  for thinning the edges. By default the thinning value is 1. Higher values produce thinner edges. |
| <span class="table-cell-nowrap">/I</span> | inverts the output, i.e., sets the edges to 255 and the background to 0. |
| <span class="table-cell-nowrap">/M = *threshMethod*</span> |  |
|  | See [ImageThreshold](/igorpro/commands/imagethreshold.md) automatic methods for obtaining a threshold value. Methods 1, 2, 4 and 5 are supported in this operation. If you use *threshMethod*  = -1, threshold is not applied. |
|  | If you want to apply your own thresholding algorithm, use /M=6 to bypass the thresholding completely. The wave M_RawCanny contains the result regardless of any other flags you may have used. |
| <span class="table-cell-nowrap">/N</span> | Sets the background level to 64 (i.e., NaN) |
| <span class="table-cell-nowrap">/O</span> | Overwrites the source image with the output image. |
| <span class="table-cell-nowrap">/P = *layer*</span> | Applies the operation to the specified layer of a 3D wave. |
|  | /P is incompatible with /O. |
|  | /P was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/R = *roiSpec*</span> | Specify a region of interest (ROI). The ROI is defined by a wave of type unsigned byte (/b/u). The ROI wave must have the same number of rows and columns as the image wave. The ROI itself is defined by the entries/pixels whose values are 0. Pixels outside the ROI can take any nonzero value. The ROI does not have to be contiguous and can take any arbitrary shape. See [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md) for more information on creating ROI waves. |
|  | In general, the *roiSpec*  has the form {*roiWaveName* , *roiFlag* }, where *roiFlag*  can take the following values: |
|  |<table class="nested-table"><tbody><tr><td>**roiFlag**</td><td>**Meaning**</td></tr><tr><td>0</td><td>set pixels outside the ROI to 0</td></tr><tr><td>1</td><td>set pixels outside the ROI as in original image</td></tr><tr><td>2</td><td>set pixels outside the ROI to NaN (=64)</td></tr></tbody></table>
|  | By default *roiFlag*  is set to 1 and it is then possible to use the /R flag using the abbreviated form /R=*roiWave* . |
| <span class="table-cell-nowrap">/S = *smoothVal*</span> | Specify the standard deviation or the width of the smoothing filter. By default the operation uses 1. Larger values require longer computation time. In the *shen*  operation the default value is 0.9 and the valid range is (0 < *smoothVal*< 1). |
| <span class="table-cell-nowrap">/T = *thresh*</span> | Manual threshold for any method above that uses a single threshold. This is faster than using /M. |
| <span class="table-cell-nowrap">/W = *width*</span> | Used in the *shen*  operation to specify window width. By default *width* is set to 10 and it is clipped to 49. |

### *See Also* {#see-also}
[Image Processing](/igorpro/analysis/image-processing.md), [Edge Detectors](/igorpro/analysis/image-processing.md#edge-detectors), [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md), [ImageThreshold](/igorpro/commands/imagethreshold.md)

### *References* {#references}
Pratt, William K., *Digital Image Processing*, John Wiley, New York, 1991.