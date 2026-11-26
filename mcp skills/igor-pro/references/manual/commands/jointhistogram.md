---
description: "The JointHistogram computes 2D, 3D and 4D joint histograms of data provided in the input waves."
slug: /commands/jointhistogram
---

<div className="command-signature">

## <strong>JointHistogram</strong>  [<em>flags</em>] <em>wave1</em>, <em>wave2</em> [, <em>wave3</em>, <em>wave4</em>] {#jointhistogram}

</div>

The JointHistogram computes 2D, 3D and 4D joint histograms of data provided in the input waves. The input waves must be 1D real numeric waves having the same number of points. The result of the operation is stored in the multidimensional wave *M_JointHistogram* in the current data folder or in the wave specified via the /DEST flag.

This operation was added in Igor Pro 7.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/BINS = {*nx,* *ny,* *nz,* *nt* }</span> |  |
|  | Specifies the number of bins along each axis. Set the number of bins for unused axes to zero. If the number of bins is non-zero, then the flags /XBMT, /YBMT, /ZBMT, and /TBMT are overridden. |
| <span class="table-cell-nowrap">/C</span> | Sets the output wave scaling so that the values in each axis are centered in the bins. By default, wave scaling of the output wave is set with values at the left bin edges. This flag has no effect on axes where bins are specified by using /XBWV, /YBWV, /ZBWV or /TBWV. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave created by the operation. If you omit /DEST then the output wave is *M_JointHistogram* in the current data folder. |
|  | It is an error to specify a destination which is the same as one of the input waves. |
|  | When used in a user-defined function, the JointHistogram operation by default creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/E</span> | Excludes outliers. This flag is relevant only if there are one or more bin waves specified by using /XBWV, /YBWV, /ZBWV or /TBWV. By default values that might fall below the first bin or above the last bin are folded into the first and last bin respectively. These values (outliers) are excluded from the joint histogram when you use /E. See /P below for the way outliers affect the probability calculation. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave*, as specified by /DEST, is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/P = *mode*</span> | Normalizes the histogram to a probability density. |
|  | Use *mode*=0 to count all points, including possible outliers but excluding non-finite values, in the probability calculation. This is the default setting. |
|  | Use *mode*=1 if you want to completely exclude outliers from the normalization. |
|  | When outliers are excluded the output wave sums to 1. When they are included the sum of the output wave is smaller by the ratio of the number of outliers to the total number of points in the histogram. |
| <span class="table-cell-nowrap">/W = *weightWave*</span> |  |
|  | Creates a weighted histogram. Instead of adding a single count to the appropriate bin, the corresponding value from *weightWave* is added to the bin. *weightWave* may be any real number type. |
| <span class="table-cell-nowrap">/XBMT = *method*</span> |  |
| <span class="table-cell-nowrap">/YBMT = *method*</span> |  |
| <span class="table-cell-nowrap">/ZBMT = *method*</span> |  |
| <span class="table-cell-nowrap">/TBMT = *method*</span> | These flags specify which method is used to set the bins. By default *method*=0. These flags are overridden by /BINS if a non-zero value is specified for a given axis and by /XBWV, /YBWV, /ZBWV and /TBWV. |
|  | See ***JointHistogram Binning Methods*** below for details. |
| <span class="table-cell-nowrap">/XBWV = *xBinWave*</span> |  |
| <span class="table-cell-nowrap">/YBWV = *yBinWave*</span> |  |
| <span class="table-cell-nowrap">/ZBWV = *zBinWave*</span> |  |
| <span class="table-cell-nowrap">/TBWV = *tBinWave*</span> |  |
|  | Specifies the exact bins for a corresponding axis. |
|  | The wave must be 1D real numeric wave with monotonically increasing finite values and must contain a minimum of 3 data points. |
|  | The values in a bin wave specify the edges of the bins. A bin wave with N points defines n-1 bins. In the case of a 3-point bin wave, the first point corresponds to the minimum value of the first bin, the second point is the boundary between the two bins and the last point is the upper limit of the second bin. |
|  | These flags override the corresponding bin specification set via /BINS, /XBMT, /YBMT, /ZBMT and /TBMT. |
| <span class="table-cell-nowrap">/Z [ = zval]</span> | Suppresses error reporting. |
|  | /Z is equivalent to /Z=1 and /Z=0 is equivalent to not using the /Z flag at all. |

### *Details* {#details}
The input waves must be 1D real numeric waves. If one or more waves contain a non-finite value (a NaN or INF) the corresponding row of all waves are not counted in the joint histogram.

The optional waves that define user-specified bins must be real numeric waves and contain a monotonically increasing values. Using non-finite values in user-specified bin waves may lead to unpredictable results.

### *JointHistogram Binning Methods* {#jointhistogram-binning-methods}
The /XBMT, /YBMT, /ZBMT and /TBMT flags set the binning method for the X, Y, Z and T dimensions respectively.

These flags are overridden by /BINS if a non-zero value is specified for a given axis and by /XBWV, /YBWV, /ZBWV and /TBWV.

The *method* parameter is defined as follows:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">*method* = 0:</span> | 128 equally spaced bins between the minimum and maximum of the input data. This is the default setting. |
| <span class="table-cell-nowrap">*method* = 1:</span> | The number of bins is computed using Sturges' method where |
|  | *numBins*=1+log2(N). |
|  | N is the number of data points in each wave. The bins are distributed so that they include the minimum and maximum values. |
| <span class="table-cell-nowrap">*method* = 2:</span> | The number of bins is computed using Scott's method where the optimal bin width is given by |
|  | *binWidth*=3.49\*σ\*N<sup>-1/3</sup>. |
|  | σ is the standard deviation of the distribution and N is the number of points. The bins are distributed so that they include the minimum and maximum values. |
| <span class="table-cell-nowrap">*method* = 3:</span> | Freedman-Diaconis method where |
|  | *binWidth*=2\**IQR*\*N<sup>-1/3</sup>, |
|  | where IQR is the interquartile distance (see [StatsQuantiles](/igorpro/commands/statsquantiles.md)) and the bins are evenly distributed between the minimum and maximum values. |

Bin selection methods are described at: [http://en.wikipedia.org/wiki/Histogram](http://en.wikipedia.org/wiki/Histogram)

### *Examples: 2D Joint Histogram* {#examples-2d-joint-histogram}

```igor
Make/O/N=(1000) xwave=gnoise(10), ywave=gnoise(5)
JointHistogram/BINS={20,30} xwave,ywave
NewImage M_JointHistogram
```

### *Examples: 2D Joint Histogram using one bins wave* {#examples-2d-joint-histogram-using-one-bins-wave}

```igor
Make/O/N=(1000) xwave=gnoise(10), ywave=gnoise(5)
Make/O/N=3 xBinsWave={-8,0,14}
JointHistogram/BINS={0,30}/XBWV=xBinsWave/E xwave,ywave
Display; AppendImage/T M_JointHistogram vs {xBinsWave,*}
```

### *Examples: 3D Joint Histogram* {#examples-3d-joint-histogram}

```igor
Make/O/N=(1000) xwave=gnoise(10), ywave=gnoise(5), zwave=enoise(4)
JointHistogram/BINS={15,15,20,0} xwave,ywave,zwave
NewImage M_JointHistogram
ModifyImage M_JointHistogram plane=10
```

### *See Also* {#see-also}
[Histogram](/igorpro/commands/histogram.md), [ImageHistogram](/igorpro/commands/imagehistogram.md)