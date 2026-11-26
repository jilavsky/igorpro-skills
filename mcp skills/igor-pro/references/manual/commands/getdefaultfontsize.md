---
description: "The GetDefaultFontSize function returns the default font size of the graph or of the graph's axis (in points) in the specified window or subwindow."
slug: /commands/getdefaultfontsize
---

<div className="command-signature">

## <strong>GetDefaultFontSize</strong> (<em>graphNameStr</em>, <em>axisNameStr</em>) {#getdefaultfontsize}

</div>

The GetDefaultFontSize function returns the default font size of the graph or of the graph's axis (in points) in the specified window or subwindow.

### *Details* {#details}
If *graphNameStr* is "" the top graph is examined.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

If *axisNameStr* is "", the font size of the default font for the graph is returned.

If named axis exists, the default font size for the named axis in the graph is returned.

If named axis does not exist, NaN is returned.

### *See Also* {#see-also}
[GetDefaultFont](/igorpro/commands/getdefaultfont.md), [GetDefaultFontStyle](/igorpro/commands/getdefaultfontstyle.md), [FontSizeHeight](/igorpro/commands/fontsizeheight.md), [FontSizeStringWidth](/igorpro/commands/fontsizestringwidth.md)