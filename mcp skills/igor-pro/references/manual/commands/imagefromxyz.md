---
description: "ImageFromXYZ converts XYZ data to matrix form. You might use it, for example, to convert a \"sparse matrix\" to an actual matrix for easier display and…"
slug: /commands/imagefromxyz
---

<div className="command-signature">

## <strong>ImageFromXYZ</strong>  [/AS] <em>xyzWave</em> , <em>dataMatrix</em> , <em>countMatrix</em> {#imagefromxyz}

</div>
<div className="command-signature">

## <strong>ImageFromXYZ</strong>  [/AS] {<em>xWave</em>,<em>yWave</em>,<em>zWave</em> }, <em>dataMatrix</em> , <em>countMatrix</em> {#imagefromxyz}

</div>

ImageFromXYZ converts XYZ data to matrix form. You might use it, for example, to convert a "sparse matrix" to an actual matrix for easier display and processing.

You provide the input data in the XYZ triplet *xyzWave* or in 1D waves *xwave*, *ywave*, and *zwave*.

*dataMatrix* and *countMatrix* receive output data but you must create them prior to calling ImageFromXYZ.

For each XY location in the input data, ImageFromXYZ adds the corresponding Z value to an element of *dataMatrix*. The element is determined based on the input XY location and the X and Y scaling of *dataMatrix* .

For each XY location in the input data, ImageFromXYZ increments the corresponding element of *countMatrix*. This permits you to obtain an average Z value if multiple input values fall into a given element of *dataMatrix*.

### *Parameters* {#parameters}
*xyzWave* is a triplet wave containing the input XYZ data.

*xWave*, *yWave* and *zWave* are 1D input waves containing XYZ data.

You specify either *xyzWave* by itself or *xWave*, *yWave* and *zWave* in braces.

*dataMatrix* is a 2D wave to which the Z values are added. It must be either single-precision or double-precision floating point. The X and Y scaling of *dataMatrix* determines how input values are mapped to output matrix elements.

*countMatrix* is a 2D wave the elements of which store the number of Z values added to each corresponding element of *dataMatrix*. ImageFromXYZ sets it to 32-bit integer if it is not already so.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/AS</span> | If /AS (autoscale) is specified, ImageFromXYZ clears both *dataMatrix* and *countMatrix* and sets the X and Y scaling of *dataMatrix* based on the range of X and Y input values. |

### *Details* {#details}
For each point in the XYZ input data, ImageFromXYZ adds the Z value to the appropriate element of *dataMatrix* and increments the corresponding element of *countMatrix*. Normally you will clear *dataMatrix* and *countMatrix* before calling it.

You can combine multiple XYZ datasets in one matrix by calling ImageFromXYZ multiple times with different input data and the same *dataMatrix* and *countMatrix*. In this case you would clear *dataMatrix* and *countMatrix* before the first call to ImageFromXYZ only.

What you do with the output is up to you but one technique is to divide *dataMatrix* by *countMatrix* to get the average and then use [MatrixFilter](/igorpro/commands/matrixfilter.md) NanZapMedian to eliminate any NaN values that result from zero divided by zero.

### *Example* {#example}

```igor
Make /N=1000 /O wx=enoise(2), wy= enoise(2), wz= exp(-(wx^2+wy^2))
Make /O /N=(100,100) dataMat=0
SetScale x,-2,2,dataMat
SetScale y,-2,2,dataMat
Duplicate /O dataMat,countMat
ImageFromXYZ /AS {wx,wy,wz}, dataMat, countMat
// Execute these one at a time
NewImage dataMat
dataMat /= countMat                 // Replace cumulative z value with average
MatrixFilter NanZapMedian, dataMat  // Apply median filter, zapping NaNs
```

### *See Also* {#see-also}
[SetScale](/igorpro/commands/setscale.md), [Image X and Y Coordinates](/igorpro/graphing/image-plots.md#image-x-and-y-coordinates)