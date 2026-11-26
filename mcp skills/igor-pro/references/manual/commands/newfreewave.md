---
description: "The NewFreeWave function creates a free 1D wave of the given type and number of points and then returns its wave reference."
slug: /commands/newfreewave
---

<div className="command-signature">

## <strong>NewFreeWave</strong> (<em>type</em> , <em>npoints</em> [, <em>nameStr</em>]) {#newfreewave}

</div>

The NewFreeWave function creates a free 1D wave of the given type and number of points and then returns its wave reference.

Recommended for advanced programmers only.

### *Details* {#details}
By default, NewFreeWave creates a free wave named '\_free\_'. You can specify another name via the optional *nameStr* input. The ability to specify the name of a free wave was added in Igor Pro 9.00 as a debugging aid - see [Free Wave Names](/igorpro/programming/programming.md#free-wave-names) and [Wave Tracking](/igorpro/programming/programming-techniques.md#wave-tracking) for details.

You can also create free waves using [Make](/igorpro/commands/make.md)/FREE and [Duplicate](/igorpro/commands/duplicate.md)/FREE. These are preferable for creating multidimensional free waves and also fine for general use.

The *type* parameter can be either a code as documented for [WaveType](/igorpro/commands/wavetype.md), or can be 0 to create a text wave, or 0x100 to create a data folder reference wave, or 0x200 to create a wave reference wave.

You can redimension free waves as desired but, for maximum efficiency, you should create the wave with the desired type and total number of points and then use the /E=1 flag with Redimension to simply reshape without moving data.

A free wave is automatically discarded when the last reference to it disappears.

### *See Also* {#see-also}
[Free Waves](/igorpro/programming/programming.md#free-waves), [Make](/igorpro/commands/make.md), [Duplicate](/igorpro/commands/duplicate.md)