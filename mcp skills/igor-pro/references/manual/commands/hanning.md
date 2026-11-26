---
description: "The WindowFunction operation has replaced the Hanning operation. You can use Hanning in preparation for performing an FFT on a wave if the wave is not an…"
slug: /commands/hanning
---

<div className="command-signature">

## <strong>Hanning</strong>  <em>waveName</em> [, <em>waveName</em> ]... {#hanning}

</div>

:::note
The WindowFunction operation has replaced the Hanning operation.
:::

You can use Hanning in preparation for performing an FFT on a wave if the wave is not an integral number of cycles long.

The Hanning operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *See Also* {#see-also}
The [WindowFunction](/igorpro/commands/windowfunction.md) operation implements the Hanning window as well as other forms such as Hamming, Parzen, and Bartlet (triangle).

The [ImageWindow](/igorpro/commands/imagewindow.md) operation for windowing of images.

[DPSS](/igorpro/commands/dpss.md)