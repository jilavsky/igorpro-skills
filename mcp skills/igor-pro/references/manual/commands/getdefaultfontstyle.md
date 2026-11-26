---
description: "The GetDefaultFontStyle function returns the default font style of the graph or of the graph's axis in the specified window or subwindow."
slug: /commands/getdefaultfontstyle
---

<div className="command-signature">

## <strong>GetDefaultFontStyle</strong> (<em>graphNameStr</em>, <em>axisNameStr</em>) {#getdefaultfontstyle}

</div>

The GetDefaultFontStyle function returns the default font style of the graph or of the graph's axis in the specified window or subwindow.

### *Details* {#details}
If *graphNameStr* is "" the top graph is examined.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

If *axisNameStr* is "", the font style of the default font for the graph is returned.

If named axis exists, the default font style for the named axis in the graph is returned.

If named axis does not exist, NaN is returned.

The function result is a bitwise value with each bit identifying one aspect of the font style as follows:

|  |  |
| --- | --- |
| Bit 0: | Bold |
| Bit 1: | Italic |
| Bit 2: | Underline |
| Bit 4: | Strikethrough |

See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

### *See Also* {#see-also}
[GetDefaultFont](/igorpro/commands/getdefaultfont.md), [GetDefaultFontSize](/igorpro/commands/getdefaultfontsize.md), [FontSizeHeight](/igorpro/commands/fontsizeheight.md), [FontSizeStringWidth](/igorpro/commands/fontsizestringwidth.md)