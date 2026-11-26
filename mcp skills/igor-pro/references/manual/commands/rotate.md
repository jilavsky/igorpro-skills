---
description: "The Rotate operation rotates the Y values of waves in wavelist by rotPoints points."
slug: /commands/rotate
---

<div className="command-signature">

## <strong>Rotate</strong>  <em>rotPoints</em>, <em>waveName</em> [, <em>waveName</em> ]... {#rotate}

</div>

The Rotate operation rotates the Y values of waves in wavelist by *rotPoints* points.

### *Parameters* {#parameters}
If *rotPoints* is positive then values are rotated from the start of the wave toward the end and *rotPoints* values from the end of a wave wrap around to the start of the wave.

If *rotPoints* is negative then values are rotated from the end of the wave toward the start and *rotPoints* values from the start of a wave wrap around to the end of the wave.

### *Details* {#details}
The X scaling of the named waves is changed so that the X values for the Y values remains the same except for the points that wrap around.

The Rotate operation is not multidimensional aware. To rotate rows or columns of 2D waves, see the  rotateRows and rotateCols keywords for the [MatrixOp](/igorpro/commands/matrixop.md) and [ImageTransform](/igorpro/commands/imagetransform.md) operations.

For general information about multidimensional analysis, see [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md) and [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves).