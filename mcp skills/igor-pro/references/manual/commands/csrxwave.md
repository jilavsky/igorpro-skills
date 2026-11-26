---
description: "The CsrXWave function returns a string containing the name of the wave supplying the X coordinates for an XY plot of the Y wave the specified cursor (A…"
slug: /commands/csrxwave
---

<div className="command-signature">

## <strong>CsrXWave</strong> (<em>cursorName</em> [, <em>graphNameStr</em> ]) {#csrxwave}

</div>

The CsrXWave function returns a string containing the name of the wave supplying the X coordinates for an XY plot of the Y wave the specified cursor (A through J) is attached to in the top (or named) graph.

### *Details* {#details}
CsrXWave returns an empty string ("") if the wave the cursor is on is not plotted versus another wave providing the X coordinates (that is, if the wave was not plotted with a command such as `Display theWave vs anotherWave`).

The name of a wave by itself is not sufficient to identify the wave because it does not tell Igor what data folder contains the wave. Thus, if you are calling CsrXWave for the purpose of passing the wave name to other Igor procedures, you should use the [CsrXWaveRef](/igorpro/commands/csrxwaveref.md) function instead. Use CsrXWave if you want the name of the wave to use in an annotation or a notebook.

### *Examples* {#examples}

```igor
Display ywave vs xwave
```

ywave supplies the Y coordinates and xwave supplies the X coordinates for this XY plot.


```igor
Cursor A ywave,0
Print CsrXWave(A)	// prints  xwave
```

### *See Also* {#see-also}
[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors)