---
description: "The PanelResolution function returns the current resolution of the specified window in pixels per inch."
slug: /commands/panelresolution
---

<div className="command-signature">

## <strong>PanelResolution</strong> (<em>wName</em>) {#panelresolution}

</div>

The PanelResolution function returns the current resolution of the specified window in pixels per inch.

If *wName* is empty, it returns the current global setting for panel resolution in pixels per inch which is controlled by [SetIgorOption PanelResolution](/igorpro/user-interface/platform-related-issues.md#setigoroption-panelresolution), and (for panels) the [ModifyPanel](/igorpro/commands/modifypanel.md) expand command.

If *wName* is the name of a graph window, it returns the resolution for the [ControlBar](/igorpro/commands/controlbar.md) area in pixels per inch.

*wName* can be a subwindow specification.

The PanelResolution function was added in Igor Pro 7.00.

When ScreenResolution is 96 DPI, which is typical for normal-resolution screens, panels are (re-)created presuming a 72 DPI panel resolution, to create panels at a size comparable to panels created with Igor Pro 6. This makes the panels 75% of the size they would be if 96 DPI was used.

Use the [ModifyPanel](/igorpro/commands/modifypanel.md) operation's expand parameter to change the PanelResolution of a panel, which also changes the size of the window and of the contained controls.

### *See Also* {#see-also}
[Control Panel Resolution on Windows](/igorpro/user-interface/platform-related-issues.md#control-panel-resolution-on-windows), [ScreenResolution](/igorpro/commands/screenresolution.md), [ModifyPanel](/igorpro/commands/modifypanel.md), [Control Panel Expansion](/igorpro/user-interface/controls.md#control-panel-expansion)