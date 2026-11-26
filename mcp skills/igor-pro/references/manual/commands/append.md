---
description: "The Append operation is interpreted as AppendToGraph, AppendToTable, or AppendToLayout, depending on the target window."
slug: /commands/append
---

<div className="command-signature">

## <strong>Append</strong> {#append}

</div>

The Append operation is interpreted as AppendToGraph, AppendToTable, or AppendToLayout, depending on the target window. This does not work when executing a user-defined function. Therefore we now recommend that you use [AppendToGraph](/igorpro/commands/appendtograph.md), [AppendToTable](/igorpro/commands/appendtotable.md), or [AppendLayoutObject](/igorpro/commands/appendlayoutobject.md) rather than Append.