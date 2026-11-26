---
description: "The ImageSeedFill operation takes a seed pixel and fills a contiguous region with the target value, storing the result in the wave M_SeedFill."
slug: /commands/imageseedfill
---

<div className="command-signature">

## <strong>ImageSeedFill</strong>  [/O][/B=<em>backgroundValue</em> ][/C][/K=<em>killCount</em> ] [/R=<em>roiWave</em> ] [<em>adaptive</em>=<em>factor</em>, <em>fillNumber</em>=<em>num</em>, <em>fuzzyCenter</em>=<em>fcVal</em>, <em>fuzzyProb</em>=<em>fpVal</em>, <em>fuzzyScale</em>=<em>fsVal</em>, <em>fuzzyWidth</em>=<em>fwVal</em>, <em>min</em>=<em>minval</em>, <em>max</em>=<em>maxval</em> ], <em>seedP</em>=<em>row</em>, <em>seedQ</em>=<em>col</em>, <em>seedR</em>=<em>layer</em>, <em>seedX</em>=<em>xLoc</em>, <em>seedY</em>=<em>yLoc</em>, <em>seedZ</em>=<em>zLoc</em>, <em>target</em>=<em>setValue</em>, <em>srcWave</em>=<em>srcImage</em> {#imageseedfill}

</div>

The ImageSeedFill operation takes a seed pixel and fills a contiguous region with the target value, storing the result in the wave M_SeedFill. The filled region is defined by all contiguous pixels that include the seed pixel and whose pixel values lie between the specified minimum and maximum values (inclusive). ImageSeedFill works on 2D and 3D waves.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">adaptive = *factor*</span> | Invokes the adaptive algorithm where a pixel or voxel is accepted if its value is between the specified minimum and maximum or its value satisfies: |
|  | $$ \displaystyle \|v a l-a v g\|< { factor } *  { stdv } . $$ |
|  | Here *val* is the value of the pixel or voxel in question, *avg* is the average value of the pixels or voxels in the neighborhood and *stdv* is the standard deviation of these values. By choosing a small *factor* you can constrain the acceptable values to be very close to the neighborhood average. A large *factor* allows for more deviation assuming that the stdv is greater than zero. |
|  | This requirement means that a connected pixel has to be between the specified minimum and maximum value and satisfy the adaptive relationship.  In most situations it is best to set wide limits on the minimum and maximum values and allow the adaptive parameter to control the local connectivity. |
| <span class="table-cell-nowrap">fillNumber = *num*</span> | Specifies the number, in the range 1 to 26, of voxels in each 3x3x3 cube that belong to the set. If fillNumber is exceeded, the operation fills the remaining members of the cube. If you do not specify this keyword, the operation does not fill the cube. Used only in the fuzzy algorithm. |
| <span class="table-cell-nowrap">fuzzyCenter = *fcVal*</span> | Specifies the center value for the fuzzy probability with the fuzzy algorithm (see details below). The default value is 0.25. Its standard range is 0 to 0.5, although interesting results might be obtained outside this range. |
| <span class="table-cell-nowrap">fuzzyProb = *fpVal*</span> | Specifies a probability threshold that must be met by a voxel to be accepted to the seeded set. The value must be in the range 0 to 1. The default value is 0.75. |
| <span class="table-cell-nowrap">fuzzyScale = *fsVal*</span> | Determines if a voxel is to be considered in a second stage using fuzzy probability. *fsVal* must be nonzero in order to invoke the fuzzy algorithm. The scale is used in comparing the value of the voxel to the value of the seed voxel. The scale should normally be in the range 0.5 to 2.0. |
| <span class="table-cell-nowrap">fuzzyWidth = *fwVal*</span> | Defines the width of the fuzzy probability distribution with the fuzzy algorithm (see details below). In most situations you should not need to specify this parameter. The default value is 1. |
| <span class="table-cell-nowrap">min = *minval*</span> | Specifies the minimum value that is accepted in the seeded set. Not needed when using fuzzy algorithm. |
| <span class="table-cell-nowrap">max = *maxval*</span> | Specifies the maximum value that is accepted to the seeded set. Not needed when using the fuzzy algorithm. |
| <span class="table-cell-nowrap">seedP = *row*</span> | Specifies the integer row location of the seed pixel or voxel. Use this keyword to get around roundoff issues when srcWave has wave scaling.  You must provide either seedP or seedX with all algorithms. It is sometimes convenient to use this keyword with cursors e.g., seedP=pcsr(a). |
| <span class="table-cell-nowrap">seedQ = *col*</span> | Specifies the integer column location of the seed pixel or voxel. Use this keyword to avoid roundoff difficulties when srcWave has wave scaling.  You must provide either seedQ or seedY with all algorithms. |
| <span class="table-cell-nowrap">seedR = *layer*</span> | Specifies the integer layer position of the seed voxel. When srcWave is a 3D wave you must use either seedR or seedZ. |
| <span class="table-cell-nowrap">SeedX = *xLoc*</span> | Specifies the pixel or voxel index. If srcWave has wave scaling, SeedX must be expressed in terms of the scaled coordinate. This keyword or seedP is required with all algorithms. |
| <span class="table-cell-nowrap">SeedY = *yLoc*</span> | Specifies the pixel or voxel index. If srcWave has wave scaling, SeedY must be expressed in terms of the scaled coordinate. This keyword or seedQ is required with all algorithms. |
| <span class="table-cell-nowrap">SeedZ = *zLoc*</span> | Specifies the voxel index. If srcWave has wave scaling, SeedZ must be expressed in terms of the scaled coordinate. You must use this keyword or seedR whenever srcWave is 3D. |
| <span class="table-cell-nowrap">srcWave = *srcImage*</span> | Specifies the source image wave. |
| <span class="table-cell-nowrap">target = *val*</span> | Sets the value assigned to pixels or voxels that belonging to the seeded set. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *bValue*</span> | Specifies the value assigned to pixels or voxels that do not belong to the filled area. If you omit /B, these pixels or voxels are assigned the corresponding values of the wave specified by the srcWave keyword. |
| <span class="table-cell-nowrap">/C</span> | Uses 8-connectivity where a pixel can be connected to any one of its neighbors and with which it shares as little as a single boundary point.  The default setting is 4-connectivity where pixels can be connected if they are neighbors along a row or a column. This has no effect in 3D, where 26-connectivity is the only option. |
| <span class="table-cell-nowrap">/DEST = *destW*</span> | Use this flag to designate the output wave containing the modified image. By default, ImageSeedFill saves the output in the wave M_SeedFill in the current data folder. |
|  | The /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destW* as a free wave. |
|  | /FREE is allowed only in functions and only if the destination wave name is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/K = *killCount*</span> | Terminates the fill operation after killCount elements have been accepted. |
| <span class="table-cell-nowrap">/O</span> | Overwrite the source wave with the output (2D only). |
| <span class="table-cell-nowrap">/R = *roiWave*</span> | Specifies a region of interest (ROI). The ROI is defined by a wave of type unsigned byte (/b/u), that has the same number of rows and columns and layers as the image wave. The ROI itself is defined by the entries/pixels whose value are 0. Pixels outside the ROI can take any nonzero value. The ROI does not have to be contiguous. See ImageGenerateROIMask for more information on creating ROI waves. |

