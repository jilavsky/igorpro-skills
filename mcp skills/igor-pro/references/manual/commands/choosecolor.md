---
description: "The ChooseColor operation displays a dialog for choosing a color. The color initially shown is black unless you specify a different color with /C."
slug: /commands/choosecolor
---

<div className="command-signature">

## <strong>ChooseColor</strong>  [/A[=<em>a</em>]/C=(<em>r</em>,<em>g</em>,<em>b</em>[,<em>a</em>] )] {#choosecolor}

</div>

The ChooseColor operation displays a dialog for choosing a color.

The color initially shown is black unless you specify a different color with /C.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A[ = *a* ]</span> | *a* =1 shows the alpha (opacity) channel. /A is the same as /A=1. |
|  | *a* =0 hides the alpha channel. This is the default setting. |
|  | The /A flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/C = (*r*,*g*,*b*[,*a*])</span> | Sets the color initially displayed in the dialog. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |

### *Details* {#details}
ChooseColor sets the variable V_Flag to 1 if the user clicks OK in the dialog or to 0 otherwise.

If V_Flag is 1 then V_Red, V_Green, V_Blue, and V_Alpha are set to the selected color as integers from 0 to 65535.

A fully opaque color sets V_Alpha=65535. A fully transparent color sets V_Alpha=0.

### *See Also* {#see-also}
[ImageTransform](/igorpro/commands/imagetransform.md) *rgb2hsl* and *hsl2rgb* keywords.