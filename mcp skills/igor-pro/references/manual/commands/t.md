---
description: "The t function returns the T value for the current chunk of the destination wave when used in a multidimensional wave assignment statement."
slug: /commands/t
---

<div className="command-signature">

## <strong>t</strong> {#t}

</div>

The t function returns the T value for the current chunk of the destination wave when used in a multidimensional wave assignment statement. T is the scaled chunk index while s is the chunk index itself.

### *Details* {#details}
Unlike x, outside of a wave assignment statement, t *does not* act like a normal variable.

### *See Also* {#see-also}
[Waveform Arithmetic and Assignment](/igorpro/igor-basics/waves.md#waveform-arithmetic-and-assignment)

For scaled dimension indices, the [x](/igorpro/commands/x.md), [y](/igorpro/commands/y.md), and [z](/igorpro/commands/z.md) functions.

For other dimensions, the [p](/igorpro/commands/p.md), [q](/igorpro/commands/q.md), [r](/igorpro/commands/r.md), and [s](/igorpro/commands/s.md) functions.