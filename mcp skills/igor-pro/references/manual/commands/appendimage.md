---
description: "The AppendImage operation appends the matrix as an image to the target or named graph. By default the image is plotted versus the left and bottom axes."
slug: /commands/appendimage
---

<div className="command-signature">

## <strong>AppendImage</strong>  [/G=<em>g</em> /LAYR=<em>layer</em> /W=<em>winName</em>][<em>axisFlags</em>] <em>matrix</em> [<em>vs</em> {<em>xWaveName</em>, <em>yWaveName</em>}] {#appendimage}

</div>

The AppendImage operation appends the matrix as an image to the target or named graph. By default the image is plotted versus the left and bottom axes.

### *Parameters* {#parameters}
*matrix* is either an NxM matrix for false color or indexed color images or can be a 3D NxMx3 wave containing a plane of data for red, a plane for green and a plane for blue. It can also be a 3D NxMx4 wave with the fourth plane containing alpha values.

If *matrix* contains multiple planes other than three or four, or if it contains three or four planes and multiple chunks, the [ModifyImage](/igorpro/commands/modifyimage.md) plane keyword can be used to specify the desired subset to display.

If you provide *xWaveName*  and *yWaveName* , *xWaveName*  provides X coordinate values, and *yWaveName*  provides Y coordinate values. This makes an image with uneven pixel sizes. In both cases, you can use * to specify calculated values based on the dimension scaling of *matrix*. See Details below if you use *xWaveName*  or *yWaveName*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| *axisFlags* | Flags /L/R/B/T are the same as used by [AppendToGraph](/igorpro/commands/appendtograph.md). |
| /G=*g* |<table class="nested-table"><tbody><tr><td>*g*&nbsp;=1:</td><td>Suppresses the auto-detection of three or four plane images as direct (rgb) color.</td></tr><tr><td>*g*&nbsp;=&nbsp;0:</td><td>Same as no /G flag (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/LAYR = *layer*</span> | Selects an image layer to insert the image into. |
|  |<table class="nested-table"><tbody><tr><td>*layer*&nbsp;=&nbsp;0:</td><td>Insert the image at the topmost position in Layer 0 (that is, at the end of the Layer 0 list), below traces and axes.</td></tr><tr><td>*layer*&nbsp;=&nbsp;1:</td><td>Insert the image at the topmost position in Layer 1 (that is, at the end of the Layer 1 list), above traces and axes.</td></tr></tbody></table>
|  | Omitting /LAYR is the same as /LAYR=0. |
| <span class="table-cell-nowrap">/PACK = *pkMode*</span> | Use this flag to specify the binary packaging of the image.  By default, *pkMode*=packSTD, where 2D numeric waves represent grayscale images and 3D waves represent color images. See [Direct Color Packing Modes](/igorpro/graphing/image-plots.md#direct-color-packing-modes) for more information. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Appends to the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
When appending an image to a graph each image data point is displayed as a rectangle. You can supply optional X and Y waves to define the coordinates of the rectangle edges. *These waves must contain one more data point than the X (row) or Y (column) dimension of the matrix.* The waves must also be either strictly increasing or strictly decreasing. See [Image X and Y Coordinates](/igorpro/graphing/image-plots.md#image-x-and-y-coordinates) for details.

For false color, the values in the matrix are linearly mapped into a color table. See the ctab keyword as used in the [ModifyImage](/igorpro/commands/modifyimage.md) operation. For indexed color, the values in the matrix are interpreted as Z values to be looked up in a user-supplied 3 column matrix of colors. See the cindex keyword as used in the [ModifyImage](/igorpro/commands/modifyimage.md) operation. Direct color NxMx3 waves contain the actual red, green and blue values for each pixel. NxMx4 waves add an alpha channel. If the number type is unsigned bytes, then the range of intensity ranges from 0 to 255. For all other number types, the intensity ranges from 0 to 65535.

By default, nondirect color matrices are initially displayed as false color using the Grays color table and autoscale mode.

If the matrix is complex, the image is displayed in terms of the magnitude of the Z value, that is, sqrt(real<sup>2</sup> + imag<sup>2</sup>).

### *See Also* {#see-also}
[Image X and Y Coordinates](/igorpro/graphing/image-plots.md#image-x-and-y-coordinates), [Color Blending](/igorpro/graphing/making-figures/graphics.md#color-blending)

[NewImage](/igorpro/commands/newimage.md), [ModifyImage](/igorpro/commands/modifyimage.md), [RemoveImage](/igorpro/commands/removeimage.md)