### *Details* {#details}
In two dimensions, the operation takes a seed pixel, optional minimum and maximum pixel values and optional adaptive coefficient. It then fills a contiguous region (in a copy of the source image) with the target value. There are two algorithms for 2D seed fill. In direct seed fill (only min, max, seedX and seedY are specified) the filled region is defined by all contiguous pixels that include the seed pixel and whose pixel values lie between the specified minimum and maximum values (inclusive). In adaptive fill, there is an additional condition for the pixel or voxel to be selected, which requires that the pixel value must be within the standard deviation of the average in the 3x3 (2D) or 3x3x3 (3D) nearest neighbors. If you do not specify the minimum and maximum values then the operation selects only values identical to that of the seed pixel.

In 3D, there are three available algorithms. The direct seed fill algorithm uses the limits specified by the user to fill the seeded domain. In adaptive seed fill the algorithm requires the limits as well as the adaptive parameter. It fills the domain by accepting only voxels that lie within the adaptive factor times the standard deviation of the immediate voxel neighborhood. To invoke the third algorithm you must set fuzzyScale to a nonzero value. The fuzzy seed fill uses two steps to determine if a voxel should be in the filled domain. In the first step the value of the voxel is compared to the seed value using the fuzzy scale. If accepted, it passes to the second stage where a fuzzy probability is calculated based on the number of voxels in the 3x3x3 cell which passed the first step together with the user-specified probability center (fuzzyCenter) and width (fuzzyWidth). If the result is greater than fuzzyProb, the voxel is set to belong to the filled domain.

If the /O flag is not specified, the result is stored in the wave M_SeedFill.

If you specify a background value with the /B flag, the resulting image consists of the background value and the target value in the area corresponding to the seed fill. Although the wave is now bi-level, it retains the same number type as the source image.

ImageSeedFill returns a "bad seed pixel specification" if the seed pixel location derived from the various keywords above satisfies one or more of the following conditions:


1.  The computed integer pixel/voxel is outside the image.


2.  The value stored in the computed integer pixel/voxel location does not satisfy the min/max or fuzzy conditions. This is the most common condition when srcWave has wave scaling. To avoid this difficulty you should use the keywords seedP, seedQ, and seedR.

### *Examples* {#examples}
Using Cursor A position and value to supply parameter inputs for a 2D seedFill:


```igor
ImageSeedFill seedP=pcsr(a),seedQ=qcsr(a),min=zcsr(a),max=zcsr(a),target=0,srcwave=image0
```

Using the fuzzy algorithm for a 3D wave (command wrapped over two lines):


```igor
ImageSeedFill seedX=232,seedY=175,seedZ=42,target=1,fillNumber=10,fuzzyCenter=.25, fuzzyWidth=1,fuzzyScale=1,fuzzyProb=0.4,srcWave=ddd
```

### *See Also* {#see-also}
To display the result of the operation for 3D waves it is useful to convert the 3D wave M_SeedFill into an array of quads. See [ImageTransform](/igorpro/commands/imagetransform.md) vol2surf.

[Image Processing](/igorpro/analysis/image-processing.md)