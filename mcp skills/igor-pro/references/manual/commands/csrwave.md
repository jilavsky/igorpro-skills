---
description: "The CsrWave function returns a string containing the name of the wave the specified cursor (A through J) is on in the top (or named) graph."
slug: /commands/csrwave
---

<div className="command-signature">

## <strong>CsrWave</strong> (<em>cursorName</em> [, <em>graphNameStr</em> [, <em>wantTraceName</em> ]]) {#csrwave}

</div>

The CsrWave function returns a string containing the name of the wave the specified cursor (A through J) is on in the top (or named) graph. If the optional *wantTraceName* is nonzero, the trace name is returned. A trace name is the wave name with optional instance notation (see [ModifyGraph for Traces](/igorpro/commands/modifygraph.md#modifygraph-for-traces)).

### *Details* {#details}
The name of a wave by itself is not sufficient to identify the wave because it does not tell Igor what data folder contains the wave. Thus, if you are calling CsrWave for the purpose of passing the wave name to other Igor procedures, you should use the [CsrWaveRef](/igorpro/commands/csrwaveref.md) function instead. Use CsrWave if you want the name of the wave to use in an annotation or a notebook.

### *Examples* {#examples}

```igor
String waveCursorAIsOn = CsrWave(A)             // not CsrWave("A")
String waveCursorBIsOn = CsrWave(B,"Graph0")    // in specified graph
String traceCursorBIsOn = CsrWave(B,"",1)       // trace name in top graph
```

### *See Also* {#see-also}
[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors)

[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)