---
description: "The HideIgorMenus operation hides the named built-in menus or, if none are explicitly named, hides all built-in menus in the menu bar."
slug: /commands/hideigormenus
---

<div className="command-signature">

## <strong>HideIgorMenus</strong>   [<em>MenuNameStr</em>  [,<em>MenuNameStr</em> ] ... {#hideigormenus}

</div>

The HideIgorMenus operation hides the named built-in menus or, if none are explicitly named, hides all built-in menus in the menu bar.

The effect of HideIgorMenus is lost when a new experiment is opened. The state of HideIgorMenus is saved with the experiment.

User-defined menus are not hidden by HideIgorMenus unless attached to built-in menus and the menu definition uses the hideable keyword.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *MenuNameStr* | The name of an Igor menu, like "File", "Data", or "Graph". |

### *Details* {#details}
The optional menu names are in English and not abbreviated. This ensures that code developed for a localized version of Igor will run on all versions.

The built-in menus that can be shown or hidden (the Help menu can be hidden only on Windows) are those that appear in the menu bar:

|  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- |
| File | Edit | Data | Analysis | Macros | Windows | Graph |
| Layout | Notebook | Panel | Procedure | Table | Misc | Help |

Hiding a built-in menu to which a user-defined menu is attached results in a built-in menu with only the user-defined items. For example, if this menu definition attaches items to the built-in Graph menu:


```igor
Menu "Graph"
	"Do My Graph Thing", ThingFunction()
End
```

Calling HideIgorMenus "Graph" will still leave a Graph menu showing (when a Graph is the top-most target window) with only the user-defined menu(s) in it: in this example the one "Do My Graph Thing" item.

Hiding the Macros menu hides menus created from Macro definitions like:


```igor
Macro MyMacro()
	Print "Hello, world."
End
```

but does not hide normal user-defined Macros definitions like:


```igor
Menu "Macros"
	"Macro 1", MyMacro(1)
End
```

You can set user-defined menus to hide and show along with built-in menus by adding the optional hideable keyword to the menu definition:


```igor
Menu "Graph", hideable
	"Do My Graph Thing", ThingFunction()
End
```

Then HideIgorMenus "Graph" will hide those items, too. If all user-defined Graph menu definitions use the hideable keyword, then no Graph menu will appear in the menu bar.

Some WaveMetrics procedures use the hideable keyword so that only customer-defined menus remain when HideIgorMenus is executed.

### *See Also* {#see-also}
[ShowIgorMenus](/igorpro/commands/showigormenus.md), [DoIgorMenu](/igorpro/commands/doigormenu.md), [SetIgorMenuMode](/igorpro/commands/setigormenumode.md), [User-Defined Menus](/igorpro/user-interface/user-defined-menus.md)