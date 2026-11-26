---
description: "The ImageAnalyzeParticles operation performs one of two particle analysis operations on a 2D or 3D source wave imageMatrix."
slug: /commands/imageanalyzeparticles
---

<div className="command-signature">

## <strong>ImageAnalyzeParticles</strong>   [ <em>flags</em> ] <em>keyword</em>  <em>imageMatrix</em> {#imageanalyzeparticles}

</div>

The ImageAnalyzeParticles operation performs one of two particle analysis operations on a 2D or 3D source wave *imageMatrix*. The source image wave must be binary, i.e., an unsigned char format where the particles are designated by 0 and the background by 255 (the operation will produce erroneous results if your data uses the opposite designation). Note that all nonzero values in the source image will be considered part of the background. Grayscale images must be thresholded before invoking this operation (you may need to use the /I flag with the [ImageThreshold](/igorpro/commands/imagethreshold.md) operation).

:::note
ImageAnalyzeParticles does not take into account wave scaling. All measurements are in terms of pixels and all pixels are assumed to be square.
:::

*keyword*  is one of the following names:

|  |  |
| --- | --- |
| mark | Creates a masking image for a single particle, which is specified by an internal (seed) pixel using the /L flag. The masking image is stored in the wave M_ParticleMarker, which is an unsigned char wave. All points in M_ParticleMarker are set to 64  (image operations on binary waves use the value 64 to designate the equivalent of NaN) except points in the particle which are set to the 0. This wave is designed to be used as an overlay on the original image (using the explicit=1 mode of ModifyImage). This keyword has now been superseded by [ImageSeedFill](/igorpro/commands/imageseedfill.md). |
| stats | Measures the particles in the image. Results of the measurements are reported for all particles whose area exceeds the *minArea* specified by the /A flag. The results of the measurements are: |
|  |<table class="nested-table"><tbody><tr><td>V_NumParticles</td><td>Number of particles that exceed *minArea* limit.</td></tr><tr><td>W_ImageObjArea</td><td>Area (in pixels) for each particle.</td></tr><tr><td>W_ImageObjPerimeter</td><td>Perimeter (in pixels) of each particle. The perimeter calculation involves estimates for 45-degree edges resulting in noninteger values.</td></tr><tr><td>W_circularity</td><td>Ratio of the square of the perimeter to (4\*pi\*objectArea). This value approaches 1 for a perfect circle.</td></tr><tr><td>W_rectangularity</td><td>Ratio of the area of the particle to the area of the inscribing (nonrotated) rectangle. This ratio is pi/4 for a perfect circular object and unity for a nonrotated rectangle.</td></tr><tr><td>W_SpotX&nbsp;and&nbsp;W_SpotY</td><td>Single x, y point from each object. There is one entry per particle and the entries follow the same order as all other waves created by this operation. Each (x,y) point from these waves can used to define the position of a tag/annotation for a particle. Points can also be used as seed pixels for the associated *mark* method or for the [ImageSeedFill](/igorpro/commands/imageseedfill.md) operation.</td></tr><tr><td>W_xmin,&nbsp;W_xmax,&nbsp;W_ymin,&nbsp;W_ymax</td><td>Each contains a single point for each particle defining an inscribing rectangular box with axes along the X and Y directions.</td></tr></tbody></table>
|  | One of the following four waves can be created depending on the /M specification. The waves are designed to be used as an overlay on the original image (using the explicit=1 mode of ModifyImage). |
|  | <div><Admonition type="note"><p>The additional time required to create these waves is negligible compared with the time it takes to generate the stats data.</p></Admonition></div> |
|  |<table class="nested-table"><tbody><tr><td>M_ParticlePerimeter</td><td>Masking image of particle boundaries. It is an unsigned char wave that contains 0 values for the object boundaries and 64 for all other points.</td></tr><tr><td>M_ParticleArea</td><td>Masking image of the area occupied by the particles. It is an unsigned char wave that contains 0 values for the object boundaries and 64 for all other points. It is also different from the input image in that particles smaller than the minimum size, specified by /A, are absent.</td></tr><tr><td>M_Particle</td><td>Masking image of both the area and the boundary of the particles. It is an unsigned char wave that contains the value 16 for object area, the value 18 for the object boundaries and the value 64 for all other points.</td></tr><tr><td>M_rawMoments</td><td>Five column wave. The first column is the raw sum of the x values for each particle, and the second column contains the sum of the y values. To obtain the average or &quot;center&quot; of a particle divide these values by the corresponding area. The third column contains the sum of x<sup>2</sup>, the fourth column the sum of y<sup>2</sup>, and the fifth column the sum of x*y. The entries of this wave are used in calculating a fit to an ellipse (using the /E flag).</td></tr></tbody></table>
|  | When *imageMatrix* is a 3D wave, the different results are packed into a single 2D wave M_3DParticleInfo, which consists of one row and 11 columns for each particle. Columns are arranged in the following order: minRow, maxRow, minCol, maxCol, minLayer, maxLayer, xSeed, ySeed, zSeed, volume, and area. Use Edit M_3DParticleInfo.ld to display the results in a table with dimension labels describing the different columns. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *minArea*</span> | Specify a minimum area as a threshold that must be exceeded for a particle to be counted (e.g., use *minArea*=0 to find single pixel particles). The minimum area is measured in pixels; its default value is *minArea*=5. |
|  | When the source wave is 3D, *minArea* specifies the minimum number of voxels that constitute a particle. |
|  | /A has no effect when used with the *mark* method. |
| <span class="table-cell-nowrap">/B</span> | Erases a 1 pixel wide frame inset from the boundary. This insures that no particles will have boundary pixels (see /EBPC below) and all boundary waves will describe close contours. |
| <span class="table-cell-nowrap">/CIRC = {*minCircularity*, *maxCircularity* }</span> |  |
|  | Use this flag to filter the output so that only particles in the range of the specified circularity are counted. |
| <span class="table-cell-nowrap">/D = *dataWave*</span> | Specify a wave from which the minimum, maximum, and total particle intensity are sampled when used with the stats keyword. *dataWave* must be of the same dimensions as the input binary image *imageMatrix*. It can be of any real numeric type. Results are returned in the waves W_IntMax, W_IntMin, and W_IntAvg. |
| <span class="table-cell-nowrap">/DS3D = *dest3DInfo*</span> |  |
|  | Use this flag to specify the destination of the 3D particle info wave. If this flag is not specified, the operation saves the data in the wave M_3DParticleInfo in the current data folder. |
| <span class="table-cell-nowrap">/DSBI = *destBIndex*</span> |  |
|  | Use this flag to specify the destination of the boundary index wave. If the flag is not specified, the operation saves the index in the wave W_BoundaryIndex in the current data folder. |
| <span class="table-cell-nowrap">/DSPA = *destPAWave*</span> |  |
|  | Use this flag to specify the destination of the particle area wave. If the flag is not specified, the operation saves the data in the wave M_ParticleArea in the current data folder. |
| <span class="table-cell-nowrap">/DSPL = *destMPWave*</span> |  |
|  | Use this flag to specify the destination of the masking image for the particle. If the flag is not specified the masking image is saved in the wave M_Particle in the current data folder. |
| <span class="table-cell-nowrap">/DSPP = destPerimeter</span> |  |
|  | Use this flag to specify the destination of the particle perimeter wave. If the flag is not specified, the operation saves the data in the wave M_ParticlePerimeter in the current data folder. |
| <span class="table-cell-nowrap">/DSTA = *destIOAWave*</span> |  |
|  | Use this flag to specify the destination object area wave. If this flag is not specified, the operation saves the data in the wave W_ImageObjArea in the current data folder. |
| <span class="table-cell-nowrap">/DSTC = *destCircularity*</span> |  |
|  | Use this flag to specify the destination for the circularity wave. If the flag is not specified, the operation saves the data in the wave W_circularity in the current data folder. |
| <span class="table-cell-nowrap">/DSTM = *destMarkerWave*</span> |  |
|  | Use this flag to specify the destination marker wave. If this flag is not specified, the operation saves the marker wave in the wave M_ParticleMarker in the current data folder. |
| <span class="table-cell-nowrap">/DSTP = *destIOPWave*</span> |  |
|  | Use this flag to specify the destination object perimeter wave. If this wave is not specified the operation saves the data in the wave W_ImageObjPerimeter in the current data folder. |
| <span class="table-cell-nowrap">/DSTR = destRectWave</span> |  |
|  | Use this flag to specify the destination of the object rectangularity wave. If the flag is not specified, the operation saves the data in the wave W_rectangularity in the current data folder. |
| <span class="table-cell-nowrap">/DSTX = *destSpotXW*</span> |  |
|  | Use this flag to specify the destination of the spotX wave. If the flag is not specified, the operation saves the data in the wave W_SpotX in the current data folder. |
| <span class="table-cell-nowrap">/DSTXM = destXMaxW</span> |  |
|  | Use this flag to specify the destination of the xmax position wave. If the flag is not specified, the operation saves the data in the wave W_xmax in the current data folder. |
| <span class="table-cell-nowrap">/DSTY = *destSpotYW*</span> |  |
|  | Use this flag to specify the destination of the spotY wave. If the flag is not specified, the operation saves the data in the wave W_SpotY in the current data folder. |
| <span class="table-cell-nowrap">/DSRM = *destRMWave*</span> |  |
|  | Use this flag to specify the destination of the raw moments wave. If the flag is not specified, the operation saves the data in the wave M_rawMoments in the current data folder. |
| <span class="table-cell-nowrap">/DSIN = *destIntMin*</span> |  |
|  | Use this flag to specify the destination of the minimum particle intensity wave. If the flag is not specified, the operation saves the data in the wave W_IntMin in the current data folder. |
| <span class="table-cell-nowrap">/DSIA = *destIntAvg*</span> |  |
|  | Use this flag to specify the destination of the average intensity wave. If the flag is not specified, the operation saves the data in the wave W_IntAvg in the current data folder. |
| <span class="table-cell-nowrap">/DSIX = *destIntMax*</span> |  |
|  | Use this flag to specify the destination of the maximum particle intensity wave. If the flag is not specified, the operation saves the data in the wave W_IntMax in the current data folder. |
| <span class="table-cell-nowrap">/DSBX = *destBoundaryX*</span> |  |
|  | Use this flag to specify the destination of the boundaryX wave. If the flag is not specified the operation saves the data in the wave W_BoundaryX in the current data folder. |
| <span class="table-cell-nowrap">/DSBY = *destBoundaryY*</span> |  |
|  | Use this flag to specify the destination of the boundaryY wave.  If the flag is not specified the operation saves the data in the wave W_BoundaryY in the current data folder. |
| <span class="table-cell-nowrap">/DSMM = *dest3dMoments*</span> |  |
|  | Use this flag to specify the destination for saving the 3D moments wave. If this flag is not specified, the operation saves the data in the wave M_Moments in the current data folder. |
| <span class="table-cell-nowrap">/DSXN = *destXMinWave*</span> |  |
|  | Use this flag to specify the destination for saving the XMin wave. If the flag is not specified the operation saves the data in the wave W_xmin in the current data folder. |
| <span class="table-cell-nowrap">/DSYN = *destYMinWave*</span> |  |
|  | Use this flag to specify the destination for saving the YMin wave. If the flag is not specified the operation saves the data in the wave W_ymin in the current data folder. |
| <span class="table-cell-nowrap">/DSYM = *destYMaxWave*</span> |  |
|  | Use this flag to specify the destination for saving the YMax wave. If the flag is not specified the operation saves the data in the wave W_ymax in the current data folder. |
| <span class="table-cell-nowrap">/E</span> | Calculate an ellipse that best fits each particle. The equivalent ellipse is calculated by first finding the moments of the particle (i.e., average x-value, average y-value, average x<sup>2</sup>, average y<sup>2</sup> and average x\*y), and then requiring that the area of the ellipse be equal to that of the particle. The resulting ellipses are saved in the wave M_Moments. When *imageMatrix* is a 2D wave, the results returned in M_Moments are the columns: the X-center of the ellipse, the Y-center of the ellipse, the major axis, the minor axis, and the angle (radians) that the major axis makes with the X-direction. When *imageMatrix* is a 3D wave, the results in M_Moments include the sum of the X, Y, and Z components as well as all second order permutations of their products. They are arranged in the order: sumX, sumY, sumZ, sumXX, sumYY, sumZZ, sumXY, sumXZ, and sumYZ. |
| <span class="table-cell-nowrap">/EBPC</span> | Use this flag to exclude from counting any particle that has one or more pixels on any boundary of the image. |
| <span class="table-cell-nowrap">/F</span> | Fills 2D particles having internal holes and adjusts their area measure for the removal of holes. Internal boundaries around the holes are also eliminated.   When the boundary of the particle consists of thin elements that cannot be traversed as a single closed path which passes each boundary pixel only once, the particle will not be filled.  Note that filling particles may increase execution time considerably and on some images it may require large amount of memory. It is likely that a more efficient approach would be to preprocess the binary image and remove holes using morphology operations. This flag is not supported when *imageMatrix* is a 3D wave. |
| <span class="table-cell-nowrap">/FILL</span> | Use /FILL to fill holes inside particles. The reported values of area and perimeter are computed as if there are no holes. The filling algorithm could fail if, for example, there is a closed contour of zeros around the particles. |
|  | If you specify both /F and /FILL the operation uses only /FILL. |
|  | Added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all specified destination waves as a free waves. This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions and only if *destWave*, as specified by /DEST, is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/L = (*row*,*col*)</span> | Specifies a 2D particle location in connection with the mark method. (row, col) is a seed value corresponding to any pixel inside the particle. If the seed belongs to the particle boundary, the particle will not be filled. This flag is not supported when *imageMatrix* is a 3D wave. |
| <span class="table-cell-nowrap">/M = *markerVal*</span> | Use with the stats for 2D images. See stats keyword for a full description of the following waves. |
|  |<table class="nested-table"><tbody><tr><td>***markerVal***</td><td>**Wave**</td></tr><tr><td>0</td><td>no marker waves</td></tr><tr><td>1</td><td>M_ParticlePerimeter</td></tr><tr><td>2</td><td>M_ParticleArea</td></tr><tr><td>3</td><td>M_Particle</td></tr></tbody></table>
|  | This flag is not supported when imageMatrix is a 3D wave. |
| <span class="table-cell-nowrap">/MAXA = *maxArea*</span> |  |
|  | Specifies an upper limit of the area of an acceptable particle when used with the stats keyword. The area is measured in pixels and the default value of *maxArea* is the number of pixels in the image. In 3D the maximum value applies to the number of voxels. |
| <span class="table-cell-nowrap">/NSW</span> | Creates the marker wave (see /M flag) but not the particle statistics waves when used with the stats keyword. This should reduce execution time in images containing many particles. |
| <span class="table-cell-nowrap">/P = *plane*</span> | Specifies the plane when operating on a single layer of a 3D wave. |
| <span class="table-cell-nowrap">/PADB</span> | Use this flag with the stats keyword to pad the image with a 1 pixel wide background. This has the effect that particles touching the image boundary are now interior particles with closed perimeter (that extend one pixel beyond the original image frame). In addition, entries in the wave W_ObjPerimeter will be longer for all boundary particles which will also affect other derived parameters such as circularity. |
|  | /PADB is different from /B in that it takes into account all pixels belonging to the particle that lie on the boundary of the image. The two flags are mutually exclusive. |
|  | /PADB was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/PDLG</span> | Displays a progress dialog. |
|  | /PDLG is useful when you are processing very large 3D images. The progress dialog provides feedback and allows the user to abort the operation. |
|  | /PDLG was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/Q</span> | Quiet flag, does not report the number of particles to the history area. |
| <span class="table-cell-nowrap">/R = *roiWave*</span> | Specifies a region of interest (ROI). The ROI is defined by a wave of type unsigned byte (/b/u) that has the same number of rows and columns as *imageMatrix*. The ROI itself is defined by the entries or pixels in the *roiWave* with value of 0. Pixels outside the ROI may have any nonzero value. The ROI does not have to be contiguous. When *imageMatrix* is a 3D wave, *roiWave* can be either a 2D wave (matching the number of rows and columns in *imageMatrix* ) or it can be a 3D wave that must have the same number of rows, columns and layers as *imageMatrix*. When using a 2D *roiWave* with a 3D *imageMatrix* the ROI is understood to be defined by *roiWave* for each layer in the 3D wave. |
|  | See [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md) for more information on creating 2D ROI waves. |
| <span class="table-cell-nowrap">/U</span> | Save the wave M_ParticleMarker as an 8-bit unsigned instead of the default 16-bit when used with the mark keyword. |
| <span class="table-cell-nowrap">/W</span> | Creates boundary waves W_BoundaryX, W_BoundaryY and W_BoundaryIndex for a 2D *imageMatrix* wave. W_BoundaryX and W_BoundaryY contain the pixels along the boundary of the particles. The boundary of each particle ends with a NaN entry in both waves. Each entry in W_BoundaryIndex is the index to the start of a new particle in W_BoundaryX and W_BoundaryY, so that you can quickly locate the boundary of each particle. |
|  | When there are holes in particles, the entries in W_BoundaryX and W_BoundaryY start with the external boundary followed by all the internal boundaries for that particle. There are no index entries for internal boundaries. |
|  | This flag is not supported when *imageMatrix* is a 3D wave. |

