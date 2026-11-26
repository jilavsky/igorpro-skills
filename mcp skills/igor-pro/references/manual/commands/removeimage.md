---
description: "The RemoveImage operation removes the given image from the target or named graph."
slug: /commands/removeimage
---

<div className="command-signature">

## <strong>RemoveImage</strong>  [/ALL /W=<em>winName</em> /Z] <em>imageInstance</em> {#removeimage}

</div>

The RemoveImage operation removes the given image from the target or named graph.

### *Parameters* {#parameters}
*imageInstance* is usually simply the name of a wave. More precisely, *imageInstance* is a wave name, optionally followed by the # character and an instance number to identify which image of a given wave is to be removed.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ALL</span> | Removes all image plots from the graph. Any image name parameters listed are ignored. /ALL was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Removes an image from the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/Z</span> | Suppresses error if specified image is not on the graph. |

### *Details* {#details}
If the axes used by the given image are not in use after removing the image, they will also be removed.

An image name in a string can be used with the $ operator for *imageInstance*.

### *See Also* {#see-also}
[AppendImage](/igorpro/commands/appendimage.md)