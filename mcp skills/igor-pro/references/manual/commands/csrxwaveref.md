---
description: "The CsrXWaveRef function returns a wave reference to the wave supplying the X coordinates for an XY plot of the Y wave the specified cursor (A through J) is…"
slug: /commands/csrxwaveref
---

<div className="command-signature">

## <strong>CsrXWaveRef</strong> (<em>cursorName</em> [, <em>graphNameStr</em>]) {#csrxwaveref}

</div>

The CsrXWaveRef function returns a wave reference to the wave supplying the X coordinates for an XY plot of the Y wave the specified cursor (A through J) is attached to in the top (or named) graph.

### *Details* {#details}
The wave reference can be used anywhere Igor is expecting the name of a wave (not a string containing the name of a wave).

CsrXWaveRef returns a null reference (see [WaveExists](/igorpro/commands/waveexists.md)) if the wave the cursor is on is not plotted versus another wave providing the X coordinates (that is, if the wave was not plotted with a command such as `Display theWave vs anotherWave`). CsrXWaveRef should be used in place of the CsrXWave() string function in order to work properly with data folders.

### *Examples* {#examples}

```igor
Display ywave vs xwave
```

ywave supplies the Y coordinates and xwave supplies the X coordinates for this XY plot.


```igor
Cursor A ywave,0
Print CsrXWaveRef(A)[50]	// prints value of xwave at point #50
```

### *See Also* {#see-also}
[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors), [Wave Reference Functions](/igorpro/programming/programming-techniques.md#wave-reference-functions)