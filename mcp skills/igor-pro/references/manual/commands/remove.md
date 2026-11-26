---
description: "When interpreting a command, Igor treats the Remove operation as RemoveFromGraph, RemoveFromTable, or RemoveFromLayout, depending on the target window."
slug: /commands/remove
---

<div className="command-signature">

## <strong>Remove</strong> {#remove}

</div>

When interpreting a command, Igor treats the Remove operation as RemoveFromGraph, RemoveFromTable, or RemoveFromLayout, depending on the target window. This does not work when executing a user-defined function. Therefore we now recommend that you use [RemoveFromGraph](/igorpro/commands/removefromgraph.md), [RemoveFromTable](/igorpro/commands/removefromtable.md), or [RemoveLayoutObjects](/igorpro/commands/removelayoutobjects.md) rather than Remove.