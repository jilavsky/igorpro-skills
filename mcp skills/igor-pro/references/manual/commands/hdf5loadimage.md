---
description: "The HDF5LoadImage operation loads an image dataset and in some cases a palette dataset from an HDF5 file using the format specified in the HDF5 Image and…"
slug: /commands/hdf5loadimage
---

<div className="command-signature">

## <strong>HDF5LoadImage</strong>  [ /CMDL=<em>colorModelStr</em> /GRPH=<em>showInGraph</em> /N=<em>name</em> /O /PAL=<em>paletteNumber</em> /PALN=<em>palNameStr</em> /SCLI={<em>offset</em>, <em>multiplier</em>, <em>min</em>, <em>max</em>, <em>round</em>} /SCLP={<em>offset</em>, <em>multiplier</em>, <em>min</em>, <em>max</em>, <em>round</em>} /Q /Z ] <em>locationID</em>, <em>nameStr</em> {#hdf5loadimage}

</div>

The HDF5LoadImage operation loads an image dataset and in some cases a palette dataset from an HDF5 file using the format specified in the HDF5 Image and Palette Specification version 1.2. This format is described at:

[https://support.hdfgroup.org/documentation/hdf5/latest/_i_m_g.html](https://support.hdfgroup.org/documentation/hdf5/latest/_i_m_g.html)

HDF5LoadImage attempts to create an Igor 2D wave and in some cases a corresponding palette wave which, when displayed in an Igor image plot, most closely represents the image defined by the HDF5 dataset.

Because the HDF5 specification has some features that Igor lacks, and vice versa, in some cases this requires massaging the image data after loading it from the HDF5 file. Thus the data in the Igor wave created by HDF5LoadImage may not be identical to the data in the HDF5 dataset.

If you want the Igor wave to be an exact copy of the HDF5 image dataset, you must use [HDF5LoadData](/igorpro/commands/hdf5loaddata.md) instead of HDF5LoadImage.

HDF5LoadImage does an automatic transposition so that an image viewed in Igor has the same orientation as in HDFView and most other programs. See [HDF5 Images Versus Igor Images](/igorpro/data/igor-hdf5-guide.md#hdf5-images-versus-igor-images) for details.

Depending on the subclass of the HDF5 image, HDF5LoadImage may create just an image wave or both an image wave and a palette wave. This is explained below in the details section.

You can control scaling of data and color conversion using the /SCLI, /SCLP and /CMDL flags.

By default, the name of the loaded wave is a possibly cleaned up version of the name of the dataset being loaded.

### *Parameters* {#parameters}
*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*nameStr* is a string containing the name of the image dataset to be loaded. This can be a full HDF5 path or partial HDF5 path or simple name relative to *locationID*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CMDL = *colorModelStr*</span> | Controls color model conversions for `IMAGE_INDEXED` and `IMAGE_TRUECOLOR` images. For most purposes you should use /CMDL="PerFile". |
|  | *colorModelStr* = "PerFile": Convert from the color model specified in the HDF5 file to RGB. The color model is specified by an `IMAGE_COLORMODEL` attribute of the image dataset or by a `PAL_COLORMODEL` attribute of the palette dataset. If these attributes are missing, no conversion is done. |
|  |<table class="nested-table"><tbody><tr><td>*colorModelStr*&nbsp;=&nbsp;&quot;None&quot;:</td><td>Do not do any color model conversions. This is the default behavior used if /CMDL is not specified.</td></tr><tr><td>*colorModelStr*&nbsp;=&nbsp;&quot;RGB&quot;:</td><td>Convert from RGB to RGB. This is a NOP.</td></tr><tr><td>*colorModelStr*&nbsp;=&nbsp;&quot;YUV&quot;:</td><td>Convert from YUV to RGB.</td></tr><tr><td>*colorModelStr*&nbsp;=&nbsp;&quot;CMY&quot;:</td><td>Convert from CMY to RGB.</td></tr><tr><td>*colorModelStr*&nbsp;=&nbsp;&quot;CMYK&quot;:</td><td>Convert from CMYK to RGB.</td></tr><tr><td>*colorModelStr*&nbsp;=&nbsp;&quot;YCbCr&quot;:</td><td>Convert from YCbCr to RGB.</td></tr><tr><td>*colorModelStr*&nbsp;=&nbsp;&quot;HSV&quot;:</td><td>Convert from HSV to RGB.</td></tr></tbody></table>
|  | Note that color model conversions are approximations. |
|  | In the case of CMYK to RGB when loading a palette dataset, if the palette dataset has exactly 4 columns, HDF5LoadImage removes the fourth column from the loaded palette wave after doing the conversion. |
|  | In the case of CMYK to RGB when loading an image dataset, if the image dataset has exactly 4 layers, HDF5LoadImage removes the fourth layer from the loaded image wave after doing the conversion. |
| <span class="table-cell-nowrap">/GRPH = *showInGraph*</span> | *showInGraph =* 0: Do not show loaded image wave in a new image plot graph. This is the default behavior. |
|  |<table class="nested-table"><tbody><tr><td>*showInGraph&nbsp;=*&nbsp;1:</td><td>Always show loaded image wave in a new image plot graph.</td></tr><tr><td>*showInGraph&nbsp;=*&nbsp;2:</td><td>Append loaded image wave as image plot to top graph. If there are no graphs, a new graph is created as if *showInGraph* were 1.</td></tr><tr><td>*showInGraph&nbsp;=*&nbsp;3:</td><td>Same as *showInGraph* = 1 except if the loaded image wave existed prior to the call to HDF5LoadImage in which case it acts like *showInGraph* = 0.</td></tr><tr><td>*showInGraph&nbsp;=*&nbsp;4:</td><td>Same as *showInGraph* = 2 except if the loaded image wave existed prior to the call to HDF5LoadImage in which case it acts like *showInGraph* = 0.</td></tr></tbody></table>
|  | The /GRPH flag is ignored when HDF5LoadImage is called from a preemptive thread. |
| <span class="table-cell-nowrap">/N = *name*</span> | *name* is the name to be used for the loaded image wave. If /N is omitted, the name used is a possibly cleaned up version of the name of the image dataset. |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing waves in case of a name conflict. If /O is omitted, HDF5LoadImage choose names that don't conflict with existing objects. |
| <span class="table-cell-nowrap">/PAL = *paletteNumber*</span> | *paletteNumber* is a zero-based index that indicates which palette dataset should be used to interpret the colors in the image dataset. The default value is zero. |
|  | This is used only for image datasets that have `PALETTE` attributes that refer to multiple palette datasets. |
|  | *paletteNumber* is clipped to n-1 where n is the number of palette datasets actually referenced by the image dataset. |
| <span class="table-cell-nowrap">/PALN = *palNameStr*</span> | *palNameStr* is a string containing the name to be used for the palette wave if a palette wave is created. |
|  | If /PALN is omitted or if *palNameStr* is "", we would like to use the name of the HDF5 palette dataset as the palette wave name. However, for technical reasons HDF5LoadImage has no simple way of determining the name of the palette dataset. Therefore it generates a palette wave name by concatenating "Pal" to the image wave name. |
| <span class="table-cell-nowrap">/SCLI = {*offset*, *multiplier*, *min*, *max*, *round*}</span> |  |
|  | Controls the scaling of image data. In Igor, 8-bit color data is assumed to be scaled from 0 to 255. 16-bit or greater color data is assumed to be scaled from 0 to 65535. The /SCLI flag allows you to compensate if the data being loaded is scaled differently. |
|  | If /SCLI is omitted, HDF5LoadImage behaves as if /SCLI={0, 0, -INF, INF, 0} were specified. This does default scaling, no clipping and no rounding. |
|  | If *offset* is 0.0 and *multiplier* is 1.0, no scaling is done. |
|  | If *offset* and *multiplier* are zero, default scaling is done. "Default" means that the data is scaled to Igor's standard range of 0..255 for 8-bit data or 0..65535 for all other data.
|  | <div><Admonition type="note"><p>This is currently not implemented because the HDF5 Image and Palette 2.0 specification provides no way for HDF5LoadImage to determine the full scale value of the image dataset in the HDF5 file.</p></Admonition></div> |
|  | For other values of *offset* and *multiplier*, HDF5LoadImage performs the following transformation: |
|  | <code class="igor">out = (in + offset) \* multiplier</code> |
|  | If *min* is -INF and *max* is +INF, no clipping is done. If both *min* and *max* are zero, the result is clipped to the minimum and maximum value that can be stored for integer data types and not clipped at all for floating point data types. Otherwise the output value is clipped to be between *min* and *max*. |
|  | If *round* is non-zero, the result is rounded to the nearest integer. |
| <span class="table-cell-nowrap">/SCLP = {*offset*, *multiplier*, *min*, *max*, *round*}</span> |  |
|  | Controls the scaling of palette data, if any. In Igor, 8-bit color data is assumed to be scaled from 0 to 255. 16-bit or greater color data is assumed to be scaled from 0 to 65535. The /SCLP flag allows you to compensate if the data being loaded is scaled differently. |
|  | If /SCLP is omitted, HDF5LoadImage behaves as if /SCLP={0, 0, -INF, INF, 0} were specified. This does default scaling, no clipping and no rounding. |
|  | If *offset* is 0.0 and *multiplier* is 1.0, no scaling is done. |
|  | If *offset* and *multiplier* are zero, default scaling is done. "Default" means that the data is scaled to Igor's standard range of 0..255 for 8-bit data or 0..65535 for all other data. HDF5LoadImage determines the full scale value of the palette dataset in the HDF5 file by examining the `PAL_MINMAXNUMERIC` attribute. If this attribute is missing, then the full scale value of the palette dataset is assumed to be the full range of its data type (e.g., 0..255 for an 8-bit palette). |
|  | For other values of *offset* and *multiplier*, HDF5LoadImage performs the following transformation: |
|  | <code class="igor">out = (in + offset) \* multiplier</code> |
|  | If *min* is -INF and *max* is +INF, no clipping is done. If both *min* and *max* are zero, the result is clipped to the minimum and maximum value that can be stored for integer data types and not clipped at all for floating point data types. Otherwise the output value is clipped to be between *min* and *max*. |
|  | If *round* is non-zero, the result is rounded to the nearest integer. |
| <span class="table-cell-nowrap">/Q</span> | Be quiet. Suppresses normal diagnostic messages. |
| /T=*showInTable* |<table class="nested-table"><tbody><tr><td>*showInTable&nbsp;=*&nbsp;0:</td><td>Do not show loaded waves in table.</td></tr><tr><td>*showInTable&nbsp;=*&nbsp;1:</td><td>Show loaded waves in a new table.</td></tr><tr><td>*showInTable&nbsp;=*&nbsp;2:</td><td>Append loaded waves to top table.</td></tr></tbody></table>
|  | If *showInTable* is 2 but there are no tables, a new table is created as if *showInTable* were 1. |
|  | The /T flag is ignored when HDF5LoadImage is called from a preemptive thread. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Details* {#details}
The HDF5 Image and Palette Specification version 1.2 says that an image dataset of subclass other than `IMAGE_TRUECOLOR` can be 2D or 3D with one element in the third dimension. When HDF5LoadImage loads such an image dataset, it always creates a 2D wave.

The specification does not say what to do if the image dataset has more elements than required to define a single image, for example, an indexed image of dimensions 5x4x10. HDF5LoadImage treats this as a stack of images and creates a 3D wave with 10 layers. 4D datasets are also treated as stacks of images. True color image datasets with extra elements or dimensions are treated similarly, as a set of true color images.

### *IMAGE_TRUECOLOR Data Scaling* {#image_truecolor-data-scaling}
The specification does not say how to interpret the scaling of `IMAGE_TRUECOLOR` data. This is what Igor calls "direct" color. Empirically, 8-bit HDF5 datasets use 0-255 to represent min/max for each element. This is also how Igor interprets 8-bit direct color data.

The specification does not say how to interpret the scaling of `IMAGE_TRUECOLOR` data greater than 8 bits. Igor expects such data to use 0-65535 to represent min/max for each element for all color data greater than 8 bits.

Since HDF5LoadImage has no way to know how `IMAGE_TRUECOLOR` data is scaled, it does nothing and leaves it to you to scale the data if necessary, either by using the /SCLI flag or by scaling it after you load it. This generally is not be required for 8-bit data, which is the most common form, but might be required for higher resolution data.

### *Output Variables* {#output-variables}
HDF5LoadImage sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |
| S_waveNames | Set to a semicolon-separated list of the loaded waves. The first item is the name of the image wave. If a palette wave was loaded there is a second item, the name of the palette wave. |

### *See Also* {#see-also}
[HDF5CreateFile](/igorpro/commands/hdf5createfile.md), [HDF5OpenFile](/igorpro/commands/hdf5openfile.md), [HDF5CloseFile](/igorpro/commands/hdf5closefile.md), [HDF5FlushFile](/igorpro/commands/hdf5flushfile.md), [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md), [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md), [HDF5CloseGroup](/igorpro/commands/hdf5closegroup.md), [HDF5SaveImage](/igorpro/commands/hdf5saveimage.md)

See [HDF5 Images Versus Igor Images](/igorpro/data/igor-hdf5-guide.md#hdf5-images-versus-igor-images) for special considerations when loading images.