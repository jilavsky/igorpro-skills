---
description: "The ImageFilter operation is identical to MatrixFilter, accepting the same parameters and flags, with the exception of the additional features described below."
slug: /commands/imagefilter
---

<div className="command-signature">

## <strong>ImageFilter</strong>  [/N=<em>n</em> /O /P=<em>nIterations</em> /b=<em>b</em> /R=<em>roiWave</em> ] <em>Method</em>  <em>dataMatrix</em> {#imagefilter}

</div>

The ImageFilter operation is identical to [MatrixFilter](/igorpro/commands/matrixfilter.md), accepting the same parameters and flags, with the exception of the additional features described below.

### *Parameters* {#parameters}
*Method*  selects the filter type. *Method*  is one of the following names:


|  |  |
| --- | --- |
| avg3d | *n* x *n* x *n*  average filter for 3D waves. |
| gauss3d | *n* x *n* x *n*  gaussian filter for 3D waves. |
| hybridmedian | Implements ranking pixel values between two groups of pixels in a 5x5 neighborhood. The first group includes the horizontal and vertical lines through the center, the second group includes the diagonal lines through the center, and both groups include the center pixel itself. The resulting median value is the ranked median of both groups and the center pixel. |
| max3d | *n* x *n* x *n*  maximum rank filter for 3D waves. |
| median3d | *n* x *n* x *n*  median filter for 3D waves where *n*  must be of the form 3<sup>r</sup> (integer *r* ), e.g., 3x3x3, 9x9x9 etc. The filter does not change the value of the voxel it is centered on if any of the filter voxels lies outside the domain of the data. |
| min3d | *n* x *n* x *n*  minimum rank filter for 3D waves. |
| point3d | *n* x *n* x *n*  point finding filter using normalized (*n*<sup>3</sup>-1)*center-outer for 3D waves. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/N = *n*</span> | Specifies the filter size. By default *n* =3. In most situations it will be useful to set *n*  to an odd number in order to preserve the symmetry in the filters. |
| <span class="table-cell-nowrap">/O</span> | Overwrites the source image with the output image. Used only with the hybridmedian filter, which does not automatically overwrite the source wave. |

### *Details* {#details}
You can operate on 3D waves using the 3D filters listed above. These filters are extensions of the 2D filters available under MatrixFilter. The avg3d, gauss3d, and point3d filters are implemented by a 3D convolution that uses an averaging compensation at the edges.

This operation does not support complex waves.

### *See Also* {#see-also}
[MatrixFilter](/igorpro/commands/matrixfilter.md) for descriptions of the other available parameters and flags.

[MatrixConvolve](/igorpro/commands/matrixconvolve.md) for information about convolving your own 3D kernels.

[Image Processing](/igorpro/analysis/image-processing.md)

### *References* {#references}
Russ, J., *Image Processing Handbook*, CRC Press, 1998.