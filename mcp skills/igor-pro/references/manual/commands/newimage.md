---
description: "The NewImage operation creates a new image graph much like \"Display;AppendImage matrix \", except that the graph is prepared using a style more appropriate for…"
slug: /commands/newimage
---

<div className="command-signature">

## <strong>NewImage</strong>  [/F/G=<em>g</em> /HIDE=<em>h</em> /HOST=<em>hcSpec</em> /K=<em>k</em> /LAYR=<em>layer</em> /N=<em>name</em> /S=<em>s</em> ] <em>matrix</em> {#newimage}

</div>

The NewImage operation creates a new image graph much like "Display;AppendImage *matrix* ", except that the graph is prepared using a style more appropriate for images. Rather than using preferences, NewImage provides several discrete styles to choose from.

### *Parameters* {#parameters}
*matrix* is usually an MxN matrix containing image data. See the [AppendImage](/igorpro/commands/appendimage.md) command for details.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/F</span> | By default, the image is flipped vertically to correspond to normal image orientation. if /F is present then the image is not flipped. |
| /G=*g* |<table class="nested-table"><tbody><tr><td>*g*&nbsp;=0:</td><td>Default, which is same as no /G flag.</td></tr><tr><td>*g*&nbsp;=1:</td><td>Suppresses the autodetection of three plane images as direct (rgb) color. Flag also suppresses detection of explicit mode.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/HIDE = *h*</span> | Hides (*h* = 1) or shows (*h* = 0, default) the window. |
| <span class="table-cell-nowrap">/HOST = *hcSpec*</span> | Embeds the new image plot in the host window or subwindow specified by *hcSpec*. |
|  | When identifying a subwindow with *hcSpec*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/K = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr><tr><td>*k*&nbsp;=4:</td><td>Kills with no dialog and is not saved with the experiment.</td></tr></tbody></table>
|  | If you use /K=2 or /K=3, you can still kill the window using the [KillWindow](/igorpro/commands/killwindow.md) operation. |
| <span class="table-cell-nowrap">/LAYR = *layer*</span> | Selects an image layer to use for the new image plot. |
|  |<table class="nested-table"><tbody><tr><td>*layer*&nbsp;=&nbsp;0:</td><td>The image will be put into Layer 0 (below axes and traces), and Layer 1 wlll be empty.</td></tr><tr><td>*layer*&nbsp;=&nbsp;1:</td><td>The image will be put into Layer 1 (above axes and traces), and Layer 0 will be empty.</td></tr></tbody></table>
|  | Omitting /LAYR is the same as /LAYR=0. |
| <span class="table-cell-nowrap">/N = *name*</span> | Requests that the created graph have this name, if it is not in use. If it is in use, then *name*0, *name*1, etc are tried until an unused window name is found. In a function or macro, S_name is set to the chosen graph name. |
| <span class="table-cell-nowrap">/PACK = *pkMode*</span> | Use this flag to specify the binary packaging of the image. By default, *pkMode*=packSTD, where 2D numeric waves represent grayscale images and 3D waves represent color images. See [Direct Color Packing Modes](/igorpro/graphing/image-plots.md#direct-color-packing-modes) for more information. |
| <span class="table-cell-nowrap">/S = *s*</span> | *s* specifies one of several styles. If /S is not present, *s* =2 is the default. |
|  |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=0:</td><td>Fills entire window with image. No axes. However, this can result in the lower right corner not being visible due to the target icon.</td></tr><tr><td>*s*&nbsp;=1:</td><td>Like *s* =0 but insets image to avoid corner icon.</td></tr><tr><td>*s*&nbsp;=2:</td><td>Provides minimalist axes (default).</td></tr></tbody></table>

### *Details* {#details}
The graph is sized to make the image pixels a multiple of the screen pixels with the graph size constrained to be not too small and not too large.

If *matrix* appears to fit Igor's standard monochrome category, then explicit mode is set (See ModifyImage explicit). To be considered monochrome the wave must be unsigned byte and contain only values of 0, 64 or 255.

Once the graph is created it is a normal graph and has no special properties other than the settings it was created with. Specifically, it will not autosize itself if the dimensions of *matrix* are changed. NewImage is just a shortcut for creating a graph window with a style appropriate for images.

This operation is limited in scope by design. If you need to specify the position, size or title, then use the operations Display and AppendImage.

If the styles provided are not what you desire, touch up an image graph to meet your needs and then use Capture Graph Prefs from the Graphs menu. Then use "Display; AppendImage" rather than NewImage.

### *See Also* {#see-also}
[Display](/igorpro/commands/display.md), [AppendImage](/igorpro/commands/appendimage.md), [ModifyImage](/igorpro/commands/modifyimage.md)

[Direct Color Packing Modes](/igorpro/graphing/image-plots.md#direct-color-packing-modes)