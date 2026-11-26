---
description: "The SetIgorMenuMode operation allows an Igor programmer to disable or enable Igor's built-in menus and menu items."
slug: /commands/setigormenumode
---

<div className="command-signature">

## <strong>SetIgorMenuMode</strong>  <em>MenuNameStr</em>, <em>MenuItemStr</em>, <em>Action</em> {#setigormenumode}

</div>

The SetIgorMenuMode operation allows an Igor programmer to disable or enable Igor's built-in menus and menu items. This is useful for building applications that will be used by end-users that shouldn't have access to all Igor's extensive and confusing functionality.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *MenuNameStr* | The name of an Igor menu, like "File", "Graph", or "Load Waves". |
| *MenuItemStr* | The text of an Igor menu item, like "Copy" (in the Edit menu) or "New Graph" (in the Windows menu). |
| *Action* | One of DisableItem, EnableItem, DisableAllItems, or EnableAllItems. |
|  | DisableItem and EnableItem disable or enable just the single item named by *MenuNameStr* and *MenuItemStr*. If *MenuItemStr* is "", then the menu itself is disabled. |
|  | DisableAllItems and EnableAllItems disable/enable all the items in the menu named by *MenuNameStr*. |

### *Details* {#details}
All menu names and menu item text are in English. This ensures that code developed for a localized version of Igor will run on all versions. Note that no trailing "..." is used in *MenuItemStr*.

The SetIgorMenuModeProc.ipf procedure file is provided with procedures and commands that disable/enable every menu and item possible. It is in your Igor Pro folder, in WaveMetrics Procedures:Utilities. It is not intended to be used as-is. You should make a copy and edit the copy to include just the parts you need.

The text of some items in the File menu changes depending on the type of the active window. In these cases you must pass generic text as the *MenuItemStr*  parameter. Use "Save Window", "Save Window As", "Save Window Copy", "Adopt Window" and "Revert Window" instead of "Save Notebook" or "Save Procedure", etc. Use "Page Setup" instead of "Page Setup For All Graphs", etc. Use "Print" instead of "Print Graph", etc.

### *See Also* {#see-also}
[DoIgorMenu](/igorpro/commands/doigormenu.md), [ShowIgorMenus](/igorpro/commands/showigormenus.md), [HideIgorMenus](/igorpro/commands/hideigormenus.md)

The SetIgorMenuModeProc.ipf WaveMetrics procedure file contains SetIgorMenuMode commands for every menu and menu item. You can load it using


```igor
#include <SetIgorMenuModeProc>
```