### *Details* {#details}
Particle analysis is accomplished by first converting the data from its original format into a binary representation where the particle is designated by zero and the background by any nonzero value. The algorithm searches for the first pixel or voxel that belongs to a particle and then grows the particle from that seed while keeping count of the area, perimeter and count of pixels or voxels in the particle. If you use additional flags the algorithm has to compute additional quantities for each pixel or voxel that belong to the particle. If your goal is only to mask the particle, a more efficient approach is to use the [ImageSeedFill](/igorpro/commands/imageseedfill.md) operation, which similarly follows the particle but does not spend processing time on computing unrelated particle properties. ImageSeedFill also has the additional advantage of not requiring that the input wave is binary so that it also saves you the time on performing the initial threshold and, in fact, may produce much better results if you are using the adaptive/fuzzy features, which are not available in ImageAnalyzeParticles.

### *Examples* {#examples}
Convert a grayscale image (blobs) into a proper binary input:


```igor
ImageThreshold/M=4/Q/I blobs
```

Get the statistics on the thresholded image of blobs and create an image mask output wave for the perimeter of the particles:


```igor
ImageAnalyzeParticles/M=1 stats M_ImageThresh
```

Display an image of the blobs with a red overlay of the perimeter image:


```igor
NewImage/F blobs; AppendImage M_ParticlePerimeter
ModifyImage M_ParticlePerimeter explicit=1, eval={0,65000,0,0}
```

### *See Also* {#see-also}
[ImageThreshold](/igorpro/commands/imagethreshold.md), [ImageGenerateROIMask](/igorpro/commands/imagegenerateroimask.md), [ImageSeedFill](/igorpro/commands/imageseedfill.md), [ModifyImage](/igorpro/commands/modifyimage.md)

[Image Processing](/igorpro/analysis/image-processing.md)