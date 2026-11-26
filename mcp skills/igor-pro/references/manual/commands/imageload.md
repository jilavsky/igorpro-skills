---
description: "The ImageLoad operation loads an image file into an Igor wave. It can load PNG, JPEG, BMP, TIFF, and Sun Raster files."
slug: /commands/imageload
---

<div className="command-signature">

## <strong>ImageLoad</strong>   [ <em>flags</em> ] [<em>fileNameStr</em> ] {#imageload}

</div>

The ImageLoad operation loads an image file into an Igor wave. It can load PNG, JPEG, BMP, TIFF, and Sun Raster files.

### *Parameters* {#parameters}
The file to be loaded is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If Igor cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

If you want to force a dialog to select the file, omit the *fileNameStr* parameter or pass "" for it.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/AINF</span> | Loads all of the image files in a disk folder into the current data folder. For example, if you have created an Igor symbolic path named ImagePath that points to a folder containing image files, you can execute: |
|  | <code class="igor">ImageLoad/P=ImagePath/T=TIFF/AINF</code> |
|  | When using /AINF, you must omit *fileNameStr* and you must include /T to specify the type of image file to be loaded. |
|  | This flag requires Igor Pro 7.03 or later. |
| <span class="table-cell-nowrap">/BIGT = *mode*</span> | When *mode* is 1, ImageLoad uses the LibTIFF library to load TIFF files.This is the default if you omit /BIGT. The LibTIFF library supports the traditional TIFF file format and the Big TIFF file format, which supports file sizes greater than 4 GB and files containing compressed data. |
|  | When *mode* is 0, ImageLoad uses Igor's internal TIFF code to load image data. This internal code does not support Big TIFF and is limited to file sizes less than 2 GB. |
|  | If you omit /BIGT, ImageLoad first attempts to load the file using LibTIFF. If an error occurs, it automatically attempt to load the file using Igor's internal TIFF code. |
|  | The  /SCNL, /STRP and /TILE flags require using LibTIFF. If you use any of these flags, /BIGT=1 is automatically in effect. |
|  | The /RAT and /RTIO flags require using Igor's internal TIFF code. If you use these flags, /BIGT=0 is automatically in effect. |
|  | See ***Loading TIFF Files*** below for more information about supported data types. |
| <span class="table-cell-nowrap">/C = *count*</span> | Specifies the number of images to load from a TIFF stack containing multiple images. The images are stored in individual waves if /LR3D is omitted or in a single 3D wave if /LR3D is present. |
|  | By default, Igor loads only a single image (i.e., /C=1). Use /C=-1 to load all images. The images must be either 8 bits, 16 bits, or 32 bits/pixel for this option. |
|  | To load a subset of the images in a TIFF stack, use /S to specify the starting image. |
|  | If you specify a *count* that exceeds the number of images in the file, ImageLoad loads all images beginning with the first image or the image specified by /S. |
| <span class="table-cell-nowrap">/G</span> | Displays the loaded image in a new image plot window. |
| <span class="table-cell-nowrap">/LR3D</span> | Specifies that the images in a TIFF stack are to be loaded into a 3D wave rather than into multiple 2D waves. This option works with grayscale images only, not with full color (e.g., RGB). |
|  | To load a subset of the images into the 3D wave, also use /S and /C. |
| <span class="table-cell-nowrap">/LTMD</span> | Reads data stored in TIFF tags belonging to the main Image File Directory. /LTMD works only when you use /BIGT=1 and is ignored otherwise. It was added in Igor Pro 8.00. |
|  | /LTMD creates a data folder named "Tag*n*" for each loaded image. The name of the data folder has the numeric suffix *n* starting from zero. |
|  | The "Tag*n*" data folder contains a text wave named T_Tags where each row contains the metadata associated with a single tag. The order of the rows in the wave T_Tags is indeterminate. |
|  | If you need to parse the metadata, you can search for the tag descriptor which always appears at the start of the line and is followed by a colon and one space (": "). |
| <span class="table-cell-nowrap">/N = *baseName*</span> | Stores the waves using *baseName* as the wave name. Only when *baseName* conflicts with an existing wave name will a numeric suffix be appended to the new wave names. |
|  | If you omit /N, ImageLoad uses the name of the file as the base name. |
| <span class="table-cell-nowrap">/O</span> | Overwrites an existing wave with the same name. |
|  | If you omit /O and there is an existing wave with the same name, a numeric suffix is appended to the image name to create a unique name. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/Q</span> | Quiet mode. Suppresses printing a description of loaded data to the history area. |
| <span class="table-cell-nowrap">/RAT</span> | Read All Tags reads all of the tags in a TIFF file into one or more waves. |
|  | If you use /RAT, /BIGT=0 is automatically in effect. To load tags with /BIGT=1, use /LTMD instead of /RAT. |
|  | /RAT creates a data folder named "Tag*n*" with a numeric suffix, *n* , starting from zero for each loaded image. When reading multiple images from a stack TIFF file, /RAT creates a corresponding number of data folders. |
|  | Each data folder contains a text wave named T_Tags consisting of 5 columns. The first row contains the offset of the current Image File Directory (IFD) from the start of the file. The remaining rows describe the individual TIFF Tags as they appear in the IFD. |
|  | The first column contains the tag number, the second contains the tag description, the third contains the tag type, the fourth contains the tag length, and the fifth contains either the value of the tag or a statement identifying the name of the wave in which the data was stored. For example, a simple tag that contains a single value has the form: |
|  | **Num**        **Desc**                **Type**        **Length**          **Value** |
|  | 256    IMAGEWIDTH           4               1                 2560 |
|  | A tag that contains more data, such as an array of values has the form: |
|  | **Num**        **Desc**                **Type**        **Length**          **Value** |
|  | 273    STRIPOFFSETS        4             -120           tifTag273 |
|  | Here the Length field is negative (-1\*realLength) and the Value field contains the name of the wave tifTag273 which contains the array of strip offsets. |
|  | When the Value field consists of ASCII characters it is stored in the T_Tags wave itself. All other types are stored in a wave in the same Tag data folder. |
|  | Private tags are usually designated by negative tag numbers. If their data type is anything other than ASCII, they are saved in separate waves. |
|  | In Igor Pro 9.01 and later, /RAT sets the S_dataFolder output variable to the path to the data folder where the tag information is stored. |
| <span class="table-cell-nowrap">/RONI</span> | Stores the number of images in a TIFF stack file in the variable V_numImages. No images are loaded from the file. This flag is not compatible with /BIGT=0. /RONI was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/RTIO</span> | Reads tag information only from a TIFF file. /RTIO is similar /RAT but it loads tag information only without loading any images. |
|  | If you use /RTIO, /BIGT=0 is automatically in effect. To load tags with /BIGT=1, use /LTMD instead of /RAT. |
|  | If you are loading a stack of images you can use the /C and /S flags to obtain tags from a specific range of images. |
| <span class="table-cell-nowrap">/S = *start*</span> | Specifies the first image to load from a TIFF stack containing multiple images. |
|  | *start* is zero-based and defaults to 0. |
|  | Use /C to specify the number of images to load. |
| <span class="table-cell-nowrap">/SCNL = *num*</span> | Reads the specified scanline from a TIFF file using LibTiff. |
|  | Added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/STRP = *num*</span> | Reads the specified strip from a TIFF file using LibTiff. |
|  | Added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/T = *type*</span> | Identifies what kind of image file to load. *type* is one of the following image file formats: |
|  |<table class="nested-table"><tbody><tr><td>***type***</td><td>**Loads This Type of Image**</td></tr><tr><td>any</td><td>Any graphic file type</td></tr><tr><td>bmp</td><td>Windows bitmap file</td></tr><tr><td>jpeg</td><td>JPEG file</td></tr><tr><td>png</td><td>PNG file</td></tr><tr><td>rpng</td><td>raw PNG file (see Details)</td></tr><tr><td>sunraster</td><td>SUN Raster file</td></tr><tr><td>tiff</td><td>TIFF file (see ***Loading TIFF Files*** below)</td></tr></tbody></table>
|  | If you omit /T or specify /T=any, Igor makes a guess based on the file name extension. ImageLoad reports an error if it is unable to determine the image file type. |
|  | /T=any allows the user to choose any file, regardless of its file name extension, if ImageLoad displays an Open File dialog. |
|  | When loading TIFF, we recommend that you use /T=tiff. See **Loading TIFF Files** below for details. |
| <span class="table-cell-nowrap">/TILE = *num*</span> | Reads the specified tile from a TIFF file using LibTiff. |
|  | Added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The name of the wave created by ImageLoad is based on the file name or on *baseName* if you provide the /N=*baseName* flag. In either case, if and only if there is a name conflict, ImageLoad appends a number to create a unique wave name.

If you use /P=*pathName* , note that it is the name of an Igor symbolic path, created via [NewPath](/igorpro/commands/newpath.md). It is not a file system path like "hd:Folder1:" or "C:\\\\Folder1\\\\". See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details.

### *Output Variables* {#output-variables}
ImageLoad sets the following variables:


|  |  |
| --- | --- |
| V_flag | 1 if the image was successfully loaded or to 0 otherwise. |
| S_fileName | Name of the file that was loaded. |
| S_path | File system path to the folder containing the file. S_path uses Macintosh path syntax (e.g., "hd:FolderA:FolderB:"), even on Windows. It includes a trailing colon. |
| V_numImages | Number of images loaded. Applies to TIFF files only. Also set by /RONI flag. |
| S_info | When using /BIGT=1 S_info contains the text stored in the IMAGEDESCRIPTION (270) TIFF tag. See /RAT and /LTMD above for other tag data. |
| S_dataFolder | Set by the /RAT flag to the path to the data folder where the tag information is stored. Added in Igor Pro 9.01. |
| S_waveNames | Semicolon-separated list of the names of loaded waves. |

### *Loading PNG Files* {#loading-png-files}
If you use /T=rpng ("raw PNG") or if you omit /T and the file has a ".png" extension, ImageLoad interprets the PNG file as raw data.

We recommend that you use /T=rpng and use /T=png only if /T=rpng does not produce the desired results.

/T=rpng creates an 8-bit or 16-bit unsigned integer wave with 1 to 4 layers.

PNG images with physical units produce waves with X and Y units of meters.

If a PNG image has a color table, ImageLoad creates two waves: a main image wave with one layer and a color table wave of the same name but with an "_pal" suffix. If the name is too long it creates a wave named *PNG_pal* instead.

### *Loading TIFF Files* {#loading-tiff-files}
ImageLoad/BIGT=0 supports 1-bit, 8-bit, 16-bit, 24-bit, and 32-bit TIFF files as well as floating point TIFFs.

- 1-bit/pixel images are loaded into a unsigned byte wave
- 8-bits/pixel images are loaded into into unsigned byte wave
- 16-bit/pixel images are loaded into into 16-bit unsigned waves
- 24-bit/pixel images and 32-bit/pixel images are loaded into into 3D RGB and RGBA waves respectively

ImageLoad/BIGT=1 supports the following data formats:

- 8-bit/sample signed or unsigned
- 12-bits/sample (packed into 16-bit unsigned)
- 16-bit/sample signed or unsigned
- 32-bit/sample IEEE single precision floating point, signed integer or unsigned integer
- 64-bit/sample IEEE double precision floating point, signed integer or unsigned integer

### *Loading a TIFF File With a Color Table* {#loading-a-tiff-file-with-a-color-table}
If your TIFF file includes a color table, ImageLoad/T=tiff/BIGT=0 loads the data into a 2D wave and loads the color table into a separate color table wave which can be used when creating an image plot.

If you want to load the TIFF file into a 3D RGB wave, use /T=tiff to load it into a 2D wave plus a color table wave and then use [ImageTransform](/igorpro/commands/imagetransform.md) cmap2RGB to create the 3D RGB wave.

### *Loading TIFF Stacks* {#loading-tiff-stacks}
A TIFF stack is a TIFF file that contains multiple images. When loading a stack, you can:

- Load all images
- Load a range of images specified by /S (starting image) and /C (image count)

You can also load the images into:

- Separate 2D waves by omitting the /LR3D flag
- A single 3D wave by using the /LR3D flag

	When you use /LR3D, ImageLoad stores each image from the TIFF file in a layer of the 3D output wave. This option works with grayscale images only, not with full color images (e.g., RGB).

### *EXIF Metadata* {#exif-metadata}
Some applications embed metadata (information about the image) in EXIF format. In both JPEG and TIFF files, the metadata is stored using TIFF tags. To read the metadata, use the /RAT flag, even if you are loading a JPEG file.

### *Examples* {#examples}

```igor
// Load all images from a TIFF stack into separate 2D waves
ImageLoad /C=-1 /T=TIFF

// Load a single image from a TIFF stack into a 2D wave
ImageLoad/S=10/C=1/T=TIFF	// Load image 10 (zero based)

// Load all images from a TIFF stack into a single 3D wave
ImageLoad/LR3D/S=0/C=-1/T=TIFF 

// Read all tags without loading any images
ImageLoad/C=-1/T=TIFF/RTIO	

// Get the number of images in a TIFF stack
NewDataFolder/O/S tmp
ImageLoad/C=-1/T=TIFF/RTIO
Print V_numImages
KillDataFolder :
```

### *See Also* {#see-also}
[Loading Image Files](/igorpro/data/importing-and-exporting-data.md#loading-image-files)

[ImageSave](/igorpro/commands/imagesave.md) for saving waves as image files.