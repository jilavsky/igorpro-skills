---
description: "ImageLineProfile samples the source image (srcWave) along an arbitrary path described by the pair of waves: xWave and yWave."
slug: /commands/imagelineprofile
---

<div className="command-signature">

## <strong>ImageLineProfile</strong>   [/P=<em>plane</em> /S/SC/V] <em>xWave</em>=<em>xwave</em>, <em>yWave</em>=<em>ywave</em>, <em>srcwave</em>=<em>srcwave</em> [, <em>width</em>=<em>value</em>, <em>widthWave</em>=<em>wWave</em> ] {#imagelineprofile}

</div>

ImageLineProfile samples the source image (*srcWave*) along an arbitrary path described by the pair of  waves: *xWave* and *yWave*. The resulting profile is saved in the wave W_ImageLineProfile. Other waves may be created depending on flags.

### *Parameters* {#parameters}
*keyword* is one of the following names:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">srcwave = *srcwave*</span> | Specify the image for which the line profile is evaluated. The image may be a 2D or 3D numeric wave or RGB data. |
| <span class="table-cell-nowrap">xWave = *xwave*</span> | Specifies the wave containing the x-coordinates of the line segments along the path. |
| <span class="table-cell-nowrap">yWave = *ywave*</span> | Specifies the wave containing the y-oordinates of the line segments along the path. |
| <span class="table-cell-nowrap">width = *value*</span> | Provides a non-negative width (diameter) in pixels (does not have to be an integer value) in a direction perpendicular to the path over which the data is interpolated and averaged for each path point. By default, width=0 and only the interpolated value at the path point is used.  If width>0 and *srcWave* has non-default scaling, you may need to scale the width accordingly. |
| <span class="table-cell-nowrap">widthWave = *wWave*</span> | Specifies the width of the profile (see definition above) on a segment by segment basis. *wWave* should be a 1D wave that has the same number of entries as xWave and yWave. If you provide a widthWave any value assigned with the width keyword is ignored. All values in the wave must be finite and nonnegative. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSRI = *destIW*</span> | When performing radial calculations (see /RAD below), you can use this flag to specify the destination of integrated annulus segments. If this flag is not specified, the operation saves the data in W_radIntegral in the current data folder. |
|  | The /DSRI flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSSV = *destStdv*</span> | When the profile is calculated by averaging samples over width>0 and /S is used, ImageLineProfile saves the standard deviation of the samples at every profile point in *destStdv*. If this flag is not specified, the operation saves the data in the wave W_LineProfileStdv or M_LineProfileStdv in the current data folder. |
|  | The /DSSV flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTL = *destLW*</span> | Use this flag to specify the destination of the displacement wave. If you do not specify this flag, ImageLineProfile saves the data in the wave W_LineProfileDisplacement in the current data folder. |
|  | The /DSTL flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTP = *destPW*</span> | Use this flag to specify the destination of the sampled profile. If this flag is not specified, the operation saves the profile in the wave W_ImageLineProfile or M_ImageLineProfile in the current data folder. |
|  | The /DSTP flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTX = *destXW*</span> | Use this flag to specify the destination of the path profile x-component. This wave is typically different from the specified xWave because the operation computes intermediate samples along each line segment in xWave and yWave. If this flag is not specified, the operation saves the data in the wave W_LineProfileX in the current data folder. |
|  | The /DSTX flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTY = *destYW*</span> | Use this flag to specify the destination of the path profile y-component. This wave is typically different from the specified yWave because the operation computes intermediate samples for each line segment in xWave and yWave. If this flag is not specified, the operation saves the data in the wave W_LineProfileY in the current data folder. |
|  | The /DSTY flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all destination waves as a free waves. |
|  | /FREE is allowed only in functions and only if the destination wave specified is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/IRAD = *nRadIntervals*</span> |  |
|  | Use /IRAD to estimate the integrated intensity for an annular domain defined by the /RAD flag and the width parameter. For example, to integrate the intensity in the annular domain centered around *Xc*=50, *Yc*=50 for the radial range [24,25]: |
|  | <code class="igor">Make/O/N=(100,100) ddd=sqrt((x-50)^2+(y-50)^2)&#10;ImagelineProfile/RAD={50,50,24.5,0.5,0.001}/IRAD=100 srcWave=ddd&#10;Print V_integral,2*pi*(25^3-24^3)/3		// compare with exact.</code> |
|  | /IRAD was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/P = *plane*</span> | Specifies which plane (layer) of a 3D wave is to be profiled. By default *plane* =-1 and the profiles are of either the single layer of a 2D wave or all three layers of a 3D RGB wave. Use *plane* =-2 if you want to profile all layers of a 3D wave. |
| <span class="table-cell-nowrap">/RAD = {*Xc*, *Yc*, *RADc*, *radWidth* [, *deltaAngle*]}</span> |  |
|  | Use /RAD to compute a circular profile that is centered at (*Xc*,*Yc*) with a radius *RADc*. *Xc*, *Yc*, and *RADc* are expressed in terms of the scaled coordinates. |
|  | *radWidth* is in units of image pixels. |
|  | *deltaAngle* is the angle increment between samples in radians. If you omit it, the operation first computes the maximum radius (if width>0) and then computes the increment angle such that there are 5 (linearly interpolated) samples per path pixel.  If your image data is relatively smooth, you could reduce this sampling by specifying a large *deltaAngle*. |
|  | Here is an example using /RAD: |
|  | <code class="igor">Make/O/N=(100,100) ddd=x*y			// Default scaling&#10;ImagelineProfile/RAD={50,50,24.5,0} srcWave=ddd&#10;Display W_ImageLineProfile</code> |
|  | /RAD was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/S</span> | Calculate a standard deviation for each profile point. Also requires that width>0. |
| <span class="table-cell-nowrap">/SC</span> | Saves W_LineProfileX and W_LineProfileY using the X and Y scaling of *srcWave*. |
| <span class="table-cell-nowrap">/V</span> | Calculate profile points only at the vertices of xWave and yWave. Note that this flag is not compatible with radial calculations. |

### *Examples* {#examples}

```igor
Make/N=(50, 50) sampleData
sampleData = sin((x-25) / 10) * cos((y-25) / 10)
NewImage sampleData
Make/n=2 xTrace={0,50} ,yTrace={20,20}
ImageLineProfile srcWave=sampleData, xWave=xTrace, yWave=yTrace
AppendtoGraph/T yTrace vs xTrace
Display W_ImageLineProfile
```

### *Details* {#details}
ImageLineProfile computes the sampling of a *srcWave* along an arbitrary path specified by the pair of waves: *xWave* and *yWave*. The arbitrary path is made of line segments between every two consecutive vertices of *xWave* and *yWave*. The profile in each segment is calculated at a number of points (profile points) similar to the sampling density of the original image (unless the /V flag is used). Both *xWave* and *yWave* should be real numeric waves and have the same scaling as *srcWave*. If *srcWave* does not have the identical scaling in both dimensions you should set it to default scaling in order to compute a meaningful profile.

At each profile point the profile value is calculated by averaging samples along the normal to the path line segments. The operation averages the interpolated values at N equidistant points on the normal to path line segment, where N=2(width+0.5) and width is taken from the corresponding keyword or from widthWave. If samples extend outside the domain of the source image they do not contribute to the profile value.

Profile values are stored in the wave W_ImageLineProfile (/DSTP). The actual locations of the profile points are stored in the waves W_LineProfileX and W_LineProfileY (see also /DSTX and /DSTY). The scaled distance measured along the path is stored in the wave W_LineProfileDisplacement (/DSTL).

When the averaging width is greater than zero, the operation can also calculate the standard deviation of the values sampled for each profile point (see /S flag ). The results are then stored in the wave W_LineProfileStdv (/DSSV). When using this operation on 3D RGB images, the profile values are stored by default in the 3 column waves M_ImageLineProfile and M_LineProfileStdv respectively.

Radial profiles and annular calculations are supported by the /RAD flag. In this case, the path is generated internally using:

```igor
x = Xc + RADc * cos(pointIndex * deltaAngle)
y = Yc + RADc * sin(pointIndex * deltaAngle)
```

If you also use the /IRAD flag, the operation computes the integral of *srcWave* in the annulus defined by /RAD. The wave W_radIntegral (/DSRI) contains for every profile point the integral of srcWave in the segment of the annulus between the angle pointIndex\**deltaAngle* to (pointIndex+1)\**deltaAngle*. The full integral is stored in V_integral or can be computed by evaluating sum(W_radIntegral).

ImageLineProfile sets the variable V_Flag to zero when successful or to the error code returned by the operation.

### *See Also* {#see-also}
[Image Processing](/igorpro/analysis/image-processing.md)