---
description: "The ModifyImage operation changes properties of the given image in the top graph (or the specified graph if /W is used)."
slug: /commands/modifyimage
---

<div className="command-signature">

## <strong>ModifyImage</strong>  [/W=<em>winName</em> ] <em>imageInstance</em> , <em>keyword</em> =<em>value</em>  [, <em>keyword</em> =<em>value</em>  ...] {#modifyimage}

</div>

The ModifyImage operation changes properties of the given image in the top graph (or the specified graph if /W is used). *imageInstance* is the name of the image to be altered. This name is usually simply the name of the matrix wave containing the image data. If the same matrix wave is displayed more than once, you must append #0, #1 etc. to the name to distinguish which is which.

*imageInstance* can also take the form of a null name with an instance number to affect the instanceth image. That is,


```igor
ModifyImage ''#1 // Two single quotes are used, not a double quote
```

modifies the appearance of the second image that was appended to the top graph, no matter what the image names are.

### *Parameters* {#parameters}
Here are the keyword-value pairs. These apply to false color images in which the data in the matrix is used as an index into a color table. They do not apply to direct color images in which the data in the matrix specifies the color directly.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">cindex = *matrixWave*</span> | Sets the Z value mapping mode such that image colors are determined by doing a lookup in the specified matrix wave. |
|  | *matrixWave* is a 3 column wave that contains red, green and blue values from 0 to 65535. (The matrix can actually have more than three columns. It ignores any extra columns.) |
|  | The color at Z=*z* is determined by finding the RGB values in the row of *matrixWave* whose scaled X index is z. In other words, the red value is matrixWave(z)[0], the green value is matrixWave(z)[1] and the blue value is matrixWave(z)[2]. |
|  | If *matrixWave* has default X scaling, where the scaled X index equals the point number, then row 0 contains the color for Z=0, row 1 contains the color for Z=1, etc. |
|  | If you use cindex, you should not use ctab in the same command. |
| <span class="table-cell-nowrap">ctab = {*zMin*, *zMax*, *ctName*, *reverse* }</span> |  |
|  | Sets the z mapping mode by which values in the matrix are mapped linearly into the color table specified by *ctName*. |
|  | *zMin* and *zMax* set the range of z values to map. Omit *zMin* or *zMax* to leave as is, or use * to autoscale either or both. |
|  | *ctName* can be any color table name returned by the [CTabList](/igorpro/commands/ctablist.md) function, such as Grays or Rainbow (see [Color Tables](/igorpro/graphing/contour-plots.md#color-tables)) or the name of a 3 column or 4 column color table wave (see [Color Table Waves](/igorpro/graphing/image-plots.md#color-table-waves)). |
|  | The color table name can be missing if you want to leave it as is. |
|  | A color table wave name supplied for *ctName* must not be the name of a built-in color table (see [CTabList](/igorpro/commands/ctablist.md)). A 3 column or 4 column color table wave must have values that range between 0 and 65535. Column 0 is red, 1 is green, and 2 is blue. In the optional column 3, a value of 65535 is opaque, and 0 is fully transparent. |
|  | Set *reverse* to 1 to reverse the color table. Setting it to 0 or omitting it leaves the color table order unreversed. Setting it to -1 leaves the current value unchanged. |
| <span class="table-cell-nowrap">ctabAutoscale = *autoBits*</span> |  |
|  | Sets the range of data used for autoscaling ctab's *zMin* or *zMax* values when \* is used instead of a numeric expression. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Autoscales only the XY subset being displayed.</td></tr><tr><td>Bit&nbsp;1:</td><td>Autoscales only the current plane being displayed.</td></tr></tbody></table>
|  | If neither bit is set (if *autoBits* = 0, the default), then all of the data in the image wave is used to autoscale the \* *zMin*, *zMax* values for ctab. |
| <span class="table-cell-nowrap">eval = {*value*, *red*, *green*, *blue* [, *alpha*]}</span> |  |
|  | If the red, green and blue values are in the valid range for a color value (0 to 65535) the explicit value-color pair is added (or updated if value already exists). If the color values are out of range (-1 is suggested) then the value is removed from the list if it is present (no error if it is not). |
|  | *alpha* is optional: a value of 65535 is opaque, and 0 is fully transparent. |
| <span class="table-cell-nowrap">explicit = 1 *or* 0</span> | Turns explicit (monochrome) mode on (1) or off (0). Meant to be used with unsigned byte data but will do the best it can for other types. If value of data is equal to one of the defined explicit values then its defined color is used otherwise the pixel will be blank. The default predefined values are: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>white</td></tr><tr><td>255:</td><td>black</td></tr></tbody></table>
|  | You can add/change/delete explicit values with the eval keyword. |
| <span class="table-cell-nowrap">genericNotRGB = *v*</span> | Controls the auto-detection of three or four plane images: |
|  |<table class="nested-table"><tbody><tr><td>*v*&nbsp;=&nbsp;0:</td><td>Three and four plane images are treated as direct color (RGB or RGBA). This is the default if genericNotRGB is omitted.</td></tr><tr><td>*v*&nbsp;=&nbsp;1:</td><td>Suppresses the auto-detection of three or four plane images as direct color (RGB or RGBA), like AppendImage/G=1.</td></tr></tbody></table>
|  | The genericNotRGB keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">imCmplxMode = *m*</span> | Sets complex data display mode. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Magnitude (default).</td></tr><tr><td>*m*&nbsp;=1:</td><td>Real only.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Imaginary only.</td></tr><tr><td>*m*&nbsp;=3:</td><td>Phase in radians.</td></tr></tbody></table>
| <span class="table-cell-nowrap">interpolate = *mode*</span> | *mode* = 1 turns on smoothing of the boundaries between pixels. Since this is implemented via system graphics calls and not by Igor actually doing the interpolation, it will not affect EPS or EMF export on Windows and will not affect EPS export on Mac. Although this may create a more esthetically pleasing display, it is not clear that it is appropriate for scientific data. |
|  | *mode* = -1 forces pixels to be drawn as individual rectangles. This is sometimes needed when a third-party program improperly interpolates PDF or EPS exported images. |
| <span class="table-cell-nowrap">log = 1 *or* 0</span> | 0 sets the default linearly-spaced false-image colors. |
|  | 1 turns on logarithmically-spaced false-image colors. This requires that the image values be greater than 0 to display correctly. |
|  | Affects the image colors for color table and color index images only (see [Color Table Details](/igorpro/graphing/image-plots.md#color-table-details) and [Indexed Color Details](/igorpro/graphing/image-plots.md#indexed-color-details)). |
| <span class="table-cell-nowrap">lookup = *waveName*</span> | Specifies an optional 1D wave that can be used to modify the mapping of scaled z values into the color table specified with the ctab keyword. Values should range from 0.0 to 1.0. A linear ramp from 0 to 1 would have no effect while a ramp from 1 to 0 would reverse the image. Used to apply gamma correction to grayscale images or for special effects. Use a NULL wave ($"") to remove option. |
| <span class="table-cell-nowrap">maxRGB = (*red*, *green*, *blue* [, *alpha*])</span> |  |
|  | Sets the color of image values greater than the ctab *zMax* or greater than the cindex *matrixWave*'s maximum X scaling value. Also turns max color mode on. |
|  | The *red*, *green*, and *blue* color values are in the range of 0 to 65535. |
|  | *alpha* is optional: a value of 65535 is opaque, and 0 is fully transparent. |
| <span class="table-cell-nowrap">maxRGB = 1 *or* 0 *or* NaN</span> |  |
|  | Turns max color mode off, on, or transparent. These modes affect the display of image values greater than the ctab *zMax* or greater than the cindex *matrixWave*'s maximum X scaling value. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Turns max color mode off (default). The color of the affected image pixels is the last color table or color index color.</td></tr><tr><td>1:</td><td>Turns max color mode on. The color of the affected image pixels is black or the last color set by maxRGB=(*red*, *green*, *blue* ).</td></tr><tr><td>NaN:</td><td>Transparent max color mode. The affected image pixels are not drawn.</td></tr></tbody></table>
| <span class="table-cell-nowrap">minRGB = (*red*, *green*, *blue* [, *alpha*])</span> |  |
|  | Sets the color of image values less than the ctab *zMin* or less than the cindex *matrixWave*'s minimum X scaling value. Also turns min color mode on. |
|  | The *red*, *green*, and *blue* color values are in the range of 0 to 65535. |
|  | *alpha* is optional: a value of 65535 is opaque, and 0 is fully transparent. |
| <span class="table-cell-nowrap">minRGB = 1 *or* 0 *or* NaN</span> |  |
|  | Turns min color mode off, on, or transparent. These modes affect the display of image values less than the ctab *zMin* or less than the cindex *matrixWave*'s minimum X scaling value. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Turns min color mode off (default). The color of the affected image pixels is the first color table or color index color.</td></tr><tr><td>1:</td><td>Turns min color mode on. The color of the affected image pixels is black or the last color set by minRGB=(*red*, *green*, *blue* ).</td></tr><tr><td>NaN:</td><td>Transparent min color mode. The affected image pixels are not drawn.</td></tr></tbody></table>
| <span class="table-cell-nowrap">packingMode = *pkMode*</span> | Use this flag to specify the binary packaging of the image.  By default, *pkMode*=packSTD, where 2D numeric waves represent grayscale images and 3D waves represent color images. See [Direct Color Packing Modes](/igorpro/graphing/image-plots.md#direct-color-packing-modes) for more information. |
| <span class="table-cell-nowrap">plane = *p*</span> | Determines which part of a 3D or 4D image wave to display. |
|  | The meaning of *p* depends on the nature of the image wave. If the size of the layer dimension of the image wave is exactly three then the wave is treated as RGB data with R, G, and B data in the three layers. If the size of the layer dimension is exactly four, then the wave is treated as RGBA data, with A in the fourth layer. Otherwise each layer of the wave is treated as a separate grayscale image. |
|  | ***Plane=p With RGB or RGBA Data*** |
|  | If the wave is 3D, plane=*p* has no effect. |
|  | If the wave is 4D, each chunk contains a different set of R, G and B layers and *p* selects which chunk to display. |
|  | ***Plane=p With Grayscale Data*** |
|  | If the wave is 3D, plane=*p* selects which layer to display. |
|  | If the wave is 4D, plane=*p* acts as if all of the chunks were combined into a virtual 3D wave and *p* selects which layer of this virtual 3D wave to display. |
| <span class="table-cell-nowrap">rgbMult = *m*</span> | If *m* is non-zero, direct color values in a 3-plane RGB or 4-plane RGBA image are multiplied by *m*. (Alpha values are not multiplied.) This would typically be used for 10, 12 or 14 bit integers in a 16 bit word. For example, if your image data is 14 bits, use rgbMult=4. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Directs action to a specific window or subwindow. When omitted, action will affect [the target window](/igorpro/igor-basics/using-igor.md#the-target-window) or its active subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Examples* {#examples}

```igor
ModifyImage ''#0 ctab= {*,*,Turbo}  // Change first image in graph to Turbo color table, autoscale zMin,zMax
ModifyImage ''#0 ctab= {0,*,,1}     // Reverse unchanged color table, zMin=0, zMax autoscaled to entire matrix
ModifyImage ''#0 ctabAutoScale=3    // Autoscale zMax using visible XY subset, only the current plane
ModifyImage ''#0 ctab= {,,Grays,-1} // Change only the color table; leave zMin, zMax, and reverse alone
// Create and apply a two-color Color Table Wave
Make/O/N=(2,3) StopGo               // First color is fully red, second is fully green
StopGo[0][0] = {0,65535}            // Reds
StopGo[0][1] = {65535,0}            // Greens
StopGo[0][2] = {0,0}                // Blues
ModifyImage ''#0 ctab= {0,100,StopGo,0} // Use un-reversed color table wave, zMin=0, zMax=100
```

### ** {#}
### *See Also* {#see-also}
[AppendImage](/igorpro/commands/appendimage.md), [RemoveImage](/igorpro/commands/removeimage.md)