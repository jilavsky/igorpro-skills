---
description: "The BuildMenu operation rebuilds the user-defined menu items in the specified menu the next time the user clicks in the menu bar."
slug: /commands/buildmenu
---

<div className="command-signature">

## <strong>BuildMenu</strong>  <em>menuNameStr</em> {#buildmenu}

</div>

The BuildMenu operation rebuilds the user-defined menu items in the specified menu the next time the user clicks in the menu bar.

### *Parameters* {#parameters}
*menuNameStr*  is a string expression containing a menu name or "All".

### *Details* {#details}
BuildMenu should be called when you've defined a custom menu using string variables for the menu items. After you change the string variables, call BuildMenu to update the menu.

BuildMenu "All" rebuilds all the menu items and titles and updates the menu bar.

Under the current implementation, if *menuNameStr* is not "All", Igor will rebuild all user-defined menu items if BuildMenu is called for any user-defined menu.

### *See Also* {#see-also}
[Dynamic Menu Items](/igorpro/user-interface/user-defined-menus.md#dynamic-menu-items)