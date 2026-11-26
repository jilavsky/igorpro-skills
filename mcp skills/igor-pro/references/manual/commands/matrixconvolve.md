---
description: "The MatrixConvolve operation convolves a small coefficient matrix kernelWave with srcWave."
slug: /commands/matrixconvolve
---

<div className="command-signature">

## <strong>MatrixConvolve</strong>  [/R=<em>roiWave</em> ] <em>kernelWave</em>, <em>srcWave</em> {#matrixconvolve}

</div>

The MatrixConvolve operation convolves a small coefficient matrix *kernelWave* with *srcWave*.  If /DEST is not specified, the operation overwrites *srcWave* with the convolution output.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | specify the destination wave for the output of the convolution. |
|  | The /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified *destWave* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/R = *roiWave*</span> | Modifies only data contained inside the region of interest. The ROI wave should be 8-bit unsigned with the same dimensions as *srcWave*. The interior of the ROI is defined by zeros and the exterior is defined by any nonzero value. |

### *Details* {#details}
On input *kernelWave* contains an *N*x*M*  matrix of coefficients where *N*  and *M*  should be odd. Generally *N*  and *M*  will be equal. If *N*  and *M*  are greater than 13, it is more efficient to perform the convolution using the Fourier transform (see [FFT](/igorpro/commands/fft.md) or [MatrixOP](/igorpro/commands/matrixop.md)).

The convolution is performed in place on the data matrix and is acausal, i.e., the output data is not shifted.

Edges are handled by replication of edge data.

When *srcWave*  is an integer type, the results are clipped to limits of the given number type. For example, unsigned byte is clipped to the range [0, 255].  To avoid clipping you can promote *srcWave* to SP or DP.

MatrixConvolve works also when both *kernelWave* and *srcWave* are 3D waves. In this case the convolution result is placed in the wave M_Convolution in the current data folder, and the optional /R=*roiWave* is required to be an unsigned byte wave which has the same dimensions as *srcWave*.

This operation applies only to real numeric waves.

### *See Also* {#see-also}
[MatrixFilter](/igorpro/commands/matrixfilter.md), [ImageFilter](/igorpro/commands/imagefilter.md) and [MatrixOp](/igorpro/commands/matrixop.md) for convolutions.

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.

[Loess](/igorpro/commands/loess.md)