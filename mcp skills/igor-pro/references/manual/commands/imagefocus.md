---
description: "The ImageFocus operation creates in focus image(s) from a stack of images that contain in and out of focus regions."
slug: /commands/imagefocus
---

<div className="command-signature">

## <strong>ImageFocus</strong>  [/ED=<em>edepth</em> /METH=<em>method</em> /Q/Z] <em>stackWave</em> {#imagefocus}

</div>

The ImageFocus operation creates in focus image(s) from a stack of images that contain in and out of focus regions. It computes the variance in a small neighborhood around each pixel and then takes the pixel value from the plane in which the highest variance is found. The computed 2D in-focus image is saved in the wave M_ImageFocus in the current data folder or in the wave specified by the /DEST flag.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
| Specifies the output wave. |  |
|  | It is an error to specify the same wave as both *stackWave* and *destWave*. |
|  | When used in a function, ImageFocus creates a real wave reference for the *destWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/ED = *edepth*</span> | Sets the effective depth in planes. For example, an effective depth of one means that it computes the best focus for each plane using a stack of three planes, which includes the current plane and any one adjacent plane above and below it. Does not affect the default method (/METH=0). |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/METH = *method*</span> | Specifies the calculation method. |
|  |<table class="nested-table"><tbody><tr><td>*method*&nbsp;=0:</td><td>Computes a single plane output for the stack (default).</td></tr><tr><td>*method*&nbsp;=1:</td><td>Computes the best image for each plane using /ED.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Q</span> | Quiet mode; no output to history area. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *See Also* {#see-also}
[Image Processing](/igorpro/analysis/image-processing.md)