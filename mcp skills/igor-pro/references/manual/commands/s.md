---
description: "The s function returns the current chunk index of the destination wave when used in a multidimensional wave assignment statement."
slug: /commands/s
---

<div className="command-signature">

## <strong>s</strong> {#s}

</div>

The s function returns the current chunk index of the destination wave when used in a multidimensional wave assignment statement. The corresponding scaled chunk index is available as the t function.

### *Details* {#details}
Unlike p, outside of a wave assignment statement, s *does not* act like a normal variable.

### *See Also* {#see-also}
[Waveform Arithmetic and Assignment](/igorpro/igor-basics/waves.md#waveform-arithmetic-and-assignment).

For other dimensions, the [p](/igorpro/commands/p.md), [q](/igorpro/commands/q.md), and [r](/igorpro/commands/r.md) functions.

For scaled dimension indices, the [x](/igorpro/commands/x.md), [y](/igorpro/commands/y.md), [z](/igorpro/commands/z.md), and [t](/igorpro/commands/t.md) functions.