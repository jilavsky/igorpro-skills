---
description: "The RemoveLayoutObjects operation removes the specified object or objects from the top page layout, or from the layout specified by the /W flag."
slug: /commands/removelayoutobjects
---

<div className="command-signature">

## <strong>RemoveLayoutObjects</strong>  [/PAGE=<em>page</em> /W=<em>winName</em> /Z] <em>objectSpec</em>  [, <em>objectSpec</em> ] {#removelayoutobjects}

</div>

The RemoveLayoutObjects operation removes the specified object or objects from the top page layout, or from the layout specified by the /W flag. It targets the active page or the page specified by the /PAGE flag.

Unlike the RemoveFromLayout operation, RemoveLayoutObjects can be used in user-defined functions. Therefore, RemoveLayoutObjects should be used in new programming instead of RemoveFromLayout.

### *Parameters* {#parameters}
*objectSpec*  is either an object name (e.g., Graph0) or an objectName with an instance (e.g., Graph0#1). An instance is needed only if the same object appears in the layout more than one time. Graph0 is equivalent to Graph0#0 and Graph0#1 refers to the second instance of Graph0 in the layout.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/PAGE = *page*</span> | Removes the object from the specified page. |
|  | Page numbers start from 1. To target to the active page, omit /PAGE or use *page*=0. |
|  | The /PAGE flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/W = *winName*</span> | *winName* is the name of the page layout window from which the object is to be removed. If /W is omitted or if *winName* is $"", the top page layout is used. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting if the specified layout object does not exist. |

### *See Also* {#see-also}
[NewLayout](/igorpro/commands/newlayout.md), [AppendLayoutObject](/igorpro/commands/appendlayoutobject.md), [ModifyLayout](/igorpro/commands/modifylayout.md), [LayoutPageAction](/igorpro/commands/layoutpageaction.md)