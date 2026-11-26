---
description: "The ImageInterpolate operation interpolates the source srcWave and stores the results in the wave M_InterpolatedImage in the current data folder unless you…"
slug: /commands/imageinterpolate
---

<div className="command-signature">

## <strong>ImageInterpolate</strong>  [ <em>flags</em> ] <em>Method</em>  <em>srcWave</em> {#imageinterpolate}

</div>

The ImageInterpolate operation interpolates the source *srcWave* and stores the results in the wave M_InterpolatedImage in the current data folder unless you specify a different destination wave using the /DEST flag.

### *Parameters* {#parameters}
*Method* selects type of interpolation; it is one of the following names:


|  |  |
| --- | --- |
| Affine2D | Performs an affine transformation on *srcWave* using parameters specified by the /APRM flag. The transformation applies to a general combination of rotation, scaling, and translation represented by a 3x3 matrix |
|  | $$ \displaystyle M=\left[\begin{array}{ccc} r_{11} & r_{12} & t_{x} \\ r_{21} & r_{22} & t_{y} \\ 0 & 0 & w \end{array}\right] . $$ |
|  | The upper 2x2 matrix is a composite of rotation and scaling, *tx* and *ty* are composite translations and *w* is usually 1. It computes the dimensions of the output wave and then uses the inverse transformation and bilinear interpolation to compute the value of each output pixel. When an output pixel does not map back into the source domain it is set to the user-specified background value. It supports 2D and 3D input waves. If *srcWave* is a 3D wave it applies on a layer by layer basis. |
|  | The output is stored in the wave M_Affine in the current data folder or in the wave specified by /DEST flag. |
| Bilinear | Performs a bilinear interpolation subject to the specified flag. You can use either the /F or /S flag, but not both. |
| Kriging | Uses Kriging to generate an interpolated matrix from a sparse data set. Kriging calculates interpolated values for a rectangular domain specified by the /S flag. The Kriging parameters are specified via the /K flag. |
|  | Kriging is computed globally for a single user-selected variogram model. If there are significant spatial variances within the domain occupied by the data, you should consider subdividing the domain along natural boundaries and use a single variogram model in each subdivision. |
|  | If there are N data points, the algorithm first computes the NxN matrix containing the distances between the data and then inverts an associated matrix of similar size to compute the result for the selected variogram model. Because inversion of an NxN matrix can be computationally expensive, you should consider restricting the calculation to regions that are similar to the range implied by the variogram. Such an approach can also be justified in the sense that the local interpolation should not be affected by a remote datum. |
|  | <div><Admonition type="note"><p>Kriging does not support data containing NaNs or INFs. Wave scaling has no effect on kriging calculations.</p></Admonition></div> |
| Pixelate | Creates a lower resolution (pixelated) version of *srcWave* by averaging the pixels inside domain specified by /PXSZ flag. The results are saved in the wave M_PixelatedImage in the current data folder. |
|  | The computed wave has the same numeric type as *srcWave* so the averaging may be inaccurate in the case of integer waves. |
|  | When srcWave is a 3D wave you have the option of averaging only over data in each layer using /PXSZ={nx,ny} or averaging over data in a rectangular cube using /PXSZ={nx,ny,nz}. |
|  | When not averaging over layers, the number of rows and columns of the new image are obtained by integer division of the original number by the respective size of the averaging rectangle and adding one more pixel for any remainder. |
|  | When averaging over layers the resulting rows and columns are obtained by truncated integer division ignoring remainders (if any). |
|  | See also [Multidimensional Decimation](/igorpro/igor-basics/multidimensional-waves.md#multidimensional-decimation). |
| Resample | Computes a new image based on the selected interpolation function and transformation parameters. Set the interpolation function with the /FUNC flag. Use the /TRNS flag to specify transformation parameters for grayscale images, or /TRNR, /TRNG, and /TRNB for the red, green, and blue components, respectively, of RGB images. M_InterpolatedImage contains the output image in the current data folder. |
|  | There are currently two transformation functions: the first magnifies an image and the second applies a radial polynomial sampling. The radial polynomial affects pixels based on their position relative to the image center. A linear polynomial reproduces the same image. Any nonlinear terms contribute to distortion (or correction thereof). |
| Spline | Computes a 2D spline interpolation for 2D matrix data. The degree of the spline is specified by the /D flag. |
| Voronoi | Generates an interpolated matrix from a sparse data set (*srcWave* must be a triplet wave) using Voronoi polygons. It calculates interpolated values for a rectangular domain as specified by the /S or /RESL flags. |
|  | It first computes the Delaunay triangulation of X, Y locations in the Z=0 plane (assuming that X, Y positions occupy a convex domain in the plane). It then uses the Voronoi dual to interpolate the Z values for X and Y pairs from the grid defined by the /S flag. The computed grid may exceed the bounds of the convex domain defined by the triangulation. Interpolated values for points outside the convex domain are set to NaN or the value specified by the /E flag. |
|  | Use the /I flag to iterate to finer triangulation by subdividing the original triangles into smaller domains. Each iteration increases computation time by approximately a factor of two, but improves the smoothness of the interpolation. |
|  | If you have multiple sets of data in which X,Y locations are unchanged, you can use the /STW flag to store one triangulation and then use the /PTW flag to apply the precomputed triangulation to a new interpolation. To use this option you should use the Voronoi keyword first with a triplet wave for *srcWave* and set xn = x0 and yn = y0. The operation creates the wave W_TriangulationData that you use in the next triangulation with a 1D wave as *srcWave*. |
|  | Voronoi interpolation is similar to what can be accomplished with the [ContourZ](/igorpro/commands/contourz.md) function except that it does not require an existing contour plot, it computes the whole output matrix in one call, and it has the option of controlling the subdivision iterations. |
|  | See ***Voronoi Interpolation Example*** below. |
| XYWaves | Performs bilinear interpolation on a matrix scaled using two X and Y 1D waves (specified by /W). The interpolation range is defined by /S. The data domain is defined between the centers of the first and last pixels (X in this example): |
|  | xmin=(*xWave*[0]+*xWave*[1])/2 |
|  | xmax=(*xWave*[last]+*xWave*[last-1])/2 |
|  | Values outside the domain of the data are set to NaN. The interpolation is contained in the M_InterpolatedImage wave, which is single precision floating point or double precision if *srcWave* is double precision. |
| Warp | Performs image warping interpolation using a two step algorithm with three optional interpolation methods. The operation warps the image based on the relative positions of source and destination grids. The warped image has the same size as the source image. The source and destination grids are each specified by a pair of 2D X and Y waves where the rows and columns correspond to the relative location of the source grid. The smallest supported dimensions of grid waves are 2x2. All grid waves must be double-precision floating point and must have the same number of points corresponding to pixel positions within the image. Grid waves must not contain NaNs or INFs. Wave scaling is ignored. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/APRM = {*r11,r12,tx,r21,r22,ty,w,background* }</span> |  |
|  | Sets elements of the affine transformation matrix and the background value. |
| <span class="table-cell-nowrap">/ATOL</span> | Allows ImageInterpolate to use a tolerance value if the result of the interpolation at any point is a NaN. The algorithm returns the first non-NaN value it finds by adding or subtracting 1/10000th of the size of the X or Y interpolation step. At worst this algorithm is 5 times slower than the default algorithm if the interpolation is performed in a region which is completely outside the convex source domain. |
|  | /ATOL was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/CMSH</span> | Use this flag in Voronoi interpolation to create a triangle mesh surface representing the input data. After triangulating the X, Y locations (in a plane z=const), the mesh is generated from a sequence of XYZ vertices of all the resulting triangles. The output is stored in the wave M_ScatterMesh in the current data folder. It is in the form of a triplet wave where every consecutive 3 rows represent a disjoint triangle. |
|  | If the input contains a NaN or INF in any column, the corresponding row is excluded from the triangulation. |
|  | If you want to generate this mesh without generating the interpolated matrix you can omit the /S flag. |
|  | /CMSH was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/CSAF = *factor*</span> | In rare situations that usually involve spatial degeneracy, the Voronoi interpolation algorithm may need additional memory. You can use the /CSAF flag with an integer *factor* greater than 1 to increase the memory allocation. |
|  | /CSAF was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/D = *splineDeg*</span> | Specifies the spline degree with the Spline method. The default spline degree is 2. Supported values are 2, 3, 4, and 5. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the wave to contain the output of the operation. If the specified wave already exists, it is overwritten. |
|  | Creates by default a real wave reference for the destination wave in a user function. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/DSTC = *destCWave*</span> |  |
|  | Specifies the output wave for the circumcircle data in the Delaunay triangulation (Voronoi interpolation /SV). If /DSTC is not specified, the output is stored in the wave M_Circles in the current data folder. |
|  | When used in a function, ImageInterpolate creates a real wave reference for *destCWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DSTC flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTD = *destDWave*</span> |  |
|  | Specifies the output wave for the Delaunay triangulation (Voronoi interpolation /SV). If this flag is not used, the operation stores the histogram in the wave M_DelaunayTriangles in the current data folder. |
|  | When used in a function, ImageInterpolate creates a real wave reference for *destDWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DSTD flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTE = *destEWave*</span> |  |
|  | Specifies the output wave for the Voronoi edges  (Voronoi interpolation /SV). If this flag is not used, the operation stores the histogram in the wave M_VoronoiEdges in the current data folder. |
|  | When used in a function, ImageHistogram creates a real wave reference for *destEWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DSTE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTM = *destMWave*</span> |  |
|  | Specifies the output wave for an scatter mesh data (/CMSH). If this flag is not used, the operation stores the histogram in the wave M_ScatterMesh in the current data folder. |
|  | When used in a function, ImageInterpolate creates a real wave reference for *destMWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | /DSTM flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTT = *destTWave*</span> |  |
|  | Specifies the output wave for the saved triangulation data (/STW). If this flag is not used, the operation stores the histogram in the wave W_TriangulationData in the current data folder. |
|  | When used in a function, ImageInterpolate creates a real wave reference for *destTWave*. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/E = *outerValue*</span> | Assigns *outerValue* to all points outside the convex domain of the Delaunay triangulation. By default *outerValue* = NaN. |
| <span class="table-cell-nowrap">/F = {*fx*,*fy* }</span> | Bilinear interpolation of all the source data. Here *fx* is the sampling factor for the X-direction and *fy* is the sampling factor in the Y-direction. The output number of points in a dimension is factor\*(number of data intervals) +1. The number of data intervals is one less than the number of points in that dimension. |
|  | For example, if *srcWave* is a 2x2 matrix (you have a single data interval in each direction) and you use /F={2,2}, then the output wave is a 3x3 matrix (i.e., 2x2 intervals) which is a factor of 2 of the input. Sampling factors can be noninteger values. |
| <span class="table-cell-nowrap">/FDS</span> | Performs spline interpolation to a "local" cubic spline that depends only on the 2D neighboring data. The interpolation goes exactly through the original data and provides continuity of the function and its first derivative. The second derivative is set to vanish on the boundary. The implemented algorithm was provided by Francis Dalaudier. /FDS was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/FEQS</span> | When performing Voronoi interpolation, forces the algorithm to use equal scaling for both axes. Normally the scaling for each axis is determined from its range. When the ranges of the two axes are different by an order of magnitude or more, it is helpful to force the larger range to be used for scaling both axes. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all destination waves as free waves. |
|  | /FREE is allowed only in functions and only if the destination waves consist of a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FUNC = *funcName*</span> |  |
|  | Specifies the interpolation function. *funcName* can be: |
|  |<table class="nested-table"><tbody><tr><td>nn</td><td>Nearest neighbor interpolation uses the value of the nearest neighbor without interpolation. This is the fastest function.</td></tr><tr><td>bilinear</td><td>Bilinear interpolation uses the immediately surrounding pixels and computes a linear interpolation in each dimension. This is the second fastest function.</td></tr><tr><td>cubic</td><td>Cubic polynomial (photoshop-like) uses a 4x4 neighborhood value to compute the sampled pixel value.</td></tr><tr><td>spline</td><td>Spline smoothed sampled value uses a 4x4 neighborhood around the pixel.</td></tr><tr><td>sinc</td><td>Slowest function using a 16x16 neighborhood.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/I = *iterations*</span> | Specifies the number of times the original triangulation is subdivided with the Voronoi interpolation method. By default the Voronoi interpolation computes the original triangulation without subdivision. |
| <span class="table-cell-nowrap">/K = {*model*, *nugget*, *sill*, *range* }</span> |  |
|  | Specifies the variogram parameters for kriging using standard notation, models are expressed in terms of the nugget value *C*<sub>0</sub>, sill value *C*<sub>0</sub>*+C*<sub>1</sub>, and range *a*. |
|  | <img src="Images/ImageInterpolate/ImageInterpolate_1.png" width="100%"/> |
|  |<table class="nested-table"><tbody><tr><td>*model*</td><td>Selects the variogram model.</td></tr><tr><td></td><td>=1:    Spherical.  *γ* (*h*)= *C*<sub>0</sub><sub> </sub>+*C*<sub>1</sub>*(*3h* /2a -0.*5* **h* ^*3* /*a* ^*3* )</td></tr><tr><td></td><td>=2:    Exponential. *γ* (*h* )= *C*<sub>0</sub><sub> </sub>+*C*<sub>1</sub>*(1-*exp* [-*3* * *h* /*a* ])</td></tr><tr><td></td><td>=3:    Gaussian. *γ* (*h* )= *C*<sub>0</sub><sub> </sub>+*C*<sub>1</sub><sub> </sub>*(1-*exp* [-*3* *(*h* /*a* )^*2* ])</td></tr><tr><td>*nugget*</td><td>Specifies the lowest value in the variogram.</td></tr><tr><td>*sill*</td><td>Specifies the maximum (plateau) value in the variogram range the characteristic length of the different variogram models.</td></tr></tbody></table>
|  | Wave scaling has no effect on kriging calculations. |
| <span class="table-cell-nowrap">/PFTL = *tol*</span> | In Voronoi interpolation, controls the rectangular neighborhood about each datum position XY where the algorithm returns the original Z-value. The tolerance value 0<=*tol* <1 is tested separately in X and Y (i.e., it is not a geometric distance) when both X and Y are normalized to the range [0,1]. By default *tol* =1e-15. |
|  | Added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/PTW = *tWave*</span> | Uses a previous triangulation wave with Voronoi interpolation. *tWave* will be the wave saved by the /STW flag. You can't use a triangulation wave that was computed and saved on a different computer platform. |
|  | See the section ***PTW Flag Example*** below. |
| <span class="table-cell-nowrap">/PXSZ = {*nx*, *ny*}</span> | Specifies the size in pixels of the averaging rectangle used by the Pixelate operation. *nx* is the number of rows and *ny* is the number of columns that are averaged to yield a single output pixel. If *srcWave* is a 3D wave the resulting wave has the same number of layers as *srcWave* with pixelation computed on a layer-by-layer basis. |
| <span class="table-cell-nowrap">/PXSZ = {*nx*, *ny*, *nz*}</span> |  |
|  | Specifies the size in pixels of the averaging rectangle used by the Pixelate operation. *nx* is the number of rows and *ny* is the number of columns and *nz* is the number of layers that are averaged to yield a single output pixel. |
|  | This form of the /PXSZ flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/RESL = {*nx*, *ny*}</span> | Specifies resampling the full input image to an output image having *nx* rows by *ny* columns. |
| <span class="table-cell-nowrap">/S = {*x0*,*dx*,*xn*,*y0*,*dy*,*yn* }</span> |  |
|  | Calculates a bilinear interpolation of a subset of the source data. Here *x0* is the starting point in the X-direction, *dx* is the sampling increment, *xn* is the end point in the X-direction and the corresponding values for the Y-direction. If you set *x0* equal to *xn* the operation will compute the triangulation but not the interpolation. |
| <span class="table-cell-nowrap">/SPRT</span> | Skips the XY perturbation step. The perturbation step is designed to break degeneracies that originate when the XY data are sampled on a rectangular grid. If your data are not sampled on a rectangular grid you can skip the perturbation and get better accuracy in reproducing the Z-values at the sampled locations. See also [ModifyContour](/igorpro/commands/modifycontour.md) with the keyword Perturbation. |
|  | Added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/STW</span> | Saves the triangulation information in the wave W_TriangulationData in the current data folder. W_TriangulationData can only be used on the computer platform where it was created. |
| <span class="table-cell-nowrap">/SV</span> | Saves three waves containing triangulation data.  The Delaunay triangulation of the XY data is saved in the wave M_DelaunayTriangles in the current data folder or in the wave specified by /DSTD.  The vertices of each triangle are listed in 4 consecutive rows (the fourth row closes the triangle).  Triangles are separated from each other by a row of NaNs.  The triangulation circumcircles are stored in the wave M_Circles or in the wave specified by /DSTC. Each row in M_Circles contains the center and radius of a circle.  The sequential edges of the Voronoi polygons are stored in the 2D wave M_VoronoiEdges in the current data folder or in the wave specified by /DSTE. Edges are separated from each other by a row of NaNs. Note that the outer most polygons that define the convex hull share one or more edges with a large triangle containing all the data. |
| <span class="table-cell-nowrap">/TRNS = {*transformFunc*,*p1*,*p2*,*p3*,*p4* }</span> |  |
|  | Determines the mapping between a pixel in the destination image and the source pixel. transformFunc can be: |
|  |<table class="nested-table"><tbody><tr><td>*scaleShift*</td><td>Sets image scaling which could be anamorphic if the X and Y scaling are different.</td></tr><tr><td>*radialPoly*</td><td>Corrects both color as well as barrel and pincushion distortion. In radialPoly the mapping from a destination pixel to a source pixel is a polynomial in the pixel&#39;s radius relative to the center of the image.</td></tr><tr><td></td><td>A source pixel *sr* satisfies the equation:</td></tr><tr><td></td><td>$$ \displaystyle s r=a r+b r^{2}+c r^{3}+d r^{4}, $$</td></tr><tr><td></td><td>where *r* is the radius of a destination pixel having an origin at the center of the destination image.</td></tr></tbody></table>
|  | See the ***transformFunc Parameters*** table below for a description of the parameters accepted by the /TRNS flag. |



|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/U = *uniformScale*</span> |  |
|  | Calculates a bilinear interpolation of all the source data as with the /F flag but with two exceptions: A single uniform scale factor applies in both dimensions, and the scale factor applies to the number of points -- not the intervals of the data. |
| <span class="table-cell-nowrap">/W = {*xWave*, *yWave*}</span> |  |
|  | Provides the scaling waves for XYWaves interpolation. Both waves must be monotonic and must have one more point than the corresponding dimension in *srcWave*. The waves contain values corresponding to the edges of data points in *srcWave*, so that the X value at the first data point is equal to (*xWave*[0]+*xWave*[1])/2. |

### *transformFunc Parameters* {#transformfunc-parameters}

The following table describes the different parameter inputs accepted by the /TRNS flag:

| *transformFunc* | p1 | p2 | p3 | p4 |
| --- | --- | --- | --- | --- |
| *scaleShift* | xOffset | xScale | yOffset | yScale |
| *radialPoly* | a | b | c | d |

### *Flags for Warp* {#flags-for-warp}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/dgrx = *wave*</span> | Sets the wave containing the destination grid x data. |
| <span class="table-cell-nowrap">/dgry = *wave*</span> | Sets the wave containing the destination grid y data. |
| <span class="table-cell-nowrap">/sgrx = *wave*</span> | Sets the wave containing the source grid x data. |
| <span class="table-cell-nowrap">/sgry = *wave*</span> | Sets the wave containing the source grid y data. |
| <span class="table-cell-nowrap">/WM = *im*</span> | Sets the interpolation method for warping an image. |
|  |<table class="nested-table"><tbody><tr><td>***im***</td><td>**Method**</td></tr><tr><td>1</td><td>fast selection of original data values</td></tr><tr><td>2</td><td>linear interpolation</td></tr><tr><td>3</td><td>smoothing interpolation (slow)</td></tr></tbody></table>

### *Details* {#details}
When computing Bilinear or Spline interpolation *srcWave* can be a 2D or a 3D wave. When *srcWave* is a 3D wave the interpolation is computed on a layer by layer basis and the result is stored in a corresponding 3D wave. When the interpolation method is Kriging or Voronoi, *srcWave* is a 2D triplet wave (3-column wave) where each row specifies the X, Y, Z values of a datum. *srcWave* can be of any real data type. Results are stored in the wave M_InterpolatedImage. If *srcWave* is double precision so is M_InterpolatedImage; otherwise M_InterpolatedImage is a single precision wave.

### *Voronoi Interpolation Example* {#voronoi-interpolation-example}

```igor
Function DemoVoronoiInterpolation()
	Make/O/N=(100,3) sampleTriplet
	sampleTriplet[][0]=enoise(5)
	sampleTriplet[][1]=enoise(5)
	sampleTriplet[][2]=sqrt(sampleTriplet[p][0]^2+sampleTriplet[p][1]^2)
	
	// Interpolate the data to a rectangular grid of 50x50 pixels
	ImageInterpolate/RESL={50,50}/DEST=firstImage voronoi sampleTriplet
	
	// Triangulate the XY locations and save the triangulation wave
	ImageInterpolate/STW voronoi sampleTriplet
	
	// Use the previous triangulation on the Z column of the sample
	MatrixOp/O zData=col(sampleTriplet,2)
	Wave W_TriangulationData
	ImageInterpolate/PTW=W_TriangulationData/RESL={50,50}/DEST=secondImage voronoi zData
End
```

### *PTW Flag Example* {#ptw-flag-example}

```igor
Function DemoPTW()
	// Create some random data
	Make/O/N=(100,3) eee = enoise(5)
	
	// Compute triangulation wave
	ImageInterpolate/RESL={1,1}/STW voronoi eee
	Wave W_TriangulationData
	
	// Copy the Z-column to a 1D wave
	MatrixOp/O e3 = col(eee,2)
	
	// Use the previous triangulation with 1D wave
	ImageInterpolate/PTW=W_TriangulationData /RESL={100,100} voronoi e3
	Wave M_InterpolatedImage
	Duplicate/O M_InterpolatedImage, oneD
	
	// Direct computation for comparison
	ImageInterpolate/RESL={100,100} voronoi eee
	
	// Display
	NewImage M_InterpolatedImage
	NewImage oneD
End
```

### *References* {#references}
Unser, M., A. Aldroubi, and M. Eden, B-Spline Signal Processing: Part I-Theory, *IEEE Transactions on Signal Processing*, *41*, 821-832, 1993.

Douglas B. Smythe, "A Two-Pass Mesh Warping Algorithm for Object Transformation and Image Interpolation" ILM Technical Memo #1030, Computer Graphics Department, Lucasfilm Ltd. 1990.

### *See Also* {#see-also}
[Image Processing](/igorpro/analysis/image-processing.md)

The [interp](/igorpro/commands/interp.md), [Interp3DPath](/igorpro/commands/interp3dpath.md), [ImageRegistration](/igorpro/commands/imageregistration.md), and [Loess](/igorpro/commands/loess.md) operations. The [ContourZ](/igorpro/commands/contourz.md) function. For examples see [Interpolation and Sampling](/igorpro/analysis/image-processing.md#interpolation-and-sampling).

Use [ImageTransform](/igorpro/commands/imagetransform.md) with the keyword Voronoi to compute the Voronoi tesselation without interpolating data.

### *Demos* {#demos}
[Open WarpingDemo.pxp](#igor-pxp/Examples/Imaging/warpingDemo.pxp)