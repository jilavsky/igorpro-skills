---
description: "The ImageRemoveBackground operation removes a general background level, described by a polynomial of a specified order, from the image in srcWave."
slug: /commands/imageremovebackground
---

<div className="command-signature">

## <strong>ImageRemoveBackground</strong>  /R=<em>roiWave</em>  [/F/O/W][/P=<em>polynomial</em> <em>order</em> ] <em>srcWave</em> {#imageremovebackground}

</div>

The ImageRemoveBackground operation removes a general background level, described by a polynomial of a specified order, from the image in *srcWave* . The result of the operation are stored in the wave M_RemovedBackground.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destW*</span> | Use this flag to designate the output wave containing the processed image. By default ImageMorphology saves the output in the wave M_RemovedBackground in the current data folder. |
|  | The /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTC = *destC*</span> | Use this flag to designate the output fitting coefficients wave. By default ImageMorphology saves the output in the wave W_BackgroundCoeff in the current data folder. |
|  | The /DSTC flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/F</span> | Computes only the background surface fit. This option will not subtract the fit from the image and will only store the resulting fit in M_RemovedBackground. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all the specified destination waves as a free waves. This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions and only if the destination wave names are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/O</span> | Use this flag to specify if the original wave is to be overwritten. |
| <span class="table-cell-nowrap">/P = *polynomial order*</span> |  |
|  | Specifies the order of the polynomial fit to the background surface. If omitted, order is assumed to be 1. |
| <span class="table-cell-nowrap">/R = *roiWave*</span> | Specify a region of interest (ROI). The ROI is defined by a wave of type unsigned byte (/B/U), which has the same number of rows and columns as the image wave. |
|  | Set the pixels that define the background region to 1. The remaining pixels can be any value other than 1. We recommend using 64 which Igor image processing operations often interpret as "blank" in unsigned byte image waves. |
|  | The ROI does not have to be contiguous. |
|  | See [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md) for more information on creating ROI waves. |
| <span class="table-cell-nowrap">/W</span> | Specifies that the coefficients of the polynomial are to be saved in the wave W_BackgroundCoeff. |



### *Details* {#details}
The identification of the background is done via the ROI wave. Set the pixels that define the background region to 1. The remaining pixels can be any value other than 1. We recommend using 64 which Igor image processing operations often interpret as "blank" in unsigned byte image waves.

The operation first performs a polynomial fit to the points designated by the ROI wave using the specified polynomial order. A polynomial of order N corresponds to the function:

$$
\displaystyle F_{N}(x, y)=\sum_{m=0}^{N} \sum_{n=0}^{m} c_{n m} x^{m-n} y^{n} .
$$

Using the polynomial fit, a surface corresponding to the polynomial is subtracted from the source wave and the result is saved in M_RemovedBackground, unless the /O flag is used, in which case the original wave is overwritten.

Use the /W flag if you want the coefficients of the polynomial to be saved in the wave W_BackgroundCoeff. The coefficients are stored in the same order as the terms in the sums above.

If you do not specify the polynomial order using the /P flag, the default order is 1, which means that the operation subtracts a plane (fitted to the ROI data) from the source image.

Note, if the image is stored as a wave of unsigned byte, short, or long, you might consider converting it into single precision (using Redimension/S) before removing the background. To see why this is important, consider an image containing a region of pixels equal to zero and subtracting a background plane corresponding to a nonconstant value. After subtraction, at least some of the pixels in the zero region should become negative, but because they are stored as unsigned quantities, they appear incorrectly as large values.

### *Example* {#example}
See [Background Removal](/igorpro/analysis/image-processing.md#background-removal).

### *See Also* {#see-also}
[Image Processing](/igorpro/analysis/image-processing.md)

The [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md) operation for creating ROIs.