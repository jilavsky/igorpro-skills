---
description: "The MatrixFilter operation performs one of several standard image filter type operations on the destination dataMatrix."
slug: /commands/matrixfilter
---

<div className="command-signature">

## <strong>MatrixFilter</strong>  [/b=<em>b</em> /M=<em>rank</em> /N=<em>n</em> /P=<em>nIterations</em> /R=<em>roiWave</em> /T] <em>Method</em>  <em>dataMatrix</em> {#matrixfilter}

</div>

The MatrixFilter operation performs one of several standard image filter type operations on the destination *dataMatrix*.

:::note
The parameters below are also available in ImageFilter. See ImageFilter for additional parameters.
:::

### *Parameters* {#parameters}

*Method* selects the filter type. *Method* is one of the following names:

|  |  |
| --- | --- |
| avg | *n* x*n* average filter. |
| FindEdges | 3x3 edge finding filter. |
| gauss | *n* x*n* gaussian filter. |
| gradN, gradNW, gradW, gradSW, gradS, gradSE, gradE, gradNE |  |
|  | 3x3 North (NorthWest, West...) pointing gradient filter. |
| max | *n* x*n* maximum rank filter. |
| median | *n* x*n* median filter. You can assign values other than the median by specifying the desired rank using the /M flag. |
| min | *n* x*n* minimum rank filter. |
| NanZapMedian | *n* x*n* filter that only affects data points that are NaN. replaces them with the median of the *n* x*n* surrounding points. Unless /P is used, automatically cycles through matrix until all NaNs are gone or until *cols*\**rows* iterations. |
| point | 3x3 point finding filter 8\**center* -*outer*. |
| sharpen | 3x3 sharpening *filter* =(12\**center* -*outer*)/4. |
| sharpenmore | 3x3 sharpening *filter* =(9\**center* -*outer*). |
| thin | Calculates binary image thinning using neighborhood maps based on the algorithm in "Graphics Gems IV", p. 465. |
|  | <div><Admonition type="warning"><p>The thin keyword to MatrixFilter will be removed someday. The functionality will be available - just not as a part of MatrixFilter. The /R flag does not apply to the lame duck thin keyword.</p></Admonition></div> |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *b*</span> | Specifies the value that is considered background. Used with thin. If object is black on white background, use 255. If object is white on a black background, use 0. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave.  By default MatrixFilter overwrites the input with the filtered output while ImageFilter supports the /O flag. |
|  | It is an error to specify the same wave as both *dataMatrix* and *destWave*. |
|  | When used in a function, MatrixFilter and ImageFilter create a real wave reference for the *destWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/F = *value*</span> | Specifies the value in the ROI wave that marks excluded pixels. *value* is either 0 or 1. |
|  | This flag was added in Igor Pro 7.00. |
|  | By default, and for compatibility with Igor Pro 6, *value* is 0. Use /F=1 if your ROI wave contains 1 for pixels to be excluded. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/M = *rank*</span> | Assigns a pixel value other than the median when used with the median filter. Valid *rank* values are between 0 and n^2-1 (for the default median *rank*= n^2/2). |
| <span class="table-cell-nowrap">/N = *n*</span> | For any method described above as "*n* x*n* ", you can specify that the filtering kernel will be a square matrix of size *n*. In the absence of the /N flag, the default is 3. |
| <span class="table-cell-nowrap">/P = *nIterations*</span> | The filter is passed over the data *nIterations*. The default is one pass. |
| <span class="table-cell-nowrap">/R = *roiWave*</span> | Only the data outside the region of interest will be modified. The ROI wave should be 8-bit unsigned with the same dimensions as the data matrix. The exterior of the ROI is defined by zeros and the interior is any nonzero value. |
| <span class="table-cell-nowrap">/T</span> | Applies the thining algorithm of Zhang and Suen with the thin parameter. The wave M_MatrixFilter contains the results; the input wave is not overwritten. |

### *Details* {#details}
This operation does not support complex waves.

### *See Also* {#see-also}
[ImageFilter](/igorpro/commands/imagefilter.md) for descriptions of additional parameters.

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.

[Image Processing](/igorpro/analysis/image-processing.md)

[Loess](/igorpro/commands/loess.md)

### *References* {#references}
Heckbert, Paul S., (Ed.), *Graphics Gems IV*, Morgan Kaufmann Publishers, 1994.

Zhang, T. Y., and C. Y. Suen, A fast thinning algorithm for thinning digital patterns, *Comm. of the ACM*, *27*, 236-239, 1984.