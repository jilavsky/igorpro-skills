---
description: "The BoxSmooth operation replaces smoothedWave with a smoothed copy of srcWave. The waves must both exist."
slug: /commands/boxsmooth
---

<div className="command-signature">

## <strong>BoxSmooth</strong>  <em>box</em>, <em>srcWave</em>, <em>smoothedWave</em> {#boxsmooth}

</div>

The BoxSmooth operation replaces *smoothedWave* with a smoothed copy of *srcWave*. The waves must both exist.

The BoxSmooth operation is used primarily by Igor Technical Note #20 and its variants. For most purposes, use the more flexible [Smooth](/igorpro/commands/smooth.md) operation instead of BoxSmooth.

### *Parameters* {#parameters}
*box* is the number of *srcWave* points averaged to form each *smoothedWave* point. If you specify an even number, the next-higher odd number is used.

### *Details* {#details}
BoxSmooth is equivalent to the [Smooth](/igorpro/commands/smooth.md) operation with the /B flag, except that BoxSmooth does not compute the result in-place like Smooth does. This command:


```igor
BoxSmooth box, srcWave, smoothedWave
```

is equivalent to:


```igor
Duplicate/O srcWave, smoothedWave
Smooth/B/DIM=-1/E=3/F=0 box, smoothedWave
```