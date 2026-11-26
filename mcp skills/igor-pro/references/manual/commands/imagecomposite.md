---
description: "The ImageComposite operation creates a new image by combining srcImageA and srcImageB subject to one of 12 Porter-Duff compositing modes."
slug: /commands/imagecomposite
---

<div className="command-signature">

## <strong>ImageComposite</strong>  [/Z /FREE /DEST=<em>destWave</em>] <em>srcImageA</em>, <em>srcImageB</em> {#imagecomposite}

</div>

The ImageComposite operation creates a new image by combining *srcImageA* and *srcImageB* subject to one of 12 Porter-Duff compositing modes.

The ImageComposite operation was added in Igor Pro 8.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/AALP = *aWave*</span> | Specifies a 2D single-precision wave as the alpha associated with *srcImageA*. Alpha values are in the range 0 (transparent) to 1 (opaque). |
| <span class="table-cell-nowrap">/ACON = *a1*</span> | Specifies a single alpha value for the whole *srcImageA.* *a1* is in the range 0 (transparent) to 1 (opaque). |
| <span class="table-cell-nowrap">/BALP = *aWave*</span> | Specifies a 2D single-precision wave as the alpha associated with *srcImageB*. Alpha values are in the range 0 (transparent) to 1 (opaque). |
| <span class="table-cell-nowrap">/BCON = *a1*</span> | Specifies a single alpha value for the whole *srcImageB.* *a1* is in the range 0 (transparent) to 1 (opaque). |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the wave to hold the composite image. If you omit /DEST the operation stores the image in the wave M_ImageComposite in the current data folder. |
| <span class="table-cell-nowrap">/FREE</span> | Creates output wave as free waves. |
|  | /FREE is permitted in user-defined functions only, not from the command line or in macros. |
|  | If you use /FREE then *destWave* must be simple name, not a path. |
| <span class="table-cell-nowrap">/NMOD = *mode*</span> | Selects one of the 12 Porter-Duff compositing modes. *mode* is a value from 1 to 12. The default is *mode*=4 corresponding to "A over B". See ***Compositing Modes*** below. |
| <span class="table-cell-nowrap">/OUT = *layers*</span> | Specifies the number of layers of the output image. Valid values are 3 (RGB) or 4 (RGBA). By default the operation creates an RGB image. |
| <span class="table-cell-nowrap">/PMA = *pmState*</span> | Set *pmState* to 1 if the RGB components in *srcImageA* are pre-multiplied. Use *pmState*=0 otherwise. By default *srcImageA* is assumed to be pre-multiplied. See ***Pre-multiplication*** below. |
| <span class="table-cell-nowrap">/PMB = *pmState*</span> | Set *pmState* to 1 if the RGB components in *srcImageB* are pre-multiplied. Use *pmState*=0 otherwise. By default *srcImageB* is assumed to be pre-multiplied. See ***Pre-multiplication*** below. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. The operation sets V_Flag to 0 if it succeeds or to an error code otherwise. You can use [GetErrMessage](/igorpro/commands/geterrmessage.md) to obtain a description of the error. |

### *Pre-multiplication* {#pre-multiplication}
An RGB value can be raw or pre-multiplied. "Pre-multiplied" means that the red, green, and blue values have been multiplied by normalized alpha values in the range 0 (transparent) to 1 (opaque). ImageComposite operation is faster when working with pre-multiplicated values. ImageComposite assumes that your RGB values are pre-multiplied unless you specify otherwise using /PMA=0 and /PMB=0.

### *Compositing Modes* {#compositing-modes}
Here are the 12 compositing modes supported by ImageComposite:

<img src="Images/ImageComposite/ImageComposite_0.png" width="50%"/>

### *Details* {#details}
ImageComposite computes an output RGB or RGBA image that result from compositing *srcImageA* and *srcImageB* using one of the Porter-Duff compositing modes shown in the table above. The waves *srcImageA* and *srcImageB* must have the same number of pixels and the same number type.

Supported number types are: unsigned char, unsigned short, unsigned int, single precision floating point and double precision floating point. When using integer waves expected alpha values are in the range [0,2^N-1] where N is the number of bits of the number type. Floating point waves should include alpha in the range [0,1].

There are three options to specify the alpha associated with each image:


1. The alpha can be expressed as the 4th layer in the wave.


2. The alpha can be specified by a single-precision wave that has the same number of pixels as the image using the /AALP and /BALP flags.


3. The alpha can be specified by a single number in the range [0,1] using the /ACON and /BCON flags.

	Options 2 and 3 cannot override an alpha channel that is present in a source wave. To use these options you must delete the alpha channel in the source wave, if any.

### *Example* {#example}

```igor
Function SetupImageCompositeDemo()          // Setup - Create two sample images 
	Make/O/N=(128,128,4)/B/U imageA=0, imageB=0
	imageA[0,64][][0]=255
	imageA[0,64][][3]=128
	NewImage/S=0/N=imageAW imageA
	imageB[][0,64][1]=255
	imageB[][0,64][3]=128
	NewImage/S=0/N=imageBW imageB
	AutoPositionWindow/M=0/R=imageAW imageBW
End
Function CompositeAOverB()					// Composite A over B
	Wave imageA, imageB
	ImageComposite/PMA=0/PMB=0/DEST=M_Comp1/NMOD=4 imageA,imageB
	NewImage/S=0/N=comp1 M_Comp1
	AutoPositionWindow/M=0/R=imageBW 
End
Function CompositeAInB()					// Composite A in B
	Wave imageA, imageB
	ImageComposite/PMA=0/PMB=0/DEST=M_Comp2/NMOD=6 imageA,imageB
	NewImage/S=0/N=comp2 M_Comp2
	AutoPositionWindow/M=0/R=comp1 
End
Function RemoveAlphaChannel()				// Remove the alpha channel from imageA
	Wave imageA
	Duplicate/R=[][][0,2] imageA, imageA_rgb
	NewImage/S=0 imageA_rgb
End
```

### *References* {#references}
T. Porter & T. Duff - Compositing Digital Images. Computer Graphics Volume 18, Number 3, July 1984 pp 253-259.

### *See Also* {#see-also}
[ImageBlend](/igorpro/commands/imageblend.md), [Image Processing](/igorpro/analysis/image-processing.md)