---
description: "The ImageMorphology operation performs one of several standard image morphology operations on the source ImageMatrix."
slug: /commands/imagemorphology
---

<div className="command-signature">

## <strong>ImageMorphology</strong>  [/E=<em>SE</em>#  /I=<em>iterations</em> /L/N/O/R=<em>roiSpec</em>  /S= <em>StructureElement</em>  /W=<em>whiteValue</em>  /X=<em>xOrigin</em>  /Y=<em>yOrigin</em> /Z=<em>zOrigin</em> ] <em>Method</em>  <em>ImageMatrix</em> {#imagemorphology}

</div>

The ImageMorphology operation performs one of several standard image morphology operations on the source *ImageMatrix*. Unless the /O flag is specified, the resulting image is saved in the wave M_ImageMorph. The operation applies only to waves of type unsigned byte. All ImageMorphology methods except for watershed use a structure element. The structure element may be one of the built-in elements (see /E below) or a user specified element.

Erosion, Dilation, Opening and Closing are the only methods supported for 3D *ImageMatrix.*

### *Parameters* {#parameters}
*Method*  is one of the following names:


|  |  |
| --- | --- |
| BinaryErosion | Performs an erosion of the source binary image using a built-in or user specified structure element (see /E and /S flags). |
| BinaryDilation | Performs a dilation of the source binary image using a built-in or user specified structure element (see /E and /S flags). |
| Closing | Performs the closing operation (dilation followed by erosion). The same structure element is used in both erosion and dilation. Note that this operation is an idempotent which means that there is no point of executing it more than once. |
| Dilation | Performs a dilation of the source grayscale image using either a built-in structure element or a user specified structure element. The operation supports only 8-bit gray images. |
| Erosion | Performs an erosion of the source grayscale image using either a built-in structure element or a user specified structure element. The operation supports only 8-bit gray images. |
| Opening | Performs an opening operation (erosion followed by dilation). The same structure element is used in both erosion and dilation.  Note that this operation is an idempotent which means that there is no point of executing it more than once. |
| TopHat | Calculates the difference between the eroded image and dilated image using the same structure element. |
| Watershed | Calculates the watershed regions for grayscale or binary image. Use the /N flag to mark all nonwatershed lines as NaNs. The /L flag switches from using 4 neighboring pixels (default) to 8 neighboring pixels. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destW*</span> | Use this flag to designate the destination of the output image. By default ImageMorphology saves the output in the wave M_ImageMorph in the current data folder. |
|  | The /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destW* as a free wave. This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions and only if *destW*, as specified by /DEST, is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/E = *id*</span> | Use a particular built in structure element. See the table below in ***Structure Elements for /E*** for details on built-in structure elements and their *id*. Make sure to use the appropriate *id* for the dimensionality of *ImageMatrix.* |
|  | Note that this flag has no effect in watershed calculations. |
| <span class="table-cell-nowrap">/I = *iterations*</span> | Repeat the operation a specified number of times. |
| <span class="table-cell-nowrap">/L</span> | Use 8-connected neighbors instead of 4. |
| <span class="table-cell-nowrap">/N</span> | Sets the background level to 64 (=NaN) |
| <span class="table-cell-nowrap">/O</span> | Overwrites the source wave with the output |
| <span class="table-cell-nowrap">/R = *roiSpec*</span> | Specify a region of interest (ROI). The ROI is defined by a wave of type unsigned byte (/b/u). The ROI wave must have the same number of rows and columns as the image wave. The ROI itself is defined by the entries/pixels whose values are 0. Pixels outside the ROI can take any nonzero value. The ROI does not have to be contiguous and can take any arbitrary shape. See [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md) for more information on creating ROI waves. |
|  | In general, the *roiSpec*  has the form {*roiWaveName* , *roiFlag*}, where *roiFlag* can take the following values: |
|  |<table class="nested-table"><tbody><tr><td>***roiFlag***</td><td>**Meaning**</td></tr><tr><td>0</td><td>set pixels outside the ROI to 0</td></tr><tr><td>1</td><td>set pixels outside the ROI as in original image</td></tr><tr><td>2</td><td>set pixels outside the ROI to NaN (=64)</td></tr></tbody></table>
|  | By default *roiFlag* is set to 1 and it is then possible to use the /R flag using the abbreviated form /R=*roiWave*. |
| <span class="table-cell-nowrap">/S = *seWave*</span> | Specifies your own structure element. |
|  | *seWave* must be of type unsigned byte with pixels that belong to the structure element set to 1 and background pixels set to 0. |
|  | There are no limitations on the size of the structure element and you can use the /X and /Y flags to specify the origin of your structure element. |
| <span class="table-cell-nowrap">/W = *whiteVal*</span> | Use this flag if your white value in the binary image is different than 255. The black level is assumed to be zero. |
| <span class="table-cell-nowrap">/X = *xOrigin*</span> | Specifies the X-origin of a user-defined structure element starting at 0. If you do not use this flag Igor sets the origin to the center of the specified structure element. |
| <span class="table-cell-nowrap">/Y = *yOrigin*</span> | Specifies the Y-origin of a user-defined structure element starting at 0. If you do not use this flag Igor sets the origin to the center of the specified structure element. |
| <span class="table-cell-nowrap">/Z = *zOrigin*</span> | This flag should only be used for 3D structure elements to specify the Z-origin of the element. If you do not use this flag Igor sets the origin to the center of the specified structure element. |

### *Structure Elements for /E* {#structure-elements-for-e}

| *id* | Element | Origin | Shape |
| --- | --- | --- | --- |
| 1 | 2x2 | (0,0) | square (default) |
| 2 | 1x3 | (1,1) | row (in 3x3 square) |
| 3 | 3x1 | (1,1) | column (in 3x3 square) |
| 4 | 3x3 | (1,1) | cross (in 3x3 square) |
| 5 | 5x5 | (2,2) | circle(in 5x5 square) |
| 6 | 3x3 | (1,1) | full 3x3 square |
| 200 | 2x2x2 | (1,1,1) | symmetric cube |
| 202 | 2x2x2 | (1,1,1) | 2 voxel column in y direction |
| 203 | 2x2x2 | (1,1,1) | 2 voxel column in x direction |
| 204 | 2x2x2 | (1,1,1) | 2 voxel column in z direction |
| 205 | 2x2x2 | (1,1,1) | XY plane |
| 206 | 2x2x2 | (1,1,1) | YZ plane |
| 207 | 2x2x2 | (1,1,1) | XZ plane |
| 300 | 3x3x3 | (1,1,1) | symmetric cube |
| 301 | 3x3x3 | (1,1,1) | symmetric ball |
| 302 | 3x3x3 | (1,1,1) | 3 voxel column in y direction |
| 303 | 3x3x3 | (1,1,1) | 3 voxel column in x direction |
| 304 | 3x3x3 | (1,1,1) | 3 voxel column in z direction |
| 305 | 3x3x3 | (1,1,1) | XY plane |
| 306 | 3x3x3 | (1,1,1) | YZ plane |
| 307 | 3x3x3 | (1,1,1) | XY plane |
| 500 | 5x5x5 | (2,2,2) | symmetric cube |
| 501 | 5x5x5 | (2,2,2) | symmetric ball |
| 700 | 7x7x7 | (3,3,3) | symmetric cube |
| 701 | 7x7x7 | (3,3,3) | symmetric ball |

### *Examples* {#examples}
If you would like to apply a morphological operation to a wave whose data type is not an unsigned byte and you wish to retain the wave's dynamic range, you can use the following approach:


```igor
Function ScaledErosion(inWave)
	Wave inWave
	
	WaveStats/Q inWave
	Variable nor=255/(V_max-V_min)
	MatrixOp/O tmp=nor*(inWave-V_min)
	Redimension/B/U tmp
	ImageMorphology/E=5 Erosion tmp
	Wave M_ImageMorph
	MatrixOp/O inWave=(M_ImageMorph/nor)+V_min
	KillWaves/Z tmp,M_ImageMorph
End
```

### *See Also* {#see-also}
[Image Processing](/igorpro/analysis/image-processing.md), [Morphological Operations](/igorpro/analysis/image-processing.md#morphological-operations), [Particle Analysis](/igorpro/analysis/image-processing.md#particle-analysis).

The [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md) operation for creating ROIs.