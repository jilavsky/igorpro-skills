---
description: "The FindContour operation creates an XY pair of waves representing the locus of the solution to matrixWave=level."
slug: /commands/findcontour
---

<div className="command-signature">

## <strong>FindContour</strong>  [/DSTX=<em>destXWave</em> /DSTY=<em>dstYWave</em> ] <em>matrixWave</em>, <em>level</em> {#findcontour}

</div>

The FindContour operation creates an XY pair of waves representing the locus of the solution to *matrixWave*=*level*.

The FindContour operation was added in Igor Pro 7.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSTX = *destX*</span> | Saves the output X data in the specified destination wave. The destination wave is created or overwritten if it already exists. |
| <span class="table-cell-nowrap">/DSTY = *destY*</span> | Saves the output Y data in the specified destination wave. The destination wave is created or overwritten if it already exists. |

### *Details* {#details}
FindContour uses a contour-following algorithm to generate a pair of waves describing the locus of the solution to *matrixWave*=*level*.

If you omit /DSTX the output X data is written to W_XContour in the current data folder.

If you omit /DSTY the output Y data is written to W_YContour in the current data folder.

The output waves are written as double-precision floating point. They use NaNs to separate different contiguous solution points.

### *Example* {#example}

```igor
Make/N=(100,200) dataWave = 1e4*gauss(x,50,10,y,100,20)
FindContour dataWave,4		// Find solution to dataWave=4
NewImage dataWave
AppendToGraph/T W_YContour vs W_XContour
```

### *See Also* {#see-also}
[AppendMatrixContour](/igorpro/commands/appendmatrixcontour.md), [ContourZ](/igorpro/commands/contourz.md)