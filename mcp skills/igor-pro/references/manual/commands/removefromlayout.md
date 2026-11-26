---
description: "Deprecated. Use RemoveLayoutObjects. The RemoveFromLayout operation removes the specified objects from the top layout."
slug: /commands/removefromlayout
---

<div className="command-signature">

## <strong>RemoveFromLayout</strong>  <em>objectSpec</em> [, <em>objectSpec</em> ]... {#removefromlayout}

</div>

:::warning
Deprecated. Use [RemoveLayoutObjects](/igorpro/commands/removelayoutobjects.md).
:::

The RemoveFromLayout operation removes the specified objects from the top layout.

Unlike the RemoveFromLayout operation, RemoveLayoutObjects can be used in user-defined functions. Therefore RemoveLayoutObjects should be used in new programming instead of RemoveFromLayout.

### *Parameters* {#parameters}
*objectSpec* is either an object name (e.g., Graph0) or an *objectName* with an instance (e.g., Graph0#1). An instance is needed only if the same object appears in the layout more than one time. Graph0 is equivalent to Graph0#0 and Graph0#1 refers to the second instance of Graph0 in the layout.

### *See Also* {#see-also}
[RemoveLayoutObjects](/igorpro/commands/removelayoutobjects.md)