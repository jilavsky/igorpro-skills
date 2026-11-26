---
description: "The ShowIgorMenus operation shows the named built-in menus or, if none are explicitly named, shows all built-in menus in the menu bar."
slug: /commands/showigormenus
---

<div className="command-signature">

## <strong>ShowIgorMenus</strong>   [<em>MenuNameStr</em>  [,<em>MenuNameStr</em> ] ... {#showigormenus}

</div>

The ShowIgorMenus operation shows the named built-in menus or, if none are explicitly named, shows all built-in menus in the menu bar.

User-defined menus attached to built-in menus are also affected by this operation.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *MenuNameStr* | The name of an Igor menu, like "File", "Data", or "Graph". |

### *Details* {#details}
See [HideIgorMenus](/igorpro/commands/hideigormenus.md) for details.

### *See Also* {#see-also}
[HideIgorMenus](/igorpro/commands/hideigormenus.md), [DoIgorMenu](/igorpro/commands/doigormenu.md), [SetIgorMenuMode](/igorpro/commands/setigormenumode.md), [User-Defined Menus](/igorpro/user-interface/user-defined-menus.md)