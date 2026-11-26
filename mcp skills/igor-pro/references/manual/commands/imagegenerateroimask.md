---
description: "The ImageGenerateROIMask operation creates a Region Of Interest (ROI) mask for use with ImageXXX commands."
slug: /commands/imagegenerateroimask
---

<div className="command-signature">

## <strong>ImageGenerateROIMask</strong>  [/E=<em>e</em> /I=<em>i</em> /W=<em>winName</em> ] <em>imageInstance</em> {#imagegenerateroimask}

</div>

The ImageGenerateROIMask operation creates a Region Of Interest (ROI) mask for use with ImageXXX commands. It assumes the top (or /W specified) graph contains an image and that the user has drawn shapes using Igor's drawing tools in a specific manner.

ImageGenerateROIMask creates an unsigned byte mask matrix with the same x and y dimensions and scaling as the specified image. The mask is initially filled with zeros. Then the drawing layer, progFront, in the graph is scanned for suitable fillable draw objects. The area inside each shape is filled with ones unless the fill mode for the shape is set to erase in which case the area is filled with zeros.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave. |
|  | When used in a function, ImageGenerateROIMask creates a real wave reference for the *destWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/E = *e*</span> | Changes value used for the exterior from the default zero values to *e*. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/I = *i*</span> | Changes value used for the interior from the default one values to *i*. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Looks for the named graph window or subwindow containing appropriate image masks drawn by the user. If /W is omitted, ImageGenerateROIMask looks in the top graph window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
To generate an ROI wave for use with most image processing operations you need to set the values of interior pixels to zero and exterior pixels to one using /E=1/I=0.

Suitable objects are those that can be filled (rectangles, ovals, etc.) and which are plotted in axis coordinate mode specified using the same axes by which the specified image instance is displayed. Object plotted in plot relative mode are also used, However, this is not recommended because it will give correct results only if the image exactly fills the plot rectangle. If you use axis coordinate mode then you can zoom in or out as desired and the resulting mask will still be correct.

Note that the shapes can have their fill mode set to none. This still results in a fill of ones. This is to allow the drawn ROI to be visible on the graph without obscuring the image. However cutouts (fills with erase mode) will obscure the image.

Note also that nonfill drawing objects are ignored. You can use this fact to create callouts and other annotations.

In a future version of Igor, we may create a new drawing layer in graphs dedicated to ROIs.

If you use the /DEST flag the mask is stored in *destWave*. Otherwise it is stored in the wave M_ROIMask in the current data folder.

Variable V_flag is set to 1 if the top graph contained draw objects in the correct layer and 0 if not. If 0 then the M_ROIMask wave was not generated.

### *Examples* {#examples}

```igor
Make/O/N=(200,400) jack=x*y; NewImage jack; ShowTools
SetDrawLayer ProgFront
SetDrawEnv linefgc= (65535,65535,0),fillpat= 0,xcoord= top,ycoord= left, save
DrawRect 63.5,79.5,140.5,191.5
DrawRRect 61.5,206.5,141.5,280.5
SetDrawEnv fillpat= -1
DrawOval 80.5,169.5,126.5,226.5
ImageGenerateROIMask jack
NewImage M_ROIMask
AutoPositionWindow/E
```

### *See Also* {#see-also}
[Image Processing](/igorpro/analysis/image-processing.md)