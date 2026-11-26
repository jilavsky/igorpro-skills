---
description: "The ImageBlend operation takes two RGB images (3D waves) in srcWaveA and srcWaveB and computes the alpha blending so that."
slug: /commands/imageblend
---

<div className="command-signature">

## <strong>ImageBlend</strong>  [/A=<em>alpha</em> /W=<em>alphaWave</em> ] <em>srcWaveA</em>, <em>srcWaveB</em>  [, <em>destWave</em> ] {#imageblend}

</div>

The ImageBlend operation takes two RGB images (3D waves) in *srcWaveA*  and *srcWaveB*  and computes the alpha blending so that

```igor
destWave = srcWaveA * (1 - alpha ) + srcWaveB * alpha
```

for each color component. As of Igor Pro 10 the optional destWave parameter is deprecated and you should use the /DEST flag to specify the output destination *destBlendW*. If you do not specify the destination, ImageBlend saves the output in the wave M_alphaBlend in the current data folder.

The source and destination waves must be of the same data types and the same dimensions. The *alphaWave*, if used, must be a single precision (SP) float wave and it must have the same number of rows and columns as the source waves.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *alpha*</span> | Specifies a single alpha value for the whole image |
| <span class="table-cell-nowrap">/DEST = *destBlendW*</span> |  |
|  | Specifies the output wave created by the operation. It is a replacement for using the optional destWave argument at the end of the command, but it also allows *destBlendW* to be a free wave. |
|  | It is an error to specify the same wave as both *srcWave* and *destWave*. |
|  | When used in a function, the ImageBlend operation by default creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DEST flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the wave *destBlendW* as a free wave. Note that /FREE does not affect the *destWave* specified by the deprecated optional last command parameter. |
|  | /FREE is allowed only in functions and only if *destBlendW* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/W = *alphaWave*</span> | Single precision wave that specifies an alpha value for each pixel. |

### *See Also* {#see-also}
[ImageComposite](/igorpro/commands/imagecomposite.md), [Image Processing](/igorpro/analysis/image-processing.md)