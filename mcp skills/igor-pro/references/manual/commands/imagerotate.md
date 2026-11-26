---
description: "Rotates the image clockwise by angle (degrees) or counter-clockwise if /W is used."
slug: /commands/imagerotate
---

<div className="command-signature">

## <strong>ImageRotate</strong>  [<em>flags</em>] <em>ImageMatrix</em> {#imagerotate}

</div>

Rotates the image clockwise by *angle* (degrees) or counter-clockwise if /W is used.

The resulting image is saved in the wave M_RotatedImage unless the /O flag is specified. The size of the resulting image depends on the angle of rotation.

The portions of the image corresponding to points outside the domain of the original image are set to the default value 64 or the value specified by the /E flag.

You can apply ImageRotate to 2D and 3D waves of any data type.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *angle*</span> | Use this flag to specify the rotation angle measured in degrees in the counter-clockwise direction. For rotations by exactly 90 degrees use /C or /W instead. |
| <span class="table-cell-nowrap">/C</span> | Specifies a counter-clockwise rotation by 90 degrees. |
| <span class="table-cell-nowrap">/DEST = *destW*</span> | Use this flag to designate the output wave containing the rotated image. By default ImageRotate saves the output in the wave M_RotatedImage in the current data folder. |
|  | The /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/E = *val*</span> | Use this flag to specify the value for the pixels that are outside the domain of the original image. By default pixels are set to 64. If you specify /E=(NaN) and your data is of type char, short or long, the operation sets the external values to 64. |
| <span class="table-cell-nowrap">/F</span> | Rotates the image by 180 degrees. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destW* as a free wave. |
|  | /FREE is allowed only in functions and only if the destination wave names are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/H</span> | Flip the image horizontally. |
| <span class="table-cell-nowrap">/O</span> | Overwrite the original image with the rotated image. |
| <span class="table-cell-nowrap">/Q</span> | Quiet mode.  Without this flag the operation writes warnings in the history area. |
| <span class="table-cell-nowrap">/RGBA = (R,G,B [,A])</span> |  |
|  | Specifies the RGB or RGBA values of pixels that lie outside the domain occupied by the original image. This flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/S</span> | Uses wave scaling of the source image to preserve scaling and relative locations of objects in the image for rotation angles that are multiples of 90 degrees. |
| <span class="table-cell-nowrap">/V</span> | Flip the image vertically. |
| <span class="table-cell-nowrap">/W</span> | Specifies a clockwise rotation by 90 degrees. |
| <span class="table-cell-nowrap">/Z</span> | Ignore errors. |

### *See Also* {#see-also}
[Image Processing](/igorpro/analysis/image-processing.md)

[MatrixTranspose](/igorpro/commands/matrixtranspose.md)