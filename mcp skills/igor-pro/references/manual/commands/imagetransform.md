---
description: "The ImageTransform operation performs one of a number of transformations on ImageMatrix."
slug: /commands/imagetransform
---

<div className="command-signature">

## <strong>ImageTransform</strong>  [ <em>flags</em> ] <em>Method</em> <em>imageMatrix</em> {#imagetransform}

</div>

The ImageTransform operation performs one of a number of transformations on *ImageMatrix*. The result of using most keywords is a new wave stored in the current data folder. As of Igor Pro 10, users can specify the output wave using the relevant destination wave flags (/DEST, /DSTB, or /DSTC). Most flags in this operation are exclusive to the keywords in which they are mentioned.  Note that some old keywords and flags in this operation use the term "plane" when referring to a layer of a 3D or 4D wave.

### *Parameters* {#parameters}
*Method* selects type of transform. It is one of the following names:


|  |  |
| --- | --- |
| averageImage | Computes an average image for a stack of images contained in 3D *imageMatrix*. The average image is stored in the wave M_AveImage and the standard deviation for each pixel is stored in the wave M_StdvImage in the current data folder. You can use this keyword together with the optional /R flag where a region of interest is defined by zero value points in a ROI wave. The operation sets to NaN the entries in M_AveImage and M_StdvImage that correspond to pixels outside the ROI. *imageMatrix* must have at least three layers. |
| averageRGBImages | Computes an average image from a sequence of RGB(A) images represented by a 4D wave. The average is computed separately for the R, G, B, and optional A channels, and the resulting RGB(A) image is stored in the wave M_AverageRGBImage in the current data folder. The operation supports all real data types. |
|  | Added in Igor Pro 7.00. |
| backProjection | Reconstructs the source image from a projection slice and stores the result in the wave M_BackProjection. The projection slice should either be a wave produced by the projectionSlice keyword of this operation or a wave that would be similarly scaled. The input must be a single or double precision real 2D wave. Row scaling must range symmetrically about zero. For example, if the reconstructed image is expected to have 256 rows then the row scaling of the input should be from -128 to 127. Similarly, the column scaling of the input should range between zero and pi. An equivalent implementation as a user function is provided in the demo experiment. You can use this implementation as a starting point if you want to develop filtered back projection. |
|  | <div><Admonition type="note"><p>**See also:** projectionSlice keyword and the RadonTransformDemo experiment. For algorithm details see the chapter "Reconstruction of cross-sections and the projection-slice theorem of computerized tomography" in Born and Wolf, 1999.</p></Admonition></div> |
| ccsubdivision | Performs a Catmull-Clark recursive generation of B-spline surfaces. There are two valid inputs to this implementation: triangular meshes or quad meshes. |
|  | Quad meshes are assumed to be in the form of a 3D wave where the first layer contains the X-values (of mesh vertices), the second layer contains the Y-values and the third layer the Z-values. |
|  | Triangle meshes are more complicated to convert into face-edge-vertex arrays so they are less desirable in this application. They are stored in a three column (triplet) wave where the first column corresponds to the X coordinates, the second to the Y coordinates and the third to the Z coordinates. Each triangle is described by three rows in the triplet wave.  Common vertices are repeated so that each sequential three rows in the triplet wave correspond to a single triangle. You can also associate a scalar value with each vertex and it will be suitably interpolated as new vertices are computed and old ones are shifted. In this case the input source wave contains one more column in the case of a triplet wave or one more layer in the case of a quad/mesh wave. The scalar value is added everywhere as an additional dimension to the spatial part of any point calculation. |
|  | You can specify the number of iterations using the /I flag. By default the operation executes a single iteration. The output is saved in the wave M_CCBSplines that consists of 4 columns. Each row corresponds to a Quad where the 3 layers contain the X, Y, and Z components. If you are using an optional scalar in the input, the scalar result is stored in the wave M_CCBScalar. |
|  | In some situations you may encounter spatial degeneracies when two or more parts of the surface meet at common vertices. This leads to one or more error messages in the history area of the command window. You can try to break a degeneracy yourself by adding a small perturbation to the input coordinates or you can use the /PRTF flag which adds a random perturbation on the order of 1e-10 times the extent of the data in each dimension. The perturbation does not affect the scalar. |
| cmap2rgb | Converts an image and its associated colormap wave (specified using the /C flag) into an RGB image stored in a 3D wave M_RGBOut. |
| CMYK2RGB | Converts a CMYK image, stored as 4 layer unsigned byte wave, into a 3 layer, standard RGB image wave. The output wave is M_CMYK2RGB that is stored in the current data folder. |
| compress | Compresses the data in the *imageWave* using a nonlossy algorithm and stores it in the wave W_Compressed in the current data folder. The compressed wave includes all data associated with *imageWave* including its units and wavenote. Use the decompress keyword to recover the original wave. The operation supports all numeric data types. |
|  | <div><Admonition type="note"><p>The compression format for waves greater than 2GB in size was changed in version 6.30B02. If you compressed a wave greater than 2 GB in IGOR64 6.30B01, you will need to decompress it using the same version. You cannot decompress it in 6.30B02 or later.</p></Admonition></div> |
| convert2gray | Converts an arbitrary 2D wave into an 8-bit normalized 2D wave. The default output wave name is M_Image2Gray. |
| decompress | Decompresses a compressed wave. It saves a copy of the decompressed wave under the name W_DeCompressed in the current data folder. |
|  | <div><Admonition type="note"><p>The compression format for waves greater than 2GB in size was changed in version 6.30B02. If you compressed a wave greater than 2 GB in IGOR64 6.30B01, you will need to decompress it using the same version. You cannot decompress it in 6.30B02 or later.</p></Admonition></div> |
| distance | Computes the distance transform, also called "distance map", for the input image. Added in Igor Pro 7.00. |
|  | The distance transform/map is an image where every pixel belonging to the "object" is replaced by the shortest distance of that pixel from the background/boundary. |
|  | *imageMatrix* must be a 2D wave of type unsigned byte (Make/B/U) where pixels corresponding to the object are set to zero and pixels corresponding to the background are set to 255. Such an image can be obtained, for example, using [ImageThreshold](/igorpro/commands/imagethreshold.md). |
|  | The resulting distance map is stored in the wave M_DistanceMap in the current data folder. The operation supports three metrics (Manhattan, Euclidean, Euclidean + scaling) set via the /METR flag. |
| extractSurface | Extracts values corresponding to a plane that intersects a 3D volume wave (ImageMatrix). You must specify the extraction parameters using the /X flag. The volume is defined by the wave scaling of the 3D wave. The result, obtained by trilinear interpolation, is stored in the wave M_ExtractedSurface and is of the type NT_FP64. Points in the plane that lie outside the volume are set to NaN. |
| fht | Performs a Fast Hartley Transform subject to the /T flag. The source wave must be a 2D real matrix with a power of 2 number of rows and columns. Default output is saved in the double-precision wave M_Hartley in the current data folder. If you use the /O flag the result overwrites *imageMatrix* without changing the numeric type. If *imageMatrix* is single-precision float the conversion is straightforward. All other numeric types are scaled. Single- and double-byte types are scaled to the full dynamic range. 32 bit integers are scaled to the range of the equivalent 16 bit types (i.e., unsigned int is scaled to unsigned short range etc.). This keyword does not support wave scaling or NaN entries. |
| fillImage | Fills a 2D target image wave with the data from a 1D image wave (specified using /D=*wave1D* ). Both waves must have the same data type and the number of data points in the target wave must match the number of points in the data wave. There are four fill modes that are specified via the /M flag. The operation supports all noncomplex numeric data types. |
| findLakes | Originally intended to identify lakes in geographical data, this operation creates a mask for a 2D wave for all the contiguous points whose values are close to each other. You can determine the minimum number of pixels within a contiguous region using the /LARA=*minPixels* flag (the default is 100). You can determine how close values must be in order to belong to a contiguous region using the /LTOL=*tolerance* flag (default is zero). You can also limit the search region using the /LRCT flag. Use the flag /LTAR=*target* to set the value of the masked regions. By default, the algorithm uses 4-connectivity when looking at adjacent pixels. You can set it to 8-connectivity using the /LCVT flag. The result of the operation is saved in the wave M_LakeFill. It has the same data type as the source wave and contains all the source values outside the masked pixels. |
| flipCols | Rearrange pixels by exchanging columns symmetrically about a center column or the center of the image (if the number of columns is even). The exchange is performed in place and can be reverted by repeating the operation. When working with 3D waves, use the /P flag to specify the layer that you want to operate on. |
| flipRows | Rearrange pixels in the image by exchanging rows symmetrically about the middle row or the middle of the image (if the image has an even number of rows). The exchange is performed in place and can be reverted by repeating the operation. When working with 3D waves, use the /P flag to specify the layer that you want to operate on. (See also setPlane keyword, [ImageRotate](/igorpro/commands/imagerotate.md).) |
| flipPlanes | Rearrange data in a 3D wave by exchanging layers symmetrically about the middle layer. The operation is performed in place and can be reverted by repeating the operation. |
| fuzzyClassify | Segments grayscale and color images using fuzzy logic. Iteration stops when it reaches convergence defined by /TOL or the maximum number of iterations specified by /I. It is a good practice to specify the tolerance and the number of iterations. If the number of classes is small, the operation prints the class values in the history. Use /Q to eliminate printing to the history and increase performance. Use /CLAS to specify the number of classes and optionally use /CLAM to modify the fuzzy probability values. Use /SEG to generate the segmentation image. The classes are stored in the wave W_FuzzyClasses in the current data folder and it will be overwritten if it already exists. |
|  | When imageMatrix is a grayscale image, each class is a single wave entry. When imageMatrix is a RGB image, classes are stored consecutively in the wave W_FuzzyClasses. If you request more classes than are present in imageMatrix, you will likely find a degeneracy where the space of a data class is spanned by more than one class. It is a good idea to compute the Euclidean distance between every possible pair of classes and eliminate degeneracies when the distance falls below some threshold. |
|  | Any real data type is allowed but values in the range [0,255] are optimal. You can segment 3D waves of more than 3 layers in which a class will be a vector of dimensionality equal to the number of layers in imageMatrix. |
|  | For examples see Examples/Imaging/fuzzyClassifyDemo.pxp. |
| getBeam | Extracts a beam from a 3D wave. |
|  | A "beam" is a 1D array in the Z-direction. If a row is a 1D array in the first dimension and a column is a 1D array in the second dimension then a beam is a 1D array in the third dimension. |
|  | The number of points in a beam is equal to the number of layers in *imageWave*. Specify the beam with the /BEAM={*row*,*column* } flag. It stores the result in the wave W_Beam in the current data folder. W_Beam has the same numeric type as *imageWave*. Use setBeam to set beam values. (See also, [MatrixOp](/igorpro/commands/matrixop.md) beam.) |
| getChunk | Extracts the chunk specified by chunk index /CHIX from *imageMatrix* and stores it in the wave M_Chunk in the current data folder. For example, if *imageMatrix* has the dimensions (10,20,3,10), the resulting M_Chunk has the dimensions (10,20,3). See also keywords setChunk and insertChunk and [MatrixOp](/igorpro/commands/matrixop.md) chunk. |
| getCol | Creates a 1D wave named W_ExtractedCol from any type of 2 or 3D wave. You specify the column using the /G=*columnNumber* flag. If your source wave is 3D you can also specify the layer using the /P=*layerNumber* flag. If you do not specify the layer, Igor assumes that you are using the first layer. *imageMatrix* can be real or complex. (See also putCol keyword, [MatrixOp](/igorpro/commands/matrixop.md) col.) |
| getPlane | Creates a new wave named M_ImagePlane that contains the data in the layer specified by the /P flag. The new wave is of the same data type as the source wave. You can specify the type of plane using the /PTYP flag. (See also setPlane keyword, [MatrixOp](/igorpro/commands/matrixop.md).) |
| getRow | Creates a 1D wave named W_ExtractedRow from any type of 2 or 3D wave. You specify the row using the /G=*rowNumber* flag. If your source wave is 3D you can also specify the plane using the /P=*planeNumber* flag. If you do not specify the plane, Igor assumes that you are using the first plane. *imageMatrix* can be real or complex. (See also putRow keyword, [MatrixOp](/igorpro/commands/matrixop.md) row.) |
| Hough | Performs the Hough transform of the input wave. The result is saved to a 2D wave M_Hough in which the columns correspond to angle and the rows correspond to the radial domain. |
|  | By default the output consists of 180 columns. Use the /F flag to modify the angular resolution. |
|  | If the input image has N rows and M columns then the number of rows in the M_Hough is set to 1+sqrt(N^2+M^2). The output radius should be read relative to the center row. |
|  | It is assumed that the input wave has square pixels of unit size and that is binary (/B/U) where the background value is 0. |
|  | See also [Hough Transform](/igorpro/analysis/image-processing.md#hough-transform). |
| hsl2rgb | Transforms a 3-layer HSL wave into a 3-layer RGB wave. If the source wave for this operation is of any type other than byte or unsigned byte, the HSL values are expected to be between 0 and 65535. For all source wave types the resulting RGB wave is of type unsigned short. The result of the operation is the wave M_HSL2RGB (of type unsigned word), where the RGB values are in the range 0 to 65535. |
| hslSegment | Creates from the specified image a binary image of the same dimensions, in which all pixels that belong to all three of the specified Hue, Saturation and Lightness ranges are set to 255 and the others to zero. You can specify the HSL ranges using the /H, /S and /L flags. Each flag takes as an argument either a pair of values or a wave containing pairs of values. You must specify the /H flag but you can omit the /S and /L flags in which case the default values (corresponding to full range [0,1]) are used. *imageMatrix* is assumed to be an RGB image. |
| imageToTexture | Transforms a 2D or 3D image wave into a 1D wave of contiguous pixel components. The transformation is useful for creating an OpenGL texture (for Gizmo) or for saving a color image in a format requiring either RGB or RGBA sequences. |
|  | The /O flag does not apply to imageToTexture. |
|  | Use the /TEXT flag to specify the type of transformation. *imageMatrix* must be an unsigned byte wave. A 1D unsigned byte wave named W_Texture is created in the current data folder. |
|  | W_Texture's wave note is set to a semicolon-separated list of *keyword* -*value* pairs that can be parsed using [StringByKey](/igorpro/commands/stringbykey.md) and [NumberByKey](/igorpro/commands/numberbykey.md): |
|  |<table class="nested-table"><tbody><tr><td>**Keyword**</td><td>**Information Following Keyword**</td></tr><tr><td>WIDTHPIXELS</td><td>[DimSize](/igorpro/commands/dimsize.md)(*imageMatrix*,0) or truncated to nearest power of 2 if /TEXT value is odd</td></tr><tr><td>HEIGHTPIXELS</td><td>[DimSize](/igorpro/commands/dimsize.md)(*imageMatrix*,1) or truncated to nearest power of 2</td></tr><tr><td>LAYERS</td><td>[DimSize](/igorpro/commands/dimsize.md)(*imageMatrix*,2)</td></tr><tr><td>TEXTUREMODE</td><td>*val* parameter from /TEXT flag</td></tr><tr><td>SOURCEWAVE</td><td>[GetWavesDataFolder](/igorpro/commands/getwavesdatafolder.md)(*imageMatrix*, 2)</td></tr></tbody></table>
| indexWave | Creates a 1D wave W_IndexedValues in the current data folder containing values from *imageMatrix* that are pointed to by the index wave (see /IWAV). Each row in the index wave corresponds to a single value of *imageMatrix*. If any row does not point to a valid index (within the dimensions of *imageMatrix* ), the corresponding value is set to zero and the operation returns an error. Indices are zero based integers; the operation does not support interpolation and ignores wave scaling. |
| insertChunk | Inserts a chunk (a 3D wave specified by the /D flag) into *imageMatrix* at chunk index specified by the /CHIX flag. The dimensions of the inserted chunk must match the first three dimensions of *imageMatrix*. The wave must also have the same numeric type. The 4th dimension of *imageMatrix* is incremented by 1 to accommodate the new data. See also getChunk and setChunk. |
| insertImage | Inserts the image specified by the flag /INSI into *imageMatrix* starting at the position specified by the flags /INSX and /INSY. If the *imageMatrix* is a 3D wave then it inserts the image in the layer specified by the /P flag. The inserted image and *imageMatrix* must be the same data type. The inserted data is clipped to the boundaries of *imageMatrix*. See also [MatrixOP](/igorpro/commands/matrixop.md) insertMat. |
| insertXplane | Inserts a 2D wave as a new layer perpendicular to the X-axis in a 3D wave. The /P flag specifies the insertion point and the /INSW flag specifies the inserted wave. The 2D inserted wave must have the same numeric data type as the 3D wave and its dimensions must be cols x layers of the 3D wave. For example, if the 3D wave has the dimensions (10x20x30) the 2D wave must be 20x30. If you do not use the /O flag, it stores the result in the wave M_InsertedWave in the current data folder. |
| insertYplane | Inserts a 2D wave as a new layer perpendicular to the Y-axis in a 3D wave. The /P flag specifies the insertion point and the /INSW flag specifies the inserted wave. The 2D wave must be the same numeric data type as the 3D wave and its dimensions must be rows x layers of the 3D wave. For example, if the 3D wave has the dimensions (10x20x30) the 2D wave must be 10x30.   If you do not use the /O flag, it stores the result in the wave M_InsertedWave in the current data folder. |
| insertZplane | Inserts a 2D wave as a new layer perpendicular to the Z-axis in a 3D wave. The /P flag specifies the insertion point and the /INSW flag specifies the inserted wave. The 2D wave must be the same numeric data type as the 3D wave and its dimensions must be rows x cols of the 3D wave. For example, if the 3D wave has the dimensions (10x20x30) the 2D wave must be 10x20. If you do not use the /O flag, it stores the result in the wave M_InsertedWave in the current data folder. This keyword is included for completeness. You can accomplish the same task using [InsertPoints](/igorpro/commands/insertpoints.md). |
| invert | Converts pixel values using the formula newValue=255-oldValue. Works on unsigned byte waves of any dimensions. The result is stored in the wave M_Inverted unless specifying the /O flag. |
| matchPlanes | Finds pixels that match test conditions in all layers of a 3D wave. It creates a 2D unsigned byte output wave M_matchPlanes that is set to the two values 0 and 255. The value 255 indicates that the corresponding pixel has satisfied test conditions in all layers of the wave for which conditions were provided. Otherwise the pixel value is 0. |
|  | Test conditions are entered as a 2D wave using the /D flag. The condition wave must be double precision and it must contain the same number of columns as the number of layers in the 3D source wave. A condition for layer j of the source wave is specified by two rows in column j of the condition wave. The first row entry, say *A*, and the second row entry, say *B*, imply a condition on pixels in layer j such that $$ \displaystyle A \leq x \leq B $$. You can have more than one condition for a given layer by adding pairs of rows to the condition wave. For example, if you add in consecutive rows the values C and D, this implies the test: |
|  | $$ \displaystyle (A \leq x \leq B) \|(C \leq x \leq D) . $$ |
|  | If you do not have any conditions for some layer, set its corresponding condition column to NaN. Similarly, if you have two conditions for the first layer and one condition for the second layer, pad the bottom of column 1 in the condition wave with NaNs. See Examples for use of this keyword to perform hue/saturation segmentation. |
| offsetImage | Shifts an image in the XY plane by dx, dy pixels (specified by the /IOFF flag). Pixels outside the shifted image will be set to the specified background value. The operation works on 2D waves or on 3D waves with the optional /P flag. When shifting a 3D wave with no specified layer, it creates a 3D wave with all layers offset by the same amount. The wave M_OffsetImage contains the result in the current data folder. |
|  | The /O flag is not supported with offsetImage. |
| padimage | Standard padding uses the /N flag to extend the source image. When enlarged, values from the last row and column fill in the new area. The /N flag specifies the new image size in terms of the rows and columns change. The /W flag specifies whether data should be wrapped when padding the image. |
|  | Central padding uses the /CPAD flag to resize the image symmetrically.  Depending on the flag parameters the resulting image may be padded by repeating the values of boundary pixels or by mirroring values of boundary pixels.  Also, if /CPAD specifies a negative number of pixels (say *nx*), the resulting image is reduced in size by deleting *nx* rows and columns from each side of the image.  For example, you can use padImage with /CPAD={1,0} to create an input for ImageEdgeDetection and then use padImage on the result with /CPAD={-1,0} to return to the original image size. |
|  | Unless you use the /O flag, the result is stored in the wave M_PaddedImage in the current data folder or in the specified destination wave. |
| pad3d | Pads a 3D wave by extending all six faces using edge replication. The /N3DP flag specifies the number of rows, columns, and layers to add on each side. Each padding value must be strictly less than the corresponding source dimension. |
|  | The padding algorithm fills 27 sub-regions of the output volume: the original data is copied into the center, edge values are replicated into the 6 face slabs, the nearest edge values fill the 12 edge strips, and the nearest corner values fill the 8 corner cubes. |
|  | The result is stored in the wave M_Padded3D in the current data folder. imageMatrix must be a 3D wave. All numeric data types are supported. The /O flag is not supported with pad3d. |
|  | Added in Igor Pro 10.00. |
| projectionSlice | Computes a projection slice for a parallel fan of rays going through the image at various angles. For every ray in the fan the operation computes a line integral through the image (equivalent to the sum of the line profile along the ray). The operation computes the line integrals for multiple fans defined by the number and position of the rays as well as the angle that they make with the positive x-direction. Use the /PSL flag to specify the projection parameters. The projection slice itself is stored in a 2D wave M_ProjectionSlice where the rows correspond to the rays and the columns correspond to the selected range of angles. The operation does not support wave scaling. If the source wave is 3D the projection slice currently supports slices that are perpendicular to the z-axis and specified by their plane number. |
|  | <div><Admonition type="note"><p>**See also:** backProjection keyword and the RadonTransformDemo experiment. For algorithm details see the chapter "Reconstruction of cross-sections and the projection-slice theorem of computerized tomography" in Born and Wolf, 1999.</p></Admonition></div> |
| putCol | Sets a column of *imageMatrix* to the values in the wave specified by the /D flag. Use the /G flag to specify column number and the /P flag to specify the layer. Note that if there is a mismatch in the number of entries between the specified waves, the operation uses the smaller number. See also getCol keyword. |
| putRow | Sets a row of *imageMatrix* to the values in the wave specified by the /D flag. Use the /G flag to specify row number and the /P flag to specify the layer. Note that if there is a mismatch in the number of entries between the specified waves, the operation uses the smaller number. See also getRow keyword. |
| removeXplane | Removes one or more planes perpendicular to the X-axis from a 3D wave. The /P flag specifies the starting position. By default, it removes a single plane but you can remove more planes with the /NP flag. If you do not use the /O flag, it saves the result in the wave M_ReducedWave in the current data folder. |
| removeYplane | Removes one or more planes perpendicular to the Y-axis from a 3D wave. The /P flag specifies the starting position. By default, it removes a single plane but you can remove more planes with the /NP flag. If you do not use the /O flag, it saves the result in the wave M_ReducedWave in the current data folder. |
| removeZplane | Removes one or more planes perpendicular to the Z-axis from a 3D wave. The /P flag specifies the starting position. By default, it removes a single plane but you can remove more planes with the /NP flag. If you do not use the /O flag, it saves the result in the wave M_ReducedWave in the current data folder. |
| rgb2cmap | Computes a default color map of 256 colors to represent the input RGB image. The colors are computed by clustering the input pixels in RGB space. The resulting color map is stored in the wave M_ColorIndex in the current data folder. The operation also saves the wave M_IndexImage which contains an index into the colormap that can be used to display the image using the commands: |
|  | <code class="igor">NewImage M_IndexImage&#10;ModifyImage M_IndexImage cindex= M_ColorIndex</code> |
|  | To change the default number of colors use the /NCLR flag. When the number of colors is greater than 256, M_IndexImage will be a 16-bit unsigned integer or a 32 bit integer wave depending on the number. rgb2cmap supports input images in the form of 3D waves of type unsigned byte or single precision float. The floating point option may be used to input images in colorspaces that use signed numeric data. |
| rgb2gray | When the input *imageMatrix* is a 3D RGB wave, rgb2gray produces a 2D wave of type unsigned byte containing the grayscale representation of the input. By default, the operation stores the output in the wave M_RGB2Gray in the current data folder. The RGB values are converted into the luminance Y of the YIQ standard using: |
|  | <code class="igor">Y = 0.299R + 0.587G + 0.114B</code> |
|  | When the input *imageMatrix* is a 4D wave containing multiple (3 layer) RGB chunks, the conversion produces a 3D wave where each layer corresponds to the grayscale conversion of the corresponding chunk in the input wave. In this case the numeric type of the output is the same as that of the input but the conversion formula is the same. The /O flag is not supported when transforming a 4D RGB wave. |
| rgb2hsl | Converts an RGB image stored in a 3D wave into another 3D wave in which the three planes correspond to the Hue, Saturation and Lightness of the HSL color model. Values of all components are normalized to the range [0,255] unless the /U flag is used or if the source wave is not 8-bit, in which case the range is [0,65535]. The default output wave name is M_RGB2HSL. |
| rgb2i123 | Performs a colorspace conversion of an RGB image into the following quantities: |
|  | $$ \displaystyle \begin{array}{l} I_{1}=\|R-G\| D \\ I_{2}=\|R-B\| D \\ I_{3}=\|G-B\| D, \end{array} $$ where $$ \displaystyle D=\frac{255}{\|R-G\|+\|R-B\|+\|G-B\|}. $$ |
|  | I1, I2, and I3 are stored in the wave M_I123 (using the same data type as the original RGB wave) in the current data folder. I1 is stored in the first layer, I2 in the second and I3 in the third. This color transformation is said to have useful applications in machine vision. |
|  | For more information see: Gevers, T., and A.W.M. Smeulders, Color Based Object Recognition, *Pattern Recognition*, *32*, 453-464, 1999. |
| rgb2xyz | Converts a 3D RGB image wave into a 3D wave containing the XYZ color space equivalent. The conversion is based on the D65 white point and uses the following transformation: |
|  | $$ \displaystyle \left[\begin{array}{l} x \\ y \\ z \end{array}\right]=\left[\begin{array}{lll} 0.412453 & 0.357580 & 0.180423 \\ 0.212671 & 0.715160 & 0.072169 \\ 0.019334 & 0.119193 & 0.950227 \end{array}\right]\left[\begin{array}{l} R \\ G \\ B \end{array}\right] $$ |
|  | The XYZ values are stored in a wave named "M_RGB2XYZ" unless the /O flag is used, in which case the source image is overwritten and converted into single precision wave (NT_FP32). |
| roiTo1D | Copies all pixels in an ROI and saves them sequentially in a 1D wave. The ROI is specified by /R. The ROI wave must have the same dimensions as *imageMatrix*. If *imageMatrix* is a 3D wave, the ROI must have as many layers as *imageMatrix*. The wave W_roi_to_1d contains the output in the current data folder, has the same numeric type as *imageMatrix*, and contains the selected pixels in a column-major order. |
| rotateCols | Rotates rows in place. This operation is analogous to the Rotate operation except that it works on images and rotates an integer number of rows. The number of rows is specified by the /G flag. |
|  | When *imageMatrix* contains multiple layers you can use the /P flag to specify the layer of the wave that will undergo rotation. By default, if you do not specify the /P flag and if *imageMatrix* consists of three layers (RGB), then all three layers are rotated. Otherwise the operation rotates only the first layer of the wave. |
| rotateRows | Rotates columns in place. This operation is analogous to the Rotate operation except that it works on images and rotates an integer number of columns. The number of columns is specified by the /G flag. |
|  | When *imageMatrix* contains multiple layers you can use the /P flag to specify the layer of the wave that will undergo rotation. By default, if you do not specify the /P flag and if *imageMatrix* consists of three layers (RGB), then all three layers are rotated. Otherwise the operation rotates only the first layer of the wave. |
| scalePlanes | Scales each plane (layer) of the 3D wave, *imageMatrix*, by a constant taken from the corresponding entry in the 1D wave specified by the /D flag. The result is stored in the wave M_ScaledPlanes unless the /O flag is specified, in which case scaling is done in place. See also [MatrixOP](/igorpro/commands/matrixop.md) scaleLayers. |
|  | When using /O, first redimension the wave to a different data type to make sure there are no artifacts due to type clipping. |
|  | If *imageMatrix* is double precision, M_ScaledPlanes is double precision. Otherwise M_ScaledPlanes is single precision. |
|  | This operation also supports the optional /R=*ROIWave* flag. |
|  | Note that when you display M_ScaledPlanes, which has three planes that originated from scaling byte data, you will have to multiply the wave by 255 to see the image because of IGOR's RGB format for SP and DP data requires the range of [0,65535]. |
| selectColor | Creates a mask for the image in which pixel values depend on the proximity of the color of the image to a given central color. The central color, the tolerance and a grayscale indicator must be specified using the /E flag. |
|  | For example, /E={174,187,75,10,1} specifies an RGB of (174,187,75), a tolerance level of 10 and a requested grayscale output. |
|  | RGB values must be provided in a range appropriate for the source image. If the source wave type is not byte or unsigned byte, then the range of the RGB components should be 0 to 65535. |
|  | The color proximity is calculated in the nonuniform RGB space and the tolerance applies to the maximum component difference from the corresponding component of the central color. |
|  | The tolerance, just like the central color, should be appropriate to the type of the source wave. |
|  | The generated mask is stored in the wave M_SelectColor in the current data folder. If a wave by that name exists prior to the execution of this operation, it is overwritten. You can also use the /R flag with this operation to limit the color selection to pixels in the ROI wave whose value is zero. |
| setBeam | Sets the data of a particular beam in *imageMatrix*. |
|  | A "beam" is a 1D array in the Z-direction. If a row is a 1D array in the first dimension and a column is a 1D array in the second dimension then a beam is a 1D array in the third dimension. |
|  | Specify the beam with the /Beam={*row*,*column* } flag and the 1D beam data wave with the /D flag. The beam data wave must have the same number of elements as the number of layers and same numeric type as *imageMatrix*. Use getBeam to extract the beam. |
| setChunk | Overwrites the data in the wave *imageMatrix* at chunk index specified by /CHIX with the data contained in a 3D wave specified by the /D flag. The assigned data must be contained in a wave that matches the first three dimensions of *imageMatrix* and must have the same number type. See also getChunk and insertChunk. |
| setPlane | Sets a plane (given by the /P flag) in the designated image with the data in a wave specified by the /D flag. It is designed as a complement of the getPlane keyword to provide an easier (faster) way to create multiplane images. Note that the operation supports setting a plane when the source data is smaller than the destination plane in which case the source data is placed in memory contiguously starting from the corner pixel of the destination plane.  If the source data is larger than the destination plane it is clipped to the appropriate rows and columns.  If you are setting all planes in the destination wave using algorithmically named source waves you could use the keyword StackImages instead. See also getPlane keyword. |
| shading | Calculates relative reflectance of a surface for a light source position defined by the flag /A. |
|  | The calculation estimates the slope of the surface and then computes a relative reflectance defined as the dot product of the direction of the sun and the normal to the surface at the point of interest. The reflectivity is scaled using the expression: |
|  | *outPixel* = *shadingA* \* (*sunDirection* · *surfaceNormal*) + *shadingB* |
|  | By default *shadingA* = 1, *shadingB* = 0. |
|  | The result of the operation is stored in the wave M_ShadedImage, which has the same data type as the source wave. |
|  | If the source wave is any integer type, and the value of *shadingA* = 1 the operation sets that value to 255. |
|  | The smallest size wave that's supported is 4x4 elements. |
|  | Because the calculation involves evaluating derivatives, the values along the boundary (1 pixel wide) are arbitrary because there are no derivatives for those pixels. We fill the arbitrary values with duplicates of the inner rows and columns. Note that you can use Gizmo and OpenGL shading as an alternative to this operation. |
| shrinkBox | Shrinks a 3‑dimensional imageMatrix to the smallest axis‑aligned box that contains all voxels whose values differ from a specified outer value. The outer value is provided using the /F flag.  This is especially useful after using [ImageSeedFill](/igorpro/commands/imageseedfill.md), which often assigns an outer value to voxels surrounding an object of interest. The cleanup operation extracts only the minimal 3‑D region that still contains all meaningful (non‑outer) data.
The resulting sub‑volume is stored in the wave M_shrunkBox. |
|  | Added in Igor Pro 7.00. |
| shrinkRect | Shrinks *imageMatrix* to include only the minimum rectangle that contains all the pixels whose value is different from an outer value. The outer value is specified with the /F flag. This feature is useful in situations where [ImageSeedFill](/igorpro/commands/imageseedfill.md) has set the pixels around the object of interest to some outer value and it is desired to extract the smallest rectangle that contains interesting data. The output is stored in the wave M_Shrunk. |
| stackImages | Creates a 3D or 4D stack from individual image waves in the current data folder. The waves should be of the form *baseNameN*, where *N* is a numeric suffix specifying the sequence order. *imageMatrix* should be the name of the first wave that you want to add to the stack. You can use the /NP flag to specify the number of waves that you want to add to the stack. |
|  | The result is a 3D or 4D wave named M_Stack, which overwrites any existing wave of that name in the current data folder. |
|  | If the /K flag is specified, the operation kills all the waves that it copies into the stack. |
| sumAllCols | Creates a wave W_sumCols in which every entry is the sum of the pixels on the corresponding image column. Use the /P flag to specify the image plane for a 3D wave. By default the top plane will be processed. |
| sumAllRows | Creates a wave W_sumRows in which every entry is the sum of the pixels on the corresponding image row. Use the /P flag to specify the image plane for a 3D wave. By default the top plane will be processed. |
| sumCol | Stores in the variable V_value the sum of the elements in the column specified by /G flag and optionally the /P flag. |
| sumPlane | Stores in the variable V_value the sum of the elements in the plane specified by the /P flag. |
| sumPlanes | Creates a 2D wave M_SumPlanes which contains the same number of rows and columns as the 3D source wave. Each entry in M_SumPlanes is the sum of the corresponding pixels in all the planes of the source wave. M_SumPlanes is a double precision wave if the source wave is double precision. Otherwise it is a single precision wave. |
| sumRow | Stores in the variable V_value the sum of the elements of a row specified by /G flag and optionally the /P flag. |
| swap | Swaps image data following a 2D FFT. The transform swaps diagonal quadrants of the image in one or more planes. This keyword does not support any flags. The swapping is done in place and the source wave is overwritten. |
| swap3D | Swaps data following a 3D FFT. The transform swaps diagonal quadrants of the data. This keyword does not support any flags. The swapping is done in place and the source wave is overwritten. |
| transpose4D | Converts a 4D wave into a new 4D wave where the data are reordered by dimensions specified by the /TM4D flag. The results are stored in the wave M_4DTranspose in the current data folder. There is no option to overwrite the input wave so /O has no effect with transpose4D. |
|  | Added in Igor Pro 7.00. |
| transposeVol | Transposes a 3D wave. The transposed wave is stored in M_VolumeTranspose. The /O flag does not apply. The operation supports the following 5 transpose modes which are specified using the /G flag: |
|  |<table class="nested-table"><tbody><tr><td>***mode***</td><td>**equivalent command**</td></tr><tr><td>1:</td><td>M_VolumeTranspose=*imageMatrix* [p][r][q]</td></tr><tr><td>2:</td><td>M_VolumeTranspose=*imageMatrix* [r][p][q]</td></tr><tr><td>3:</td><td>M_VolumeTranspose=*imageMatrix* [r][q][p]</td></tr><tr><td>4:</td><td>M_VolumeTranspose=*imageMatrix* [q][r][p]</td></tr><tr><td>5:</td><td>M_VolumeTranspose=*imageMatrix* [q][p][r]</td></tr></tbody></table>
| vol2surf | Creates a quad-wave output (appropriate for display in Gizmo) that wraps around 3D "particles". A particle is defined as a region of nonzero value voxels in a 3D wave. The algorithm effectively computes a box at the resolution of the input wave which completely encloses the data. The output wave M_Boxy is a 2D single precision wave of 12 columns where each row corresponds to one disjoint quad and the columns provide the sequential X, Y and Z coordinates of the quad vertices. |
| voronoi | Computes the voronoi tesselation of a convex domain defined by the X, Y positions of the input wave. *imageMatrix* must be a triplet wave where the first column contains the X-values, the second column contains the Y-values and the third column is an arbitrary (zero is recommended) constant. The result of the operation is stored in the two column wave M_VoronoiEdges which contains sequential edges of the Voronoi polygons. Edges are separated from each other by a row of NaNs. The outer most polygons share one or more edges with a large triangle which contains the convex domain. |
|  | The operation creates two output waves: |
|  | M_Circles is a three column wave containing the center and radius of each natural neighborhood. The radius is correct only if equal scaling is applied. |
|  | M_DelaunayTriangles consists of 3 columns for the vertices of the triangles. Each triangle consists of 4 vertices. The 4th vertex is equal to the first. An extra row of NaNs used as a separator. |
|  | For an example, see ***Voronoi Tesselation Example*** below. |
|  | Voronoi interpolation is implemented in the [ImageInterpolate](/igorpro/commands/imageinterpolate.md) operation using the keyword Voronoi. |
| xProjection | Computes the projection in the X-direction and stores the result in the wave M_xProjection. See zProjection for more information. |
| xyz2rgb | Converts a 3D single precision XYZ color-space data into RGB based on the D65 white point. The transformation used is: |
|  | $$ \displaystyle \left[\begin{array}{l} R \\ G \\ B \end{array}\right]=\left[\begin{array}{rrr} 3.240479 & -1.537150 & -0.498535 \\ -0.969256 & 1.875992 & 0.041556 \\ 0.055648 & -0.204043 & 1.057311 \end{array}\right]\left[\begin{array}{l} x \\ y \\ z \end{array}\right] . $$ |
|  | If you do not specify the /O flag, the results are saved in a single precision 3D wave (NT_FP32) "M_XYZ2RGB". |
|  | Note that not all XYZ values map into positive RGB triplets (consider colors that reside outside the RGB triangle in the XYZ diagram). This operation gives you the following choices: by default, the output wave is a single precision wave that will include possible negative RGB values. If you specify the /U flag, for unsigned short output wave, the operation will set to zero all negative components and scale the remaining ones in the range [0,65535]. |
| yProjection | Computes the projection in the Y-direction and stores the result in the wave M_yProjection. See zProjection for more information. |
| zDot | Computes the dot product of the beam in *srcWave* with 1D zVector wave (specified with the /D flag). This will convert stacked images of spectral scans into RGB or XYZ depending on the scaling in zVector. The *srcWave* and zVector must be the same data type (float or double). The wave M_StackDot contains the result in the current data folder. |
| zProjection | Computes the projection in the z-direction and stores the result in the wave M_zProjection. The source wave must be a 3D wave of arbitrary data type. The value of the projection depends on the method specified via the /METH flag. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = {*azimuth*, *elevation* [, *shadingA*, *shadingB* ]}</span> |  |
|  | Specifies shading parameters. Position of the light source is given by *azimuth* (measured in degrees counter-clockwise) and *elevation* (measured in degrees above the horizon). |
|  | The parameters *shadingA* and *shadingB* are optional. By default their values are 1 and 0 respectively. |
| <span class="table-cell-nowrap">/Beam = {*row*,*column* }</span> |  |
|  | Designates a beam in a 3D wave; both *row* and *column* are zero based. |
| <span class="table-cell-nowrap">/BPJ = {*width, height* }</span> |  |
|  | Specifies the backprojection parameters *width* and *height*, which are the width and height of the reconstructed image and should be equal to the size of the original wave. |
| <span class="table-cell-nowrap">/C = *CMapWave*</span> | Specifies the cmap wave for cmap2rgb operation. The *CMapWave* is expected to be a 2D wave consisting of three columns corresponding to the RGB entries. |
| <span class="table-cell-nowrap">/CHIX = *chunkIndex*</span> |  |
|  | Identifies the chunk index for getting, inserting or setting a chunk of data in a 4D wave. *chunkIndex* ranges from 0 to the number of chunks in *imageMatrix*. |
| <span class="table-cell-nowrap">/CLAM = *fuzzy*</span> | Sets the value used to compute the fuzzy probability in fuzzyClassify. It must satisfy *fuzzy* > 1 (default is 2). |
| <span class="table-cell-nowrap">/CLAS = *num*</span> | Sets the number of requested classes in fuzzyClassify. If you don't know the number of expected classes and *num* is too high, fuzzyClassify will likely produce some degenerate classes. |
| <span class="table-cell-nowrap">/CPAD = {*np*, *mode*}</span> | Used with padImage this flag determines the size and mode of padding.  When *np* is negative, the operation removes abs(*np*) rows and columns from all sides of the image.  In this case the *mode* parameter is ignored.  When *np* is a positive integer, the operation adds *np* rows and *np* columns to both sides of the image.  The values of the newly added pixels are determined by the *mode* parameter.  When *mode*=0 the new pixels are set by reflecting the existing pixel values across the boundary.  When *mode*=1 the values of the boundary pixels are repeated for each new row/column. |
| <span class="table-cell-nowrap">/D = *waveName*</span> | Specifies a data wave. Check the appropriate keyword documentation for more information about this wave. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Creates or overwrites *destWave* with the first output wave from a keyword operation. Otherwise the default destination wave for the keyword is used. This flag specifically controls the first output wave produced by a keyword. If a keyword produces multiple output waves, /DSTB and /DSTC control the destination waves for the second and third output waves, respectively. The destination wave cannot be the source wave, and thus it cannot be used in combination with /O. |
| <span class="table-cell-nowrap">/DSTB = *destWave*</span> |  |
|  | Creates or overwrites the *destWave* with the second output wave from a keyword operation. Otherwise the default destination wave for the keyword is used. This can only be applied for keywords that produce at least two output waves. Use of /DSTB does not require use of /DEST. |
| <span class="table-cell-nowrap">/DSTC = *destWave*</span> |  |
|  | Creates or overwrites the *destWave* with the third output wave from a keyword operation. Otherwise the default destination wave for the keyword is used. This can only be applied for keywords that produce at least three output waves. Use of /DSTC does not require use of /DSTB and /DEST. |
| <span class="table-cell-nowrap">/F = *value*</span> | Increases the sampling in the angle domain when used with the Hough keyword. By default *value*=1 and the operation results in single degree increments in the interval 0 to 180, and if *value*=1.5 there will be 180*1.5 rows in the transform. |
|  | Specifies the outer pixel value surrounding the region of interest when used with shrinkRect keyword. |
| <span class="table-cell-nowrap">/FEQS</span> | When performing Voronoi tesselation, forces the algorithm to use equal scaling for both axes. Normally the scaling for each axis is determined from its range. When the ranges of the two axes are different by an order of magnitude or more, it is helpful to force the larger range to be used for scaling both axes. |
| <span class="table-cell-nowrap">/FREE</span> | Creates a free destination wave if it has been specified with one of the destination wave flags (/DEST, /DSTB, and /DSTC). For keywords that output multiple destination waves, only those specified using /DEST, /DSTB, or /DSTC will be free. Unspecified destination waves will be output as the default destination wave. |
| <span class="table-cell-nowrap">/G = *colNumber*</span> | Specifies either the row or column number used in connection with getRow or getCol keywords. This flag also specifies the transpose *mode* for the transposeVol keyword. |
| <span class="table-cell-nowrap">/H = {*minHue*,*maxHue* }</span> |  |
| <span class="table-cell-nowrap">/H = *hueWave*</span> | Specifies the range of hue values for selecting pixels. The hue values are specified in degrees in the range 0 to 360. Hue intervals that contain the zero point should be specified with the higher value first, e.g., /H={330,10}. |
|  | Use *hueWave* when you have more than one pair of values of hue that bracket the pixels that you want to select. |
| <span class="table-cell-nowrap">/I = *iterations*</span> | Sets the number of iterations in ccsubdivision and in fuzzyClassify. |
| <span class="table-cell-nowrap">/INSI = *imageWave*</span> |  |
|  | Specifies the wave, *imageWave*, to be used with the insertImage keyword. *imageWave* is a 2D wave of the same numeric data type as *imageMatrix*. |
| <span class="table-cell-nowrap">/INSW = *wave*</span> | Specifies the 2D wave to be inserted into a 3D wave using one of the keywords: insertXplane, insertYplane, or insertZplane. |
| <span class="table-cell-nowrap">/INSX = *xPos*</span> | Specifies the pixel position at which the first row is inserted. Ignores wave scaling. |
| <span class="table-cell-nowrap">/INSY = *yPos*</span> | Specifies the pixel position at which the first column is inserted. Ignores wave scaling. |
| <span class="table-cell-nowrap">/IOFF = {*dx*,*dy*,*bgValue*}</span> |  |
|  | Specifies the amount of positive or negative integer offset with *dx* and *dy* and the new background value, *bgValue*, with the offsetImage keyword. |
| <span class="table-cell-nowrap">/IWAV = *wave*</span> | Specifies the wave which provides the indices when used with the keyword indexWave. The wave should have as many columns as the dimensions of *imageMatrix* (2, 3, or 4). For example, to specify indices for pixels in an image, the wave should have two columns. The first column corresponds to the row designation and the second to the column designation of the pixel. The wave can be of any number type (other than complex) and entries are assumed to be integer indices; there is no support for interpolation or for wave scaling. |
| <span class="table-cell-nowrap">/L = {*minLight*, *maxLight* }</span> |  |
| <span class="table-cell-nowrap">/L = *lightnessWave*</span> |  |
|  | Specifies the range of lightness for selecting pixels. The lightness values are in the range 0 to 1. If you do not use the /L flag than the default full range is used. |
|  | Use *lightnessWave* when you have more than one pair of lightness values corresponding to the pixels that you want to select. In each pair the values should be arranged so that the smaller one is first and the larger is second. There is no restriction on the order of pairs in the wave except that they match the other waves used by the operation. |
| <span class="table-cell-nowrap">/LARA = *minPixels*</span> |  |
|  | SPecifies the minimum number of pixels required for an area to be masked by the findLakes keyword. If you do not specify this flag, the default value used is 100. |
| <span class="table-cell-nowrap">/LCVT</span> | use 8-connectivity instead of 4-connectivity. |
| <span class="table-cell-nowrap">/LRCT = {*minX*,*minY*,*maxX*,*maxY* }</span> |  |
|  | Sets the rectangular region of interest for the findLakes keyword. The operation will not affect the original data outside the specified rectangle. The X and Y values are the scaled values (i.e., using wave scaling). |
| <span class="table-cell-nowrap">/LTAR = *target*</span> | Sets the target value for the masked region in the findLakes keyword. |
| <span class="table-cell-nowrap">/LTOL = *tol*</span> | Specifies the tolerance for the findLakes keyword. By default the tolerance is zero. The tolerance must be a nonnegative number. The operation uses the tolerance by requiring neighboring pixels to have a value between that of the current pixel V and V+*tol*. |
| <span class="table-cell-nowrap">/M = *n*</span> | Specifies the method by which a 2D target image is filled with data from a 1D wave using fillImage. |
|  |<table class="nested-table"><tbody><tr><td>*n*&nbsp;=0:</td><td>Straight column fill that you can also accomplish by a redimension operation.</td></tr><tr><td>*n*&nbsp;=1:</td><td>Straight row fill.</td></tr><tr><td>*n*&nbsp;=2:</td><td>Serpentine column fill. The points from the data wave are sequentially loaded onto the first column and continue from the last to the first point of the second column, and then sequentially through the third column, etc.</td></tr><tr><td>*n*&nbsp;=3:</td><td>Serpentine row fill.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/METH = *method*</span> | Determines the values of the projected pixels in xProjection, yProjection and zProjection keywords. See zProjection for details. |
|  |<table class="nested-table"><tbody><tr><td>*method*&nbsp;=1:</td><td>Pixel (i,j) in M_zProjection is assigned the maximum value that (i,j,\*) takes among all layers of *imageMatrix* (default).</td></tr><tr><td>*method*&nbsp;=2:</td><td>Pixel (i,j) in M_zProjection is assigned the average value that (i,j,\*) takes among all layers of *imageMatrix*.</td></tr><tr><td>*method*&nbsp;=3:</td><td>Pixel (i,j) in M_zProjection is assigned the minimum value that (i,j,\*) takes among all layers of *imageMatrix*.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/METR = *method*</span> | Sets the metric used by the distance transform. Added in Igor Pro 7.00. |
|  |<table class="nested-table"><tbody><tr><td>*method*&nbsp;=0:</td><td>Manhattan distance. Default.</td></tr><tr><td>*method*&nbsp;=1:</td><td>Euclidean distance where the distance is measured between centers of pixels (assumed square).</td></tr><tr><td>*method*&nbsp;=2:</td><td>Euclidean distance that also takes into account actual pixel size using the input&#39;s wave scaling.</td></tr></tbody></table>
|  | *method* =0 executes faster than the other methods. *method* =2 can be 2x slower especially if different scaling is applied along the two axes. |
| <span class="table-cell-nowrap">/N = {*rowsToAdd*, *colsToAdd* }</span> |  |
|  | Creates an image that is larger or smaller by *rowsToAdd*, *colsToAdd*. The additional pixels are set by duplicating the values in the last row and the last column of the source image. |
|  | The result of the operation is saved in the wave M_paddedImage. |
| <span class="table-cell-nowrap">/N3DP = {dr, dc, dl}</span> |  |
|  | Specifies the number of rows (dr), columns (dc), and layers (dl) to add on each side of a 3D wave when used with the pad3d keyword. The output wave has dimensions (rows + 2*dr, cols + 2*dc, layers + 2*dl). Each value must be a non-negative integer strictly less than the corresponding source dimension. |
| <span class="table-cell-nowrap">/NCLR = *M*</span> | Specifies the maximum number of colors to find with the rgb2cmap keyword. *M* must be a positive number; the default value is 256 colors. |
| <span class="table-cell-nowrap">/NP = *numPlanes*</span> |  |
|  | Specifies the number of planes to remove from a 3D wave when using the removeXplane, removeYplane, or removeZplane keywords. Specifies the number of waves to be added to the stack with the stackImages keyword. |
| <span class="table-cell-nowrap">/O</span> | Overwrites the input wave with the result except in the cases of Hough transform and cmap2rgb. Does not apply to the transposeVol parameter. |
| <span class="table-cell-nowrap">/P = *planeNum*</span> | Specifies the plane on which you want to operate with the rgb2gray or with the getPlane methods. Also used for getRow or getCol if the source wave is 3D. |
| <span class="table-cell-nowrap">/PSL = {*xStart*,*dx*,*Nx*,*aStart*,*da*,*Na* }</span> |  |
|  | Specifies projection slice parameters. *xStart* is the first offset of the parallel rays measured from the center of the image. *dx* is the directed offset to the next ray in the fan and *Nx* is the number of rays in the fan. *aStart* is the first angle for which the projection is calculated. The angle is measured between the positive X-direction and the direction of the ray. *da* is the offset to the next angle at which the fan of rays is rotated and *Na* is the total number of angles for which the projection is computed. |
| <span class="table-cell-nowrap">/PTRF</span> | Use /PTRF with the ccsubdivision keyword to apply small perturbation to the input coordinates in order to break spatial degeneracies that may occur when multiple facets meet at some point in space. See ccsubdivision above for details. /PTRF was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/PTYP = *num*</span> | Specifies the plane (slice) to use with the getPlane keyword. |
|  |<table class="nested-table"><tbody><tr><td>*num*&nbsp;=0&nbsp;:</td><td>slice parallel to the XY plane.</td></tr><tr><td>*num*&nbsp;=1:</td><td>slice parallel to the XZ plane.</td></tr><tr><td>*num*&nbsp;=2:</td><td>slice parallel to the YZ plane.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Q</span> | Quiet flag. When used with the Hough transform, it suppresses report to the history of the angle corresponding to the maximum. |
| <span class="table-cell-nowrap">/R = *roiWave*</span> | Specifies a region of interest (ROI) defined by *roiWave*. For use with the keywords: averageImage, scalePlanes and selectColor. |
| <span class="table-cell-nowrap">/S = {*minSat*, *maxSat* }</span> |  |
| <span class="table-cell-nowrap">/S = *saturationWave*</span> |  |
|  | Specifies the range of saturation values for selecting pixels. The saturation values are in the range [0,1]. If you do not use the /S flag, the default value is the full saturation range. |
|  | Use *saturationWave* when you have more than one pair of saturation values. If you use a saturation wave you must also use a lightness wave (see /L). The saturation wave should consist of pairs of values where the first point is the lower saturation value and the second point is the higher saturation value. There is no restriction on the order of pairs within the wave. |
| <span class="table-cell-nowrap">/SEG</span> | Computes the segmentation image for fuzzyClassify. The image is stored in the 2D wave M_FuzzySegments. The value of each pixel is 255\**classIndex*/*number of classes*. Here *classIndex* is the index of the class to which the pixel belongs with the highest probability. |
| <span class="table-cell-nowrap">/T = *flag*</span> | Use one or more of the following flags. |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Swaps the data so that the DC is at the center of the image.</td></tr><tr><td>2:</td><td>Calculates the power defined as:</td></tr></tbody></table>
|  | P(f)= 0.5 \* [H(f)<sup>2</sup> + H(-f)<sup>2</sup>] |
| <span class="table-cell-nowrap">/TEXT = *val*</span> | Specifies the type of texture to create with the imageToTexture keyword. *val* is a binary flag that can be a combination of the following values: |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Truncates each dimension to the nearest power of 2, which is required for OpenGL textures.</td></tr><tr><td>2:</td><td>Creates a 1D texture (all other textures are for 2D applications).</td></tr><tr><td>4:</td><td>Creates a single channel texture suitable for alpha or luminance channels.</td></tr><tr><td>8:</td><td>Creates a RGB texture from a 3 (or more) layer data.</td></tr><tr><td>16:</td><td>Creates a RGBA texture. If *imageMatrix* does not have a 4th layer, alpha is set to 255.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/TM4D = *mode*</span> | Used with transpose4D to specify the format of the output wave. Here *mode* is a 4 digit integer that describes the mapping of the transformation. The digit 1 is used to represent the first dimension, 2 for the second, 4 for the third and 8 for the 4th dimension such that the original wave corresponds to mode=1248. All other modes are obtained by permuting one or more of the four digits and mode must consist of 4 distinct digits. |
|  | Added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/TOL = *tolerance*</span> | Sets the tolerance for iteration convergence with fuzzyClassify. Convergence is satisfied when the sum of the squared differences of all classes drops below *tolerance*, which must not be negative. |
| <span class="table-cell-nowrap">/U</span> | Creates an HSL wave of type unsigned short that contains values between 0 and 65535 when used with rgb2hsl keyword. |
| <span class="table-cell-nowrap">/W</span> | Pads the image by wrapping the data. If you are adding more rows or more columns than are available in the source wave, the operation cycles through the source data as many times as necessary. |
| <span class="table-cell-nowrap">/X = {*Nx*,*Ny*,*x1*,*y1*,*z1*,*x2*,*y2*,*z2*,*x3*,*y3*,*z3* }</span> |  |
|  | *Nx* and *Ny* are the rows and columns of the wave M_ExtractedSurface. The remaining parameters specify three 3D points on the extracted plane. The three points must be chosen at the vertices of the plane and entered in clock-wise order without skipping a vertex. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Examples* {#examples}
If you want to insert a 2D (M x N) wave, plane0, into plane number 0 of an (M x N x 3) wave, rgbWave:


```igor
ImageTransform /P=0/D=plane0 setPlane rgbWave
```

If your source wave is 100 rows by 100 columns and you want to create a montage of this image use:


```igor
ImageTransform /W/N={200,200} padImage srcWaveName
```

### *Hue and Saturation Segmentation Example* {#hue-and-saturation-segmentation-example}

```igor
Function HueSatSegment(hslW,lowH,highH,lowS,highS)
	Wave hslW

	Variable lowH,highH,lowS,highS
	Make/D/O/N=(2,3) conditionW
	conditionW={{lowH,highH},{lowS,highS},{NaN,NaN}}
	ImageTransform/D=conditionW matchPlanes hslW
	KillWaves/Z conditionW
End
```

### *Voronoi Tesselation Example* {#voronoi-tesselation-example}

```igor
Make/O/N=(33,3) ddd=gnoise(4)
ImageTransform voronoi ddd
Display ddd[][1] vs ddd[][0]
ModifyGraph mode=3,marker=19,msize=1,rgb=(0,0,65535)
AppendToGraph M_VoronoiEdges[][1] vs M_VoronoiEdges[][0]
SetAxis left -15,15
SetAxis bottom -5,10
```

### *References* {#references}
Born, Max, and Emil Wolf, *Principles of Optics*, 7th ed., Cambridge University Press, 1999.

Details about the rgb2i123 transform:

Gevers, T., and A.W.M. Smeulders, Color Based Object Recognition, *Pattern Recognition*, *32*, 453-464, 1999.

### *See Also* {#see-also}
[Image Processing](/igorpro/analysis/image-processing.md)

[Color Transforms](/igorpro/analysis/image-processing.md#color-transforms), [Handling Color](/igorpro/analysis/image-processing.md#handling-color), [General Utilities: ImageTransform Operation](/igorpro/analysis/image-processing.md#general-utilities-imagetransform-operation), [MatrixOp](/igorpro/commands/matrixop.md)

### *Demos* {#demos}
[Open Radon Transform Demo](#igor-pxp/Examples/Analysis/RadonTransformDemo.pxp)

[Open Fuzzy Classify Demo](#igor-pxp/Examples/Imaging/Fuzzy__Classify__Demo.pxp)