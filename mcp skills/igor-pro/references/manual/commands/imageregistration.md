---
description: "The ImageRegistration operation adjusts the test image wave, testWave, to match the reference image wave, refWave, possibly subject to auxiliary mask waves."
slug: /commands/imageregistration
---

<div className="command-signature">

## <strong>ImageRegistration</strong>  [<em>flags</em>] [<em>testMask</em>=<em>testMaskWave</em> ] [<em>refMask</em>=<em>refMaskWave</em> ] <em>testWave</em>=<em>imageWave1</em>, <em>refWave</em>=<em>imageWave2</em> {#imageregistration}

</div>

The ImageRegistration operation adjusts the test image wave, testWave, to match the reference image wave, refWave, possibly subject to auxiliary mask waves. The registration may involve offset, rotation, scaling or skewing.

Image data may be in two or three dimensions.

ImageRegistration is designed to find accurate registration for relatively small variation on the order of a few degrees of rotation and a few pixels offset between the reference and test images.

All the input waves are expected to be single precision float (SP) so you may have to redimension your images before using ImageRegistration.

ImageRegistration does not tolerate NaNs or INFs; use the masks if you need to exclude pixels from the registration process.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">refMask = *refMaskWave*</span> |  |
|  | Specifies an optional ROI wave used to mask refWave. Omit refMask to use all of the refWave. |
|  | The wave must have the same dimensions as refWave. refMask is a single precision floating point wave with nonzero entries marking the "ON" state. Note that the operation modifies this wave and that you should not use the same wave for both the reference and the test masks. |
| <span class="table-cell-nowrap">refWave = *imageWave2*</span> | Specifies the name of the reference image wave used to adjust testWave. |
| <span class="table-cell-nowrap">testMask = *testMaskWave*</span> |  |
|  | Specifies an optional ROI wave used to mask testWave. Omit testMask to use all of the testWave. |
|  | The wave must have the same dimensions as refWave. testMask is a single precision floating point wave with nonzero entries marking the "ON" state. Note that the operation modifies this wave and that you should not use the same wave for both the reference and the test masks. |
| <span class="table-cell-nowrap">testWave = *imageWave1*</span> | Specifies the name of the image wave that will be adjusted to match refWave. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ASTP = *val*</span> | Sets the adaptation step for the Levenberg-Marquardt algorithm. Default value is 4. |
| <span class="table-cell-nowrap">/BVAL = *val*</span> | Enables clipping and sets the background values to which masked out voxels of the test data will be set. |
| <span class="table-cell-nowrap">/CONV = *val*</span> | Sets the convergence method. |
|  |<table class="nested-table"><tbody><tr><td>*val*&nbsp;=0:</td><td>Gravity, use if the difference between the images is only in translation. This option is frequently useful as a first step when the test and reference data are too far apart for accurate registration. The result of this registration is then passed to a subsequent ImageRegistration with /CONV=1.</td></tr><tr><td>*val*&nbsp;=1:</td><td>Marquardt.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/CSNR = *val*</span> | Determines if the operation calculates the signal to noise ratio (SNR). |
|  |<table class="nested-table"><tbody><tr><td>*val*&nbsp;=0:</td><td>The SNR is not calculated.</td></tr><tr><td>*val*&nbsp;=1:</td><td>The SNR is calculated (default).</td></tr></tbody></table>
|  | Skipping the SNR calculation saves time and may be particularly useful when performing the registration on a stack of images. |
| <span class="table-cell-nowrap">/DSTM = *destM*</span> | Use this flag to designate the destination of the output mask wave. By default, ImageRegistration saves the output in the wave M_RegMaskOut in the current data folder. |
|  | The /DSTM flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTO = *destO*</span> | Use this flag to designate the destination of the registered image wave. By default, ImageRegistration saves the output in the wave M_RegOut in the current data folder. |
|  | The /DSTO flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTP = *destP*</span> | Use this flag to designate the destination of the registration parameters wave. By default, ImageRegistration saves the output in the wave W_RegParams or M_RegParams in the current data folder. |
|  | The /DSTP flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FLVL = *val*</span> | Specifies the finest level on which the optimization is to be performed. |
|  | If this is set to the same value as /PRDL, then only the coarsest registration calculation is done. |
|  | If /FLVL=1 (default), then the full multiresolution pyramid is processed. You can use this flag to terminate the computation at a specified coarseness level greater than 1. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all the specified destination waves as free waves. This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions and only if the destination wave names are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/GRYM</span> | Optimizes the gray level scaling factor. |
|  | It is sometimes dangerous to let the program adjust for gray levels because in some situations it might result in a null image. |
| <span class="table-cell-nowrap">/GRYR</span> | Renders output using the gray scaling parameter. This is more meaningful if the operation computes the optimal gray scaling (see /GRYM). |
| <span class="table-cell-nowrap">/GWDT = {*sx*,*sy*,*sz* }</span> |  |
|  | Sets the three fields to the half-width of a Gaussian window that is used to smooth the data when computing the default masks. Defaults are {1,1,1}. See /REFM and /TSTM for more details. |
| <span class="table-cell-nowrap">/INTR = *val*</span> | Sets the interpolation method. |
|  |<table class="nested-table"><tbody><tr><td>*val*&nbsp;=0:</td><td>Nearest neighbor. Used when registering the center of gravity of the test and reference images.</td></tr><tr><td>*val*&nbsp;=1:</td><td>Trilinear.</td></tr><tr><td>*val*&nbsp;=2:</td><td>Tricubic (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/ISOS</span> | Optimizes the isometric scaling. This option is inappropriate if voxels are not cubic. |
| <span class="table-cell-nowrap">/ISR</span> | Computes the multiresolution pyramid with isotropic size reduction. |
|  | If the flag is not specified, the size reduction is in the XY plane only. |
| <span class="table-cell-nowrap">/ISSQ</span> | Ignore stack sequence. |
|  | When registring a stack, this flag tells Igor to not initialize the registration solution for a layer using the data from the previous layer. Instead, each frame is initialized indpendently. This flag is required if you want the operation to perform with automatic multithreading, where the execution sequence is not predictable and so the registration of every frame is initialized relative to the reference frame. |
|  | New in Igor Pro 9. |
| <span class="table-cell-nowrap">/MING = *val*</span> | Sets the minimum gain at which the computations will stop. Default value is zero, but you can use a slightly larger value to stop the iterations earlier. |
| <span class="table-cell-nowrap">/MSKC = *val*</span> | Sets mask combination value. During computation the masks for the test data and the mask for the reference data are also transformed. This flag determines how the two masks are to be combined. The registration criteria are computed for the combination of the two masks. |
|  |<table class="nested-table"><tbody><tr><td>*val*&nbsp;=0:</td><td>or</td></tr><tr><td>*val*&nbsp;=1:</td><td>nor</td></tr><tr><td>*val*&nbsp;=2:</td><td>and (default)</td></tr><tr><td>*val*&nbsp;=3:</td><td>nand</td></tr><tr><td>*val*&nbsp;=4:</td><td>xor</td></tr><tr><td>*val*&nbsp;=5:</td><td>nxor</td></tr></tbody></table>
| <span class="table-cell-nowrap">/PRDL = *depth*</span> | Specifies the depth of the multiresolution pyramid. The finest level is *depth* =1. Each level of the pyramid decreases the resolution by a factor of 2. By default, the pyramid *depth* =4, which corresponds to a resolution reduction by a factor of 2^(*depth* -1)=8. |
|  | The algorithm starts by computing the first registration on large scale features in the image (deepest level of the pyramid). It then makes small corrections to the registration at each consecutive pyramid level. |
|  | For best results, the coarsest representation the data should be between 30 and 60 pixels on a side. For example, for an image that is *H* by *V* pixels, you should choose the depth such that |
|  | H/2^(*depth* -1) ≈ 30. |
| <span class="table-cell-nowrap">/PSTK</span> | When performing registration of a stack of images, use this flag to apply the registration parameters of the previous layer as the initial guess for the registration of each layer after the first in the 3D stack. |
| <span class="table-cell-nowrap">/Q</span> | Quiet mode; no messages printed in the history area. |
| <span class="table-cell-nowrap">/REFM = *val*</span> | Sets the reference mask. |
|  |<table class="nested-table"><tbody><tr><td>*val*&nbsp;=0:</td><td>Leave blank and then every pixel is taken into account.</td></tr><tr><td>*val*&nbsp;=1:</td><td>This value will be set if a valid reference mask is provided.</td></tr><tr><td>*val*&nbsp;=2:</td><td>Reference mask is computed (default).</td></tr></tbody></table>
|  | When computing the reference mask it is assumed that brighter features are more important. This is done by using a low pass filter on the data (using the parameters in /GWDT) which is then converted into a binary mask. Note that you do not need to specify /REFM=1 if you are providing a reference mask wave. See also /TSTM. |
| <span class="table-cell-nowrap">/ROT = {*rotX*,*rotY*,*rotZ* }</span> |  |
|  | Determines if optimization will take into account rotation about the X, Y, or Z axes. A value of one allows optimization and zero prevents optimization from affecting the corresponding rotation parameter. Defaults are {0,0,1}, which are the appropriate values for rotating images. |
| <span class="table-cell-nowrap">/SKEW = {*skewX*,*skewY*,*skewZ* }</span> |  |
|  | Determines if optimization will take into account skewness about the X, Y, or Z axes. A value of one allows optimization and zero prevents optimization from affecting the corresponding skewness parameter. Defaults are {0,0,0}. Note that skewing and rotation or isometric scaling are mutually exclusive operations. |
| <span class="table-cell-nowrap">/STCK</span> | Use /STCK to perform the registration between a 2D reference image and each of the layers in a 3D image. The number of rows and columns of the refWave must match exactly the number of rows and columns in testWave. The transformation parameters are saved in the wave M_RegParams where each column contains the parameters for the corresponding layer in testWave. |
| <span class="table-cell-nowrap">/STRT = *val*</span> | Sets the first value of the adaptation parameter in the Levenberg-Marquardt algorithm. |
|  | The default value is 1. |
| <span class="table-cell-nowrap">/TRNS = {*transX*,*transY*,*transZ* }</span> |  |
|  | Determines if optimization will take into account translation about the X, Y, or Z axes. A value of one allows optimization and zero prevents optimization from affecting the corresponding translation parameter. Defaults are {1,1,0}, which are appropriate for finding the X and Y translations of an image. |
| <span class="table-cell-nowrap">/TSTM = *val*</span> | Sets the test mask. |
|  |<table class="nested-table"><tbody><tr><td>*val*&nbsp;=0:</td><td>Leave blank and then every pixel is taken into account.</td></tr><tr><td>*val*&nbsp;=1:</td><td>This value will be set if a valid reference mask is provided.</td></tr><tr><td>*val*&nbsp;=2:</td><td>The test mask is computed (default).</td></tr></tbody></table>
|  | The test image mask is computed in the same way as the reference image mask (see /REFM) using the same set of smoothing parameters. Note that you do not need to specify /TSTM=1 if you are providing a test mask wave. |
| <span class="table-cell-nowrap">/USER = *pWave*</span> | Provides a user transformation that will be applied to the input *testWave* in order to create the trasnsformed image. *pWave* must be a double precision wave which contains the same number of rows as W_RegParams. |
|  | Note: If you use a previously created W_RegParams make sure to change its name as it is overwritten by the operation. |
|  | If *pWave* has only one column and *testWave* contains multiple layers, then the same transformation applies to all layers. If *pWave* contains more than one column, then each layer of *testWave* is processed with corresponding column. If there are more layers than columns the first column is used in place of the missing columns. |
| <span class="table-cell-nowrap">/ZMAN</span> | Modifies the test and reference data by subtracting their mean values prior to optimization. |

### *Details* {#details}
ImageRegistration will register images that have sufficiently similar features. It will not work if key features are too different. For example, ImageRegistration can handle two images that are rotated relative to each other by a few degrees, but cannot register images if the relative rotation is as large as 45 degrees. The algorithm is capable of subpixel resolution but it does not handle large variations between the test image and the reference image. If the centers of the two images are too far from each other, you should first try ImageRegistration using /CON=0 to remove the translation offset before proceeding with a finer registration of details.

The algorithm is based on an iterative processing that proceeds from coarse to fine detail. Optimization uses a modified Levenberg-Marquardt algorithm and produces an affine transformation for the relative rotation and translation as well as for isometric scaling and contrast adjustment. The algorithm is most effective with square images where the center of rotation is not far from the center of the image.

When using gravity for convergence, skew parameters can't be evaluated (only translation is supported). Skew and isoscaling are mutually exclusive options. Mask waves are defined to have zero entries for pixels outside the region of interest and nonzero entries otherwise. If a mask is not provided, every pixel is used.

ImageRegistration creates the waves M_RegOut and M_RegMaskOut, which are both single precision waves. In addition, the operation creates the wave W_RegParams which stores 20 double precision registration parameters (see below). M_RegOut contains the transformed (registered) test image and M_RegMaskOut contains the transformed mask (which is not affected by mask combination). ImageRegistration ignores wave scaling; images are compared and registered based on pixel values only.

The results printed in the history include:


|  |  |
| --- | --- |
| dx, dy, dz | Translation offsets measured in pixels. |
| a*ij* | Elements in the skewing transformation matrix. |
| phi | Rotation angle in degrees about the X-axis. Zero for 2D waves. |
| tht | Rotation angle in degrees about the Y-axis. Zero for 2D waves. |
| psi | Rotation angle in degrees about the Z-axis. |
| det | Absolute value of determinant of the skewing matrix (a*ij*). |
| err | Mean square error defined as |
|  | $$ \displaystyle \frac{1}{N} \sum\left(x_{i}-y_{i}\right)^{2}, $$ |
|  | where *xi* is the original pixel value, *yi* the computed value, and *N* is the number of pixels. |
| snr | Signal to noise ratio in dB. It is given by: |
|  | $$ \displaystyle 10 \log \left(\frac{\sum x_{i}^{2}}{\sum\left(x_{i}-y_{i}\right)^{2}}\right) . $$ |

These parameters are stored in the wave W_RegParams (or M_RegParams in the case of registering a stack). Angles are in radians. Dimension labels are used to describe the contents of each row of the output wave. Each column of the wave consists of the following rows (also indicated by dimension labels):

| Point | Content | Point | Content |
| --- | --- | --- | --- |
| 0 | dx | 11 | a33 |
| 1 | dy | 12 | gamma |
| 2 | dz | 13 | phi |
| 3 | a11 | 14 | theta |
| 4 | a12 | 15 | psi |
| 5 | a13 | 16 | lambda |
| 6 | a21 | 17 | origin_x |
| 7 | a22 | 18 | origin_y |
| 8 | a23 | 19 | origin_z |
| 9 | a31 | 20 | MSE |
| 10 | a32 | 21 | SNR |

You can view the output waves with dimension labels by executing:

```igor
Edit W_RegParams.ld
```

### *References* {#references}
This operation is based on an algorithm described by:

Thévenaz, P., and M. Unser, "A Pyramid Approach to Subpixel Registration Based on Intensity," *IEEE Transactions on Image Processing*, *7*, 27-41, 1998.

### *See Also* {#see-also}
The Warp parameter of the [ImageInterpolate](/igorpro/commands/imageinterpolate.md) operation.

### *Demos* {#demos}
[Open Image Registration Demo](#igor-pxp/Examples/Imaging/Image__Registration__Demo.pxp)