---
description: "The numpnts function returns the total number of data points in the named wave."
slug: /commands/numpnts
---

<div className="command-signature">

## <strong>numpnts</strong> (<em>waveName</em>) {#numpnts}

</div>

The numpnts function returns the total number of data points in the named wave. To find the number of elements in a dimension of a multidimensional wave, use the [DimSize](/igorpro/commands/dimsize.md) function.

Do not use numpnts to test if a wave reference is null as this causes a runtime error. Use [WaveExists](/igorpro/commands/waveexists.md).