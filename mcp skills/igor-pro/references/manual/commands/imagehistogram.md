---
description: "ImageHistogram calculates the histogram of imageMatrix. When imageMatrix is a grayscale image, the histogram is stored in the wave W_ImageHist in the current…"
slug: /commands/imagehistogram
---

<div className="command-signature">

## <strong>ImageHistogram</strong>  [/I/P=<em>plane</em> /R=<em>roiWave</em> /S] <em>imageMatrix</em> {#imagehistogram}

</div>

ImageHistogram calculates the histogram of *imageMatrix*. When *imageMatrix* is a grayscale image, the histogram is stored in the wave W_ImageHist in the current data folder or as specified by the /DEST flag. If *imageMatrix*  is a 3D RGB or RGBA  wave, the resulting histograms for the color planes are saved in the waves W_ImageHistR, W_ImageHistG, W_ImageHistB or as specified by the flags /DSTR, /DSTG and /DSTB respectively.

*imageMatrix*  must be a real-valued numeric wave.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave for a grayscale histogram.  If this flag is not specified, the operation stores the histogram in the wave W_ImageHist in the current data folder. |
|  | When used in a function, ImageHistogram creates a real wave reference for *destWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | The waves specified as *imageMatrix*, *roiWave* and *destWave* must be distinct. |
|  | /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTR = *destRWave*</span> |  |
|  | Specifies the red plane histogram wave for an RGB image.  If this flag is not used, the operation stores the histogram in the wave W_ImageHistR in the current data folder. |
|  | When used in a function, ImageHistogram creates a real wave reference for *destRWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | The waves *imageMatrix*, *roiWave*, *destRWave, destGWave* and *destBWave* must all be distinct. |
|  | /DSTR flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTG = *destGWave*</span> |  |
|  | Specifies the green plane histogram wave for an RGB image.  If this flag is not used, the operation stores the histogram in the wave W_ImageHistG in the current data folder. |
|  | When used in a function, ImageHistogram creates a real wave reference for *destGWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | The waves specified as *imageMatrix*, *roiWave*, *destRWave, destGWave* and *destBWave* must all be distinct. |
|  | /DSTG flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTB = *destBWave*</span> |  |
|  | Specifies the blue plane histogram wave for an RGB image. If this flag is not used, the operation stores the histogram in the wave W_ImageHistB in the current data folder. |
|  | When used in a function, ImageHistogram creates a real wave reference for *destBWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | The waves specified as *imageMatrix*, *roiWave*, *destRWave, destGWave* and *destBWave* must all be distinct. |
|  | /DSTB flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all destination waves as free waves. |
|  | /FREE is allowed only in functions and only if the destination waves consist of a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/I</span> | Calculates a histogram with 65536 bins evenly distributed between the minimum and the maximum data values. The operation first finds the extrema and then calculates the bins and the resulting histogram. Data can be a 2D wave of any type including float or double. |
| <span class="table-cell-nowrap">/P = *plane*</span> | Restricts the calculation of the histogram to a specific plane when imageMatrix is a non RGB 3D wave. |
| <span class="table-cell-nowrap">/R = *roiWave*</span> | Specifies a region of interest (ROI). The ROI is defined by a wave of type unsigned byte (/b/u) that has the same number of rows and columns as *imageMatrix*. The ROI itself is defined by the entries or pixels in the *roiWave*  with value of 0. Pixels outside the ROI may have any nonzero value. The ROI does not have to be contiguous. When *imageMatrix*  is a 3D wave, *roiWave*  can be either a 2D wave (matching the number of rows and columns in *imageMatrix* ) or it can be a 3D wave that must have the same number of rows, columns and layers as *imageMatrix*. When using a 2D *roiWave*  with a 3D *imageMatrix*  the ROI is understood to be defined by *roiWave*  for each layer in the 3D wave. |
|  | See [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md) for more information on creating 2D ROI waves. |
| <span class="table-cell-nowrap">/S</span> | Computes the histogram for a whole 3D wave possibly subject to 2D or 3D ROI masking. The /S and /P flags are mutually exclusive. |

### *Details* {#details}
The ImageHistogram operation works on images, but it handles both 2D and 3D waves of any data type. Unless you use one of the special features of this operation (e.g., ROI or /P or /I) you could alternatively use the Histogram operation, which computes the histogram for the full wave and includes additional options for controlling the number of bins.

If the data type of *imageMatrix*  is single byte, the histogram will have 256 bins from 0 to 255. Otherwise, the 256 bins will be distributed between the minimum and maximum values encountered in the data. Use the /I flag to increase the number of bins to 65536, which may be useful for unsigned short (/W/U) data.

### *See Also* {#see-also}
[Image Processing](/igorpro/analysis/image-processing.md), [Histograms](/igorpro/analysis/analysis.md#histograms)

[ImageHistModification](/igorpro/commands/imagehistmodification.md), [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md)

[Histogram](/igorpro/commands/histogram.md), [JointHistogram](/igorpro/commands/jointhistogram.md)