---
description: "The Histogram operation generates a histogram of the data in srcWaveName and puts the result in destWaveName or in W_Histogram or in the wave specified by…"
slug: /commands/histogram
---

<div className="command-signature">

## <strong>Histogram</strong>  [ <em>flags</em> ] <em>srcWaveName</em>, <em>destWaveName</em> {#histogram}

</div>

The Histogram operation generates a histogram of the data in *srcWaveName* and puts the result in *destWaveName* or in W_Histogram or in the wave specified by /DEST.

### *Parameters* {#parameters}
*srcWaveName* specifies the wave containing the data to be histogrammed.

For historical reasons the meaning and use of *destWaveName* depend on the binning mode as specified by /B. See **Histogram Destination Wave** below for details.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Accumulates the histogram result with the existing values in the destination wave instead of replacing the existing values with the result. Assumes /B=2 unless the /B flag is present. |
|  | <div><Admonition type="warning"><p>The result will be incorrect if you also use /P.</p></Admonition></div> |
| /B=*mode* |<table class="nested-table"><tbody><tr><td>*mode*=1:</td><td>Semi-automatic mode which sets the bin range based on the range of the Y values in *srcWaveName*. The number of bins is determined by the number of points currently in the destination wave.</td></tr><tr><td>*mode*=2:</td><td>Uses the bin range and number of bins determined by the X scaling and number of points in the destination wave.</td></tr><tr><td>*mode*=3</td><td>Uses Sturges&#39; method to determine optimal number of bins and redimensions the destination wave as necessary. According to this method</td></tr><tr><td></td><td>*numBins*=1+log2(N)</td></tr><tr><td></td><td>where N is the number of data points in *srcWaveName.* The bins will be distributed so that they include the minimum and maximum values.</td></tr><tr><td>*mode*=4</td><td>Uses a method due to D. Scott which determines the optimal bin width as</td></tr><tr><td></td><td>*binWidth*=3.49\*σ\*N<sup>-1/3</sup></td></tr><tr><td></td><td>where N is the number of data points in *srcWaveName* and σ is the standard deviation of the distribution. The bins will be distributed so that they include the minimum and maximum values.</td></tr><tr><td>*mode*=5</td><td>Uses the Freedman-Diaconis method where the optimal bin width is</td></tr><tr><td></td><td>*binWidth*=2\*IQR\*N<sup>-1/3</sup></td></tr><tr><td></td><td>where IQR is the interquartile distance (see [StatsQuantiles](/igorpro/commands/statsquantiles.md)) and the bins are evenly distributed between the minimum and maximum values.</td></tr><tr><td></td><td>Added in Igor Pro 7.00.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/B = {*binStart*, *binWidth*, *numBins*}</span> |  |
|  | Sets the histogram bins from these parameters rather than from *destWaveName*. Changes the X scaling and length of the destination wave. |
| <span class="table-cell-nowrap">/C</span> | Sets the X scaling so that X values are in the centers of the bins, which is required when you do a curve fit to the histogram output. Ordinarily, wave scaling of the output wave is set with X values at the left bin edges. |
| <span class="table-cell-nowrap">/CUM</span> | Requests a cumulative histogram in which each bin is the sum of bins to the left. The last bin will contain the total number of input data points, or, with /P, 1.0. |
|  | /CUM cannot be used with a weighted histogram (/W flag). |
|  | When used with /A, the destination wave must be the result of a histogram created with /CUM. |
|  | Note that if you use a binning mode (/B flag) that sets a bin range that does not include the entire range of the input data, then the output will not count all of input points and the last bin will not contain the total number of input points. Input points whose values fall below the left edge of the first bin or above the right edge of the last bin will not be counted. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> | Saves the histogram output in a wave specified by *destWave*. The destination wave is created or overwritten if it already exists. |
|  | Creates a wave reference for the destination wave in a user function. See Automatic Creation of Wave References for details. |
|  | See **Histogram Destination Wave** below for further discussion. |
|  | The /DEST flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/DP</span> | Causes Histogram to create the destination wave as double-precision floating point instead of single-precision floating point. The /DP flag was added in Igor Pro 8.00. |
|  | Single-precision precisely represents integers up to 1,677,721 only. Double-precision precisely represents integers up to about 9 trillion. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* (specified by /DEST) as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/N</span> | Creates a wave named W_SqrtN containing the square root of the number of counts in each bin. This is an appropriate wave to use as a weighting wave when doing a curve fit to the histogram results. /N cannot be used with a weighted histogram (/W flag). |
| <span class="table-cell-nowrap">/NLIN = *binsWave*</span> | Computes a non-linear histogram using the bins specified in the wave *binsWave* . This option is not compatible with the flags /A, /B, /C, /CUM, /N, /P, /W. |
|  | The bins must be contiguous and non-overlapping so that *binsWave*  contains monotonically increasing values with no NaNs and INFs. For example, if you want the 3 bins [1,10),[10,100),[100,1000), execute: |
|  | <code class="igor">Make/O/N=4 bins={1,10,100,1000}</code> |
|  | The upper end of each bin is open. |
|  | The /NLIN flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/P</span> | Normalizes the histogram as a probability distribution function, and shifts wave scaling so that data correspond to the bin centers. |
|  | When using the results with [Integrate](/igorpro/commands/integrate.md), you must use /METH=0 or /METH=2 to select rectangular integration methods. |
| <span class="table-cell-nowrap">/R = (*startX*,*endX* )</span> | Specifies the range of X values of *srcWaveName*  over which the histogram is to be computed. |
| <span class="table-cell-nowrap">/R = [*startP*,*endP* ]</span> | Specifies the range of points of *srcWaveName*  over which the histogram is to be computed. |
| <span class="table-cell-nowrap">/RMD = [*firstRow* , *lastRow* ][*firstColumn* , *lastColumn* ][*firstLayer* , *lastLayer* ][*firstChunk* , *lastChunk* ]</span> |  |
|  | Designates a contiguous range of data in the source wave to which the operation is to be applied. This flag was added in Igor Pro 7.00. |
|  | You can include all higher dimensions by leaving off the corresponding brackets. For example: |
|  | <code class="igor">/RMD=[firstRow,lastRow]</code> |
|  | includes all available columns, layers and chunks. |
|  | You can use empty brackets to include all of a given dimension. For example: |
|  | <code class="igor">/RMD=[][firstColumn,lastColumn]</code> |
|  | means "all rows from firstColumn to lastColumn". |
|  | You can use a * to specify the end of any dimension. For example: |
|  | <code class="igor">/RMD=[firstRow,\*]</code> |
|  | means "from firstRow through the last row". |
| <span class="table-cell-nowrap">/W = *weightWave*</span> | Creates a "weighted" histogram. In this case, instead of adding a single count to the appropriate bin, the corresponding value from weightWave is added to the bin. weightWave may be any number type, and it may be complex. If it is complex, then the destination wave will be complex. |
|  | /W cannot be used with a cumulative histogram (/CUM flag). |

### *Histogram Destination Wave* {#histogram-destination-wave}
For historical reasons there are multiple ways to specify the destination wave and the meaning and use of *destWaveName* depend on the binning mode as specified by /B. This section explains the details and then provides guidance and when to use which mode.

In binning modes 1 and 2 (/B=1 and /B=2, described above), the destination wave plays a role in determining the binning and *destWaveName* must be the name of an existing wave. If you omit /DEST then the output is written to *destWaveName*. If you provide /DEST then the output is written to the wave specified by /DEST.

In binning modes 3, 4 and 5 (/B=3, /B=4 and /B=5, described above), the destination wave plays no role in determining the binning. If you omit *destWaveName* and /DEST, Histogram stores its output in a wave named W_Histogram in the current data folder. If you omit /DEST and provide *destWaveName*, then *destWaveName* must name an existing wave to which the output is written. If you provide /DEST, you can omit *destWaveName*. If you provide both /DEST and *destWaveName*  then *destWaveName* must name an existing wave but the operation ignores it.

Here is the recommended usage:

If you want to use specific binning that you have determined, use /B={*binStart*, *binWidth*,*numBins*}, use /DEST to specify the destination wave, and omit *destWaveName*.

If you want Igor to determine the binning, use /B=3, /B=4 or /B=5, use /DEST to specify the destination wave, and omit *destWaveName*.

For backward compatibility with Igor Pro 6, use /B=1, /B=2, /B=3, /B=4 or /B={*binStart*, *binWidth*, *numBins* }, create a destination wave, use it as *destWaveName* and omit /DEST.

### *Details* {#details}
If you use /B={binStart, binWidth, numBins}, then the initial number of data points in the wave is immaterial since the Histogram operation changes the number of points.

Only one /B and only one /R flag is allowed.

If both /A and /B flags are missing, the bin range and number of bins is calculated as if /B=1 had been specified.

When accumulating multiple histograms in one output wave, typically you will want to use /B={*binStart*, *binWidth*, *numBins*} for the first histogram, and /A for successive histograms.

The Histogram operation works on a single precision floating point destination wave. If necessary, Histogram redimensions the destination wave to be single precision floating point. However, Histogram/A requires that the destination wave already be single precision floating point.

For a weighted histogram, the destination wave will be double-precision.

If you specify the range as /R=(*start*) then the end of the range is taken as the end of *srcWaveName*.

In an ordinary histogram, input data is examined one data point at a time. The operation determines which bin a data value falls into and a single count is added to that bin. A weighted histogram works similarly, except that it adds to the bin a value from another wave in which each row corresponds to the same row in the input wave.

<img src="Images/Histogram/Histogram_0.png" width="100%"/>

The Histogram operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

In fact, the Histogram operation can be usefully applied to multidimensional waves, such as those that represent images. The /R flag will not work as expected, however.

### *Examples* {#examples}

```igor
// Create histogram of two sets of data.
Make/N=1000 data1=gnoise(1), data2=gnoise(1)
Make/N=1 histResult

// Sets bins, does histogram.
Histogram/B={-5,1,10} data1, histResult
Display histResult; ModifyGraph mode=5

// Accumulates into existing bins.
Histogram/A data2, histResult
```

### *See Also* {#see-also}
[Histograms](/igorpro/analysis/analysis.md#histograms), [ImageHistogram](/igorpro/commands/imagehistogram.md), [JointHistogram](/igorpro/commands/jointhistogram.md), [TextHistogram](/igorpro/commands/texthistogram.md)

### *References* {#references}
Sturges, H.A., The choice of a class-interval, *J. Amer. Statist. Assoc*., *21*, 65-66, 1926.

Scott, D., On optimal and data-based histograms, *Biometrika*, *66*, 605-610, 1979.