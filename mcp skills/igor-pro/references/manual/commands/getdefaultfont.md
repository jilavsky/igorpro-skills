---
description: "The GetDefaultFont function returns a string containing the name of the default font for the named window or subwindow."
slug: /commands/getdefaultfont
---

<div className="command-signature">

## <strong>GetDefaultFont</strong> (<em>winName</em>) {#getdefaultfont}

</div>

The GetDefaultFont function returns a string containing the name of the default font for the named window or subwindow.

### *Parameters* {#parameters}
If *winName* is null (that is, "") returns the default font for the experiment.

When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Details* {#details}
Only graph windows and the experiment as a whole have default fonts. If winName is the name of a window other than a graph (e.g., a layout), or if winName is not the name of any window, GetDefaultFont returns the experiment default font.

In user-defined functions font names are usually evaluated at compile time. To use the output of GetDefaultFont in a user-defined function, you will usually need to build a command as a string expression and execute it with the [Execute](/igorpro/commands/execute.md) operation.

### *Examples* {#examples}

```igor
String fontName = GetDefaultFont("Graph0")
String command= "SetDrawEnv fname=\"" + fontName + "\", save"
Execute command
```

### *See Also* {#see-also}
[GetDefaultFontSize](/igorpro/commands/getdefaultfontsize.md), [GetDefaultFontStyle](/igorpro/commands/getdefaultfontstyle.md), [FontSizeHeight](/igorpro/commands/fontsizeheight.md), [FontSizeStringWidth](/igorpro/commands/fontsizestringwidth.md)