---
description: "The CsrWaveRef function returns a wave reference to the wave the specified cursor (A through J) is on in the top (or named) graph."
slug: /commands/csrwaveref
---

<div className="command-signature">

## <strong>CsrWaveRef</strong> (<em>cursorName</em> [, <em>graphNameStr</em> ]) {#csrwaveref}

</div>

The CsrWaveRef function returns a wave reference to the wave the specified cursor (A through J) is on in the top (or named) graph.

### *Details* {#details}
The wave reference can be used anywhere Igor is expecting the name of a wave (not a string containing the name of a wave).

CsrWaveRef should be used in place of the CsrWave() string function in order to work properly with data folders.

### *Examples* {#examples}

```igor
Print CsrWaveRef(A)[50]             // not CsrWaveRef("A")
Print CsrWaveRef(B,"Graph0")[50]    // in specified graph
```

### *See Also* {#see-also}
[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors), [Wave Reference Functions](/igorpro/programming/programming-techniques.md#wave-reference-functions)