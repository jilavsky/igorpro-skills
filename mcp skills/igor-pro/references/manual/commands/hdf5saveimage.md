---
description: "The HDF5SaveImage operation saves an image dataset and in some cases a palette dataset in an HDF5 file using the format specified in the HDF5 Image and…"
slug: /commands/hdf5saveimage
---

<div className="command-signature">

## <strong>HDF5SaveImage</strong>  [ /COMP=<em>compatibility</em> /CTAB={<em>colorTable</em>, <em>zMin</em>, <em>zMax</em>, <em>reverse</em>} /DIR /GRAY /O /PALD=<em>palDatasetStr</em> /PALN=<em>palNameStr</em> /PALW=<em>paletteWave</em> /Z ] <em>wave</em>, <em>locationID</em> [, <em>nameStr</em> ] {#hdf5saveimage}

</div>

The HDF5SaveImage operation saves an image dataset and in some cases a palette dataset in an HDF5 file using the format specified in the HDF5 Image and Palette Specification version 1.2. This format is described at:

[http://support.hdfgroup.org/documentation/hdf5/latest/_i_m_g.html](http://support.hdfgroup.org/documentation/hdf5/latest/_i_m_g.html)

HDF5SaveImage attempts to create an HDF5 image dataset and corresponding palette dataset which, when interpreted according to the specification, most closely represents the image wave as it would appear in an Igor image plot.

When using an Igor color table (/CTAB flag) or palette wave (/PALW flag), in some cases this requires massaging the image data before writing it to the HDF5 file. Thus the HDF5 image dataset may not be identical to the Igor image wave.

If you want the HDF5 image dataset to be an exact copy of the Igor image wave, you must use the grayscale method (/GRAY flag) or the direct color method (/DIR flag) or use [HDF5SaveData](/igorpro/commands/hdf5savedata.md) instead of HDF5SaveImage.

When you display an image plot in Igor, you can specify X and Y waves which control the width and height of an image elements on an element-by-element basis. Neither the HDF5 specification nor HDF5SaveImage supports this feature.

Igor supports four image display modes: false color (colors defined by a built-in color table), indexed color (colors defined by a palette wave), direct color (colors specified by direct RGB values) and explicit color (colors defined by a list of specific RGB colors). HDF5SaveImage supports the all of these except explicit color.

When you display an image in Igor using false color or indexed color you can specify that certain special data values be mapped to specified colors or to transparency. HDF5SaveImage does not support this.

HDF5SaveImage does an automatic transposition so that an image viewed in Igor has the same orientation when viewed in HDFView and most other programs. See [HDF5 Images Versus Igor Images](/igorpro/data/igor-hdf5-guide.md#hdf5-images-versus-igor-images) for details.

If you use the /CTAB or /PALW flags, HDF5SaveImage writes both an image dataset and a palette dataset. Otherwise it writes just an image dataset.

HDF5SaveImage always uses the RGB color model when saving palette datasets and associated image datasets.

### *Parameters* {#parameters}
*wave* is the name of or path to the wave containing the image data to be saved.

*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*nameStr* is an optional string containing the name of the image dataset to be created. This can be a full HDF5 path or partial HDF5 path or simple name relative to *locationID*. All groups referenced by *nameStr* must already exist.

If *nameStr* is omitted, the image dataset is saved in the group specified by *locationID* using the same name as the wave name.

### *Flags* {#flags}

|  |  |
| --- | --- |
| /COMP=*compatibility* |<table class="nested-table"><tbody><tr><td>*compatibility*&nbsp;=&nbsp;0:</td><td>Don&#39;t use any special compatibility settings (default).</td></tr><tr><td>*compatibility*&nbsp;=&nbsp;1:</td><td>Write the palette dataset to be compatible with HDFView 2.0.</td></tr></tbody></table>
|  | HDFView 2.0 requires that palette datasets consist of unsigned 8-bit data (unsigned char) and have 256 rows. When this setting is used, HDF5SaveImage writes 8-bit palette data and pads the palette dataset up to 256 rows if it would normally be smaller. |
|  | Neither of these palette restrictions is required by the HDF5 Image and Palette Specification version 1.2. They are a limitation of HDFView 2.0 and possibly of other HDF5 image viewers. Future versions of HDFView might remove these limitations. |
|  | Since using the /COMP flag forces writing the image data set using unsigned character data, color precision may be lost in the process of saving the image in the HDF5 file. |
| <span class="table-cell-nowrap">/CTAB = {*colorTable*, *zMin*, *zMax*, *reverse*}</span> |  |
|  | Use this flag to save an image displayed as false color in Igor, that is, displayed using a built-in Igor color table. |
|  | *colorTable* is the name of an Igor color table which is used to create a palette that is saved in the HDF5 file. |
|  | The image is saved as an HDF5 indexed color image (IMAGE_SUBCLASS="IMAGE_INDEXED"). |
|  | *zMin* is the value in *wave* which should be displayed using the first entry in the color table (or the last entry if *reverse* is 1). If you pass NaN for *zMin*, *zMin* is treated as 0.0. |
|  | *zMax* is the value in *wave* which should be displayed using the last entry in the color table (or the first entry if *reverse* is 1). If you pass NaN for *zMax*, *zMax* is treated as n-1 where n is the number of entries in the color table. |
|  | *reverse* is 1 to reverse the color table when writing the palette dataset or 0 otherwise. |
|  | When Igor displays an image using a color table, it scales the data in the image wave based on specified zMin and zMax parameters and then rounds to produce integer indices into the color table. The HDF5 Image and Palette Specification version 1.2 does not provide for this kind of scaling. Therefore when writing an image dataset using /CTAB, HDF5SaveImage scales and rounds the dataset's data values to produce integer color table indices. This is the same scaling and rounding is done by Igor when it uses the color table to display a 2D wave as an image. |
|  | The following shortcut syntax: |
|  | `/CTAB=colorTable` |
|  | is equivalent to: |
|  | `/CTAB={colorTable, 0, n-1, 0}` |
|  | which is equivalent to: |
|  | `/CTAB={colorTable, NaN, NaN, 0}` |
|  | The shortcut form is appropriate if the values in *wave* are already scaled as 0-based integer indices into the color table. |
|  | *wave* must be 2D or higher and is treated as a single image or a stack of images if there are more elements than required for a single image. |
| <span class="table-cell-nowrap">/DIR</span> | Use this flag to save an image displayed as direct color in Igor, that is, when the wave contains direct RGB values. |
|  | The image is saved as an HDF5 true color image (IMAGE_SUBCLASS="IMAGE_TRUECOLOR") using the RGB color model. |
|  | *wave* must be 3D or 4D. |
|  | 3D waves must have dimensions N x M x 3k. If k is greater than 1 then HDF5SaveImage treats the wave as a set of k RGB images. If wave is 4D, it is also treated as a set of RGB images. |
|  | The three layers are treated as R, G and B planes. |
| <span class="table-cell-nowrap">/GRAY</span> | Use this flag to save an image without any information specifying what colors are to be used to display it. |
|  | The image is saved as an HDF5 grayscale image (IMAGE_SUBCLASS="IMAGE_GRAYSCALE"). |
|  | *wave* must be 2D or higher and is treated as a single image or a stack of images if there are more elements than required for a single image. |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing datasets in case of a name conflict. If /O is omitted and the dataset already exists, HDF5SaveImage returns an error. |
| <span class="table-cell-nowrap">/PALD = *palDatasetStr*</span> | *palDatasetStr* is a string containing the name of or path to an existing HDF5 dataset that is to serve as the palette for the image dataset being written. |
|  | The purpose of this flag is to allow you to write multiple image datasets that reference the same palette dataset. |
|  | The existing palette dataset must already have the appropriate attributes to serve as a palette. Usually the existing dataset is one that was created by a preceding call to HDF5SaveImage with the /PALW flag. |
|  | Also the data in *wave* must be already scaled as indices into the palette. |
| <span class="table-cell-nowrap">/PALN = *palNameStr*</span> | *palNameStr* is a string containing the name to be used for the palette dataset in the HDF5 file when /CTAB or /PALW is used. If /PALN is omitted or *palNameStr* is empty ("") then HDF5SaveImage uses the color table name or palette wave name as the palette dataset name. |
| <span class="table-cell-nowrap">/PALW = *paletteWave*</span> | Use this flag to save an image displayed as indexed color in Igor, that is, when the wave contains indices into another wave acting as a palette. |
|  | *paletteWave* is the Igor wave containing the palette data that is used to save the palette dataset in the HDF5 file. |
|  | When Igor displays an image using a palette wave, it interprets the data in the image wave as X indices into the palette wave. However in the HDF5 Image and Palette Specification version 1.2, the image dataset values are interpreted as integer indices into the palette dataset. Therefore when writing an image dataset using /PALW, HDF5SaveImage scales and rounds the dataset's data values to produce integer palette indices. This is the same scaling and rounding done by Igor when it uses the palette wave to display a 2D wave as an image. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Details* {#details}
In the HDF5 Image and Palette Specification version 1.2, there are four subclasses of images: `IMAGE_GRAYSCALE` (a bitmap without a palette), `IMAGE_BITMAP` (not clearly defined by the specification), `IMAGE_INDEXED` (a bitmap containing indices into a palette) and `IMAGE_TRUECOLOR` (a bitmap in which explicit colors are represented).

The /GRAY, /CTAB, /PALD, /PALW and /DIR flags control how an Igor image is saved as an HDF5 image. One and only one of these flags must be present.

In all cases, the image dataset's data comes from the *wave* parameter which must specify a 2D or higher wave except when /DIR is used, in which case it must be 3D or higher.

There are ambiguities regarding palettes in the HDF5 Image and Palette Specification version 1.2 and the implementation of images that use palettes in the HDF Group's HDFView 2.0 program (and probably other viewers) is inconsistent. Consequently you get the most reliable results using the /DIR flag to create an image of subclass `IMAGE_TRUECOLOR`.

The following paragraphs explain when a palette dataset is saved and/or associated with the image dataset.

If /GRAY is used the HDF5 image subclass is `IMAGE_GRAYSCALE` and no HDF5 palette dataset is involved.

If /CTAB is used the HDF5 image subclass is `IMAGE_INDEXED`. HDF5SaveImage creates the HDF5 palette dataset from the Igor color table specified by /CTAB using the name of the color table or the name specified by /PALN.

If /PALW is used the HDF5 image subclass is `IMAGE_INDEXED`. HDF5SaveImage creates the HDF5 palette dataset from the wave specified by /PALW using the name of that wave or the name specified by /PALN.

If /PALD is used the HDF5 image subclass is `IMAGE_INDEXED`. HDF5SaveImage creates no HDF5 palette dataset but creates an image dataset PALETTE attribute which identifies the dataset specified by the /PALD flag as the palette. The palette dataset must already have the required palette attributes.

If /DIR is used the HDF5 image subclass is `IMAGE_TRUECOLOR` and no HDF5 palette dataset is required.

In Igor, color components use the range 0..255 for byte data and 0..65535 for any other type of data.

### *Mapping Igor Color Modes to HDF5SaveImage Modes* {#mapping-igor-color-modes-to-hdf5saveimage-modes}
In Igor there are four ways to represent an image:

|  |
| --- |
| False Color: |A 2D wave and a color table.
|  | The mapping of the values in the 2D wave into the color table is controlled by the ctab keyword of the ModifyImage operation. |  |
|  | Use the /CTAB flag for this kind of image. HDF5SaveImage treats your image as false color and saves it as an HDF5 indexed color image (IMAGE_SUBCLASS="IMAGE_INDEXED"). HDF5SaveImage creates two datasets: an image dataset and a palette dataset. |
|  | *wave* must be 2D or higher and is treated as a single image or a stack of images if there are more elements than required for a single image. |
| Indexed Color: | A 2D wave and a palette wave. |
|  | The values in the 2D wave are interpreted as X indices into the palette wave so the mapping takes into account the palette wave's X scaling property. |
|  | Use the /PALW flag for this kind of image. HDF5SaveImage treats your image as indexed color and saves it as an HDF5 indexed color image (IMAGE_SUBCLASS="IMAGE_INDEXED"). HDF5SaveImage creates two datasets: an image dataset and a palette dataset. The data stored in the image dataset is scaled, if necessary, so that it represents integer indices into the palette dataset. |
|  | *wave* must be 2D or higher and is treated as a single image or a stack of images if there are more elements than required for a single image. |
| Direct Color: | A 3D wave containing a red plane, a blue plane and a green plane. |
|  | The values in the 3D wave are treated as hard-coded RGB colors. |
|  | Use the /DIR flag for this kind of image. HDF5SaveImage treats your image as direct color and saves it as an HDF5 "true" color image (IMAGE_SUBCLASS="IMAGE_TRUECOLOR") with an interlace mode set to "INTERLACE_PLANE". HDF5SaveImage creates only the image dataset. No palette is required. |
|  | *wave* must be 3D or 4D. |
|  | 3D waves must have dimensions N x M x 3k. If k is greater than 1 then HDF5SaveImage treats the wave as a set of k RGB images. If wave is 4D, it is also treated as a set of RGB images. |
|  | The planes represent R, G and B. |
| Explicit Color: | A 2D wave and a list of colors. |
|  | HDF5SaveImage does not support explicit color images. |

### *Output Variables* {#output-variables}
HDF5SaveImage sets the following output variable:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |

### *Example* {#example}

```igor
Function TestSaveImage(w, palW, format, compatibility)
	Wave w
	Wave palW
	String format
	Variable compatibility

	Variable result = 0	// 0 means no error
	
	Variable fileID
	HDF5CreateFile/P=home /O /Z fileID as "Test.h5"
	if (V_flag != 0)
		Print "HDF5CreateFile failed"
		return -1
	endif

	strswitch(format)
		case "GrayScale":
			HDF5SaveImage /COMP=(compatibility) /GRAY w, fileID
			break

		case "FalseColor":
			HDF5SaveImage /COMP=(compatibility) /CTAB=Rainbow256 w, fileID
			break

		case "IndexedColor":
			HDF5SaveImage /COMP=(compatibility) /PALW=palW w, fileID
			break

		case "DirectColor":
			HDF5SaveImage /COMP=(compatibility) /DIR w, fileID
			break
	endswitch

	if (V_flag != 0)
		Print "HDF5SaveImage failed"
		result = -1
	endif
	
	HDF5CloseFile fileID
	
	return result
End
```

### *See Also* {#see-also}
[HDF5LoadImage](/igorpro/commands/hdf5loadimage.md), [HDF5SaveData](/igorpro/commands/hdf5savedata.md), [HDF5SaveGroup](/igorpro/commands/hdf5savegroup.md)

See [HDF5 Images Versus Igor Images](/igorpro/data/igor-hdf5-guide.md#hdf5-images-versus-igor-images) for special considerations when saving images.