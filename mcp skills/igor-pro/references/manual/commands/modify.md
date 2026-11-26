---
description: "We recommend that you use ModifyGraph, ModifyTable, ModifyLayout, or ModifyPanel rather than Modify."
slug: /commands/modify
---

<div className="command-signature">

## <strong>Modify</strong> {#modify}

</div>

We recommend that you use [ModifyGraph](/igorpro/commands/modifygraph.md), [ModifyTable](/igorpro/commands/modifytable.md), [ModifyLayout](/igorpro/commands/modifylayout.md), or [ModifyPanel](/igorpro/commands/modifypanel.md) rather than Modify. When interpreting a command, Igor treats the Modify operation as ModifyGraph, ModifyTable, ModifyLayout or ModifyPanel, depending on the target window. This does not work when executing a user-defined function.