---
description: "The ImageStats operation calculates wave statistics for specified regions of interest in a real matrix wave."
slug: /commands/imagestats
---

<div className="command-signature">

## <strong>ImageStats</strong>  [ <em>flags</em> ] <em>imageWave</em> {#imagestats}

</div>

The ImageStats operation calculates wave statistics for specified regions of interest in a real matrix wave. The operation applies to image pixels whose corresponding pixels in the ROI wave are set to zero. It does not print any results in the history area.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/BEAM</span> | Computes the average, minimum, and maximum pixel values in each layer of a 3D wave and 2D ROI. Output is to waves W_ISBeamAvg, W_ISBeamMax, and W_ISBeamMin in the current data folder. Use /RECT to improve efficiency for simple ROI domains.  V_ variable results correspond to the last evaluated layer of the 3D wave. Do not use /G, /GS, or /P with this flag. Set /M=1 for maximum efficiency. |
| <span class="table-cell-nowrap">/BRXY = {*xWave* , *yWave* }</span> |  |
|  | Use this option with a 3D *imageWave*. It provides a more efficient method for computing average, minimum and maximum values when the set of points of interest is much smaller than the dimensions of an image. |
|  | Here *xWave* and *yWave* are 1D waves with the same number of points containing XY integer pixel locations specifying arbitrary pixels for which the statistics are calculated on a plane by plane basis as follows: |
|  | $$ \displaystyle {W\_ISBeamAvg}[{k}]=\frac{1}{n} \sum_{i=1}^{n} {Image}[{xWave}[i]][{yWave}[i]] . $$ |
|  | Pixel locations are zero-based; non-integer entries may produce unpredictable results. |
|  | The calculated statistics for each plane are stored in the current data folder in the waves W_ISBeamAvg, W_ISBeamMax and W_ISBeamMin or in destination waves provided by /DSTA, /DSTN and /DSTX. |
|  | Note: This flag is not compatible with any other except /BEAM. |
| <span class="table-cell-nowrap">/C = *chunk*</span> | When *imageWave* is a 4D wave, /C specifies the chunk for which statistics are calculated. By default *chunk* =0. |
|  | Added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/DSTA = *dstBA*</span> | Specifies the destination for the output beam average wave (W_ISBeamAvg). |
|  | When used in a function, ImageStats creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DSTA flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTN = *dstBMin*</span> | Specifies the destination for the output beam minimum wave (W_ISBeamMin). |
|  | When used in a function, ImageStats creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DSTN flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTX = *dstBMax*</span> | Specifies the destination for the output beam maximum wave (W_ISBeamMax). |
|  | When used in a function, ImageStats creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DSTX flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the destination waves as free waves. /FREE is allowed only in functions and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/G = {*startP*, *endP*, *startQ*, *endQ* }</span> |  |
|  | Specifies the corners of a rectangular ROI. When this flag is used, an ROI wave is not required. This flag requires that *startP* <= *endP* and *startQ* <= *endQ*. When the parameters extend beyond the image area, the command will not execute and V_flag will be set to -1. You should therefore verify that V_flag=0 before using the results of this operation. |
| <span class="table-cell-nowrap">/GS = {*sMinRow*, *sMaxRow*, *sMinCol*, *sMaxCol* }</span> |  |
|  | Specifies a rectangular region of interest in terms of the scaled image coordinates. Each one of the 4 values will be translated to an integer pixel using truncation. |
|  | This flag, /G, and an ROI specification are mutually exclusive. |
| <span class="table-cell-nowrap">/M = *val*</span> | Calculates the average and locates the minimum and the maximum in the ROI when /M=1. This will save you the computation time associated with calculating the higher order statistical moments. |
| <span class="table-cell-nowrap">/P = *planeNumber*</span> |  |
|  | Restricts the calculation to a particular layer of a 3D wave. By default, *planeNumber*= -1 and only the first layer of the wave is processed. |
| <span class="table-cell-nowrap">/R = *roiWave*</span> | Specifies a region of interest (ROI) in the image. The ROI is defined by a wave of type unsigned byte (/b/u), which has the same number of rows and columns as the image wave. The ROI itself is defined by the entries/pixels whose value are 0. Pixels outside the ROI can take any nonzero value. The ROI does not have to be contiguous. See [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md) for more information on creating ROI waves. |
| <span class="table-cell-nowrap">/RECT = {*minRow*, *maxRow*, *minCol*, *maxCol* }</span> |  |
|  | Limits the range of the ROI to a rectangular pixel range with /BEAM. |

### *Details* {#details}
The image statistics are returned via the following variables:


|  |  |
| --- | --- |
| V_adev | Average deviation of pixel values. |
| V_avg | Average of pixel values. |
| V_kurt | Kurtosis of pixel values. |
| V_min | Minimum pixel value. |
| V_minColLoc | Specifies the column index where the minimum pixel value was found. The variable is set to -1 if a minimum was not found (e.g., if all pixels were NaN). |
| V_minLayerLoc | Specifies the layer index of the layer in which the minimum voxel was found. The variable is set to NaN if *imageWave* is not 3D. |
| V_minRowLoc | Specifies the index of the row where the minimum pixel value was found. The variable is set to -1 if a minimum was not found (e.g., if all values were NaN). |
| V_max | Maximum pixel value. |
| V_maxColLoc | Specifies the index of the column in which the maximum pixel value was found. The variable is set to -1 if a maximum was not found (e.g., if all values were NaN). |
| V_maxLayerLoc | Specifies the layer index of the layer in which the maximum voxel was found. The variable is set to NaN if *imageWave* is not 3D. |
| V_maxRowLoc | Specifies the index of the row in which the maximum pixel value was found. The variable is set to -1 if a maximum was not found (e.g., if all values were NaN). |
| V_npnts | Number of points in the ROI excluding NaNs. |
| V_rms | Root mean squared of pixel values. |
| V_sdev | Standard deviation of pixel values. |
| V_skew | Skewness of pixel values. |

Most of these statistical variables are defined as in the [WaveStats](/igorpro/commands/wavestats.md) operation. If there is no ROI, WaveStats will be more efficient and convenient to use when calculating statistics for an entire wave.

If *imageWave* is 4D, it may be convenient to use the reversible conversion:


```igor
Redimension/N=(rows,cols,layers*chunks) ImageWave
```

which allows you to obtain the statistics for each layer and all chunks of the wave. To convert the wave back to 4D, execute:


```igor
Redimension/N=(rows,cols,layers,chunks) ImageWave
```

This form of the Redimension operation does not move data in memory.

### *See Also* {#see-also}
[ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md), [MatrixOP](/igorpro/commands/matrixop.md), [mean](/igorpro/commands/mean.md), [median](/igorpro/commands/median.md), [variance](/igorpro/commands/variance.md), [WaveMinAndMax](/igorpro/commands/waveminandmax.md), [WaveStats](/igorpro/commands/wavestats.md)

[Image Processing](/igorpro/analysis/image-processing.md).