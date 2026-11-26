---
description: "ImageHistModification performs a modification of the image histogram and saves the results in the wave M_ImageHistEq or as specified by the /DEST flag."
slug: /commands/imagehistmodification
---

<div className="command-signature">

## <strong>ImageHistModification</strong>  [/A [/B=<em>bins</em> ][/C=<em>cFactor</em> ]] [/H=<em>hRegions</em> ] [/O/I] [/R=<em>roiSpec</em> ][/V=<em>vRegions</em> ][/W=<em>waveName</em> ] <em>ImageMatrix</em> {#imagehistmodification}

</div>

ImageHistModification performs a modification of the image histogram and saves the results in the wave M_ImageHistEq or as specified by the /DEST flag. If /W is not specified, the operation is a simple histogram equalization of *ImageMatrix.* If /W is specified, the operation attempts to produce an image with a histogram close to *waveName*. If /A is specified, the operation performs an adaptive histogram equalization. *ImageMatrix* is a wave of any noncomplex numeric type.  Adaptive histogram equalization applies only to 2D waves while the remaining parts of the operation apply both to 2D and 3D waves.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Performs an adaptive histogram equalization by subdividing the image into a minimum of 4 rectangular domains and using interpolation to account for the boundaries between adjacent domains. When the /C flag is specified with contrast factor greater than 1, this operation amounts to contrast-limited adaptive histogram equalization. By default the operation divides the image into 8 horizontal and 8 vertical regions. See /H and /V below. |
| <span class="table-cell-nowrap">/B = *bins*</span> | Specify the number of bins used with the /A feature. If not specified, this value defaults to 256. |
| <span class="table-cell-nowrap">/C = *cFactor*</span> | Specify a contrast factor (or clipping value) above which pixels are equally distributed over the whole range. *cFactor* must be greater than 1, in the limit as *cFactor*→1 the operation is a regular adaptive histogram equalization. |
|  | <div><Admonition type="note"><p>This flag is used only with the /A flag.</p></Admonition></div> |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave. |
|  | When used in a function, ImageHistModification creates a real wave reference for the *destWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/H = *hRegions*</span> | Specify the number of horizontal subdivisions to be used with the /A feature. Note, the number of image pixels in the horizontal direction must be an integer multiple of *hRegions.* |
| <span class="table-cell-nowrap">/I</span> | This is an extension of standard histogram equalization that uses 2<sup>16</sup> bins instead of 2<sup>8</sup> when calculating histogram equalization. This feature does not apply to the adaptive histogram equalization (/A flag). |
| <span class="table-cell-nowrap">/O</span> | Overwrites the source image. If this flag is not specified, the resulting image is saved in the wave M_ImageHistEq or as specified by the /DEST flag. |
| <span class="table-cell-nowrap">/R = *roiSpec*</span> | Specify a region of interest (ROI). The ROI is defined by a wave of type unsigned byte (/b/u). The ROI wave must have the same number of rows and columns as the image wave. The ROI itself is defined by the entries/pixels whose values are 0. Pixels outside the ROI can take any nonzero value. The ROI does not have to be contiguous and can take any arbitrary shape. |
|  | In general, the *roiSpec*  has the form {*roiWaveName*, *roiFlag*}, where *roiFlag* can take the following values: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Set pixels outside the ROI to 0</td></tr><tr><td>1:</td><td>Set pixels outside the ROI as in original image</td></tr><tr><td>2:</td><td>Set pixels outside the ROI to NaN (i.e., 64)</td></tr></tbody></table>
|  | By default *roiFlag*  is set to 1 and it is then possible to use the /R flag using the abbreviated form /R=*roiWave*. When *imageMatrix* is a 3D wave, *roiWave* can be either a 2D wave as described above (matching the number of rows and columns in *imageMatrix*) or it can be a 3D wave which must have the same number of rows, columns, and layers as *imageMatrix*. When using a 2D roiWave with a 3D *imageMatrix* the ROI is understood to be defined by *roiWave* for each layer in the 3D wave. |
|  | See [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md) for more information on creating ROI waves. |
| <span class="table-cell-nowrap">/V = *vRegions*</span> | Specifies the number of vertical subdivisions to be used with the /A flag. Note, the number of image pixels in the horizontal direction must be an integer multiple of *vRegions* . If the dimensions of the image are not divisible by the number of regions that you want, you can pad the image using [ImageTransform](/igorpro/commands/imagetransform.md) with the padImage keyword. |
| <span class="table-cell-nowrap">/W = *waveName*</span> | A 256-point wave that specifies the desired histogram. The operation will attempt to produce an image having approximately the desired histogram values. This flag does not apply to the adaptive histogram equalization (/A flag). |

### *See Also* {#see-also}
The [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md) and [ImageTransform](/igorpro/commands/imagetransform.md) operations for creating ROIs.

[Image Processing](/igorpro/analysis/image-processing.md)