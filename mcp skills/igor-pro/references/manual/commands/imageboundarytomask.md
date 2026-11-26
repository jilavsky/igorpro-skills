---
description: "The ImageBoundaryToMask operation scan-converts a pair of x,y waves into an ROI mask wave."
slug: /commands/imageboundarytomask
---

<div className="command-signature">

## <strong>ImageBoundaryToMask</strong>  <em>width</em>=<em>w</em>, <em>height</em>=<em>h</em>, <em>xwave</em>=<em>xwavename</em>, <em>ywave</em>=<em>ywavename</em>  [, <em>scalingWave</em>=<em>scalingWaveName</em>,  [<em>seedX</em>=<em>xVal</em>, <em>seedY</em>=<em>yVal</em> ]] {#imageboundarytomask}

</div>

The ImageBoundaryToMask operation scan-converts a pair of x,y waves into an ROI mask wave.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">width = *w*</span> | Specifies the mask width in pixels. |
| <span class="table-cell-nowrap">height = *h*</span> | Specifies the mask height in pixels. |
| <span class="table-cell-nowrap">xwave = *xwavename*</span> | Name of x wave for mask region. |
| <span class="table-cell-nowrap">ywave = *ywavename*</span> | Name of y wave for mask region. |
| <span class="table-cell-nowrap">scalingWave = *scalingWaveName*</span> |  |
|  | 2D or a 3D wave that provides scaling for the created mask. If specified, the scaling of the first two dimensions of scalingWave are copied to M_ROIMask, and both the x and y waves are assumed to describe pixels in the scaled domain. |
| <span class="table-cell-nowrap">seedX = *xVal*</span> | Specifies seed pixel location. The operation fills the region defined by the seed and the boundary with the value 1. Background pixels are set to zero. Requires seedY. |
| <span class="table-cell-nowrap">seedY = *yVal*</span> | Specifies seed pixel location. The operation fills the region defined by the seed and the boundary with the value 1. Background pixels are set to zero. Requires seedX. |

### *Details* {#details}
ImageBoundaryToMask generates a 2D unsigned char mask wave of dimensions specified by the keywords width and height.  If the output destination is not specified (see /DEST below), ImageBoundaryToMask saves the mask wave M_ROIMask in the current data folder.  The mask wave consists of background pixels that are set to 0 and mask pixels that are set to 1.

The x and y waves can be of any type. However, if the waves describe disjoint regions there must be at least one NaN entry in each wave corresponding to the discontinuity, which requires that you use either single or double precision waves. The values stored in the waves must correspond to zero-based integer pixel values.

If the x and y waves include a vertex that lies outside the mask rectangle, the offending vertex is moved to the boundary before the associated line segment is scan converted.

If you want to obtain a true ROI mask in which closed regions are filled, you can specify the seedX and seedY keywords.  The ROI mask is set with zero outside the boundary of the domain and 1 everywhere inside the domain.

### *Examples* {#examples}

```igor
Make/O/N=(100,200) src=gnoise(5)        // create a test image
SetScale/P x 500,1,"", src;DelayUpdate  // give it some funny scaling
SetScale/P y 600,1,"", src
Display; AppendImage src
Make/O/N=201 xxx,yyy                    // create boundary waves	
xxx=550+25*sin(p*pi/100)                // representing a close ellipse
yyy=700+35*cos(p*pi/100)
AppendToGraph yyy vs xxx
```

Now create a mask from the ellipse and scale it so that it will be appropriate for src:


```igor
ImageBoundaryToMask ywave=yyy,xwave=xxx,width=100,height=200,scalingwave=src
```

To generate an ROI masked filled with 1 in a region defined by a seed value and the boundary curves:


```igor
ImageBoundaryToMask ywave=yyy, xwave=xxx,width=100,height=200,scalingwave=src,seedx=550,seedy=700
```

### *See Also* {#see-also}
[ImageAnalyzeParticles](/igorpro/commands/imageanalyzeparticles.md), [ImageSeedFill](/igorpro/commands/imageseedfill.md)

[Image Processing](/igorpro/analysis/image-processing.md)