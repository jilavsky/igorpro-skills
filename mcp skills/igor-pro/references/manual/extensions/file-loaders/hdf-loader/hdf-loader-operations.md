---
description: "The HDFInfo operation provides information about the contents of the specified HDF file."
slug: /extensions/file-loaders/hdf-loader/hdf-loader-operations
---

<div className="command-signature">

## <strong>HDFInfo</strong>  [ /P=<em>pathName</em>  /Q ] [ <em>keyword</em> =<em>value</em>, <em>keyword</em> =<em>value</em>, ]  [<em>fileNameStr</em> ] {#hdfinfo}

</div>

The HDFInfo operation provides information about the contents of the specified HDF file. Typically you'd use this operation to list the components of the HDF file, obtain their reference numbers and then use another operation to read the actual data that you are interested in. Unless otherwise specified below, the output is printed in Igor's history area.

If you use one or more keywords, you must include a comma before *fileNameStr* .

### *Parameters* {#parameters}
If *fileNameStr* is omitted or is "", HDFInfo displays an open-file dialog.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for *fileNameStr.* |
| <span class="table-cell-nowrap">/Q</span> | Suppresses text output to the history window. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">Tag = *tag*</span> | Get information about the element with tag=*tag.*  Used only in conjunction with certain other keywords, as described below. |
| <span class="table-cell-nowrap">Ref = *num*</span> | Get information about the element with reference number=*num.*  Used only in conjunction with certain other keywords, as described below. |
| <span class="table-cell-nowrap">Mode = m</span> | The following 9 modes can be specified using the corresponding keywords. All combination of modes can also be achieved using the key word Mode set equal to the sum of the required modes. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Default. Lists information on all elements in the file.</td></tr><tr><td>1:</td><td>Lists the reference number of all elements whose tag is specified by the Tag keyword.</td></tr><tr><td>2:</td><td>Lists the tags for all elements whose reference number is specified by the Ref keyword.</td></tr><tr><td>4:</td><td>Lists output in a numeric wave named HDF_List instead of in the history. Use this in conjunction with mode=1 or mode=2.</td></tr><tr><td>16:</td><td>Includes a description of the tag when listing. Use in conjunction with mode=1 or mode=2.</td></tr><tr><td>32:</td><td>Lists 8 and 24 bit images only.</td></tr><tr><td>64:</td><td>Lists SDS elements only.</td></tr><tr><td>128:</td><td>Lists Vset elements only.</td></tr><tr><td>256:</td><td>Set variable HDF_Flag to 1 if an element (specified by Ref and Tag keywords) exists in the file or to 0 if it does not exist.</td></tr></tbody></table>
| FileDescription | When reference and tag numbers are not specified, the file descriptor, if it exists, is returned in the string HDF_File_Desc. |
|  | If a descriptor number is specified via the Descriptor keyword, the specified descriptor, if it exists, is returned in the same string, HDF_File_Desc. |
|  | When reference and tag numbers are specified via the Ref and Tag keywords, HDFInfo attempts to locate a corresponding descriptor and return it in the string HDF_Obj_Desc. |
|  | In any of these cases, HDFInfo creates the output string only if the specified descriptor exists. |
| <span class="table-cell-nowrap">Descriptor = *num*</span> | Designates which sequential file descriptor to return in HDF_File_Desc. Reference and Tag numbers must not be specified for this call. The first descriptor in the file is 0. |
| Image8Dim | Stores the dimensions of the image whose reference number is specified via the Ref keyword in the variables HDF_Image_Width and HDF_Image_Height. |
|  | If the image does not exist, the variables are not created. |
| Image24Dim | Stores the dimensions of the image whose reference number is specified via the Ref keyword in the variables HDF_Image_Width and HDF_Image_Height. Also places the interlace format in HDF_IMAGE_Interlace with the values 0 for RGB components of consecutive pixels, 1 for RGB components of consecutive lines and 2 for RGB components of one plane at a time. |
|  | If the image does not exist, the variables are not created. |
| Num24BImages | Stores the number of 24-bit images of the specified file in the variable HDF_Num_24BImages. |
| SDSInfo | Reads the SDS information for the SDS whose reference number is specified via the Ref keyword or, if no Ref keyword is used, attempts to read the information for the first SDS in the file. |
|  | Creates the wave HDF_SDS_Dimensions and variables: HDF_SDS_Rank which stores the number of dimensions, HDF_SDS_NumType which specifies the data type (using IGOR's definitions - see [WaveType](/igorpro/commands/wavetype.md)), and HDF_SDS_NumSets which stores the number of SDS in the whole file. |
| SDSRange | Reads the range of the SDS whose reference number is specified via the Ref keyword or, if no Ref keyword is used, that of the first SDS in the file. |
|  | The range and the fill value are stored in the variables: HDF_SDS_Max, HDF_SDS_Min and HDF_SDS_Fill respectively. |
|  | If any of this information is not available from the file, HDFInfo will not create the corresponding variable. |
| SDSCal | Reads the calibration information of the SDS whose reference number is specified via the Ref keyword or, if no Ref keyword is used, that of the first SDS in the file. |
|  | The values are stored in the variables: HDF_SDS_Cal, HDF_SDS_CalError and HDF_SDS_CalOffset and HDF_SDS_CalOffsetError. |
|  | If any of this information is not available from the file, HDFInfo will not create the corresponding variable. |
| VSets | Stores in the numeric wave HDF_VDataRefs the reference number of each Vset in the specified file. |
| VFieldNames | Stores in the string variable HDF_VFieldNames a comma-separated list of the name of each VField in the VSet whose reference number is specified via the Ref keyword. |
| VSetName | Stores in the string variable HDF_VDataName the name of the VSet whose reference number is specified via the Ref keyword. |
| VSetInfo | Stores in numeric and string variables information on the VSet whose reference number is specified via the Ref keyword. The variables are HDF_VDataName, HDF_VClassName, HDF_VInterlace, HDF_VRecCount, HDF_VRecSize (record size in bytes), HDF_VNumFields, and HDF_VRef (the specified reference number). |
| <span class="table-cell-nowrap">VField = *num*</span> | Specifies the number of the field to be read when used with the VFieldSize and VFieldType keywords. *num*  must be in the range 0 to n-1 where n is the number of fields in the VSet. |
| VFieldSize | Stores the size of the specified field in HDF_VFieldSize. Use the Ref keyword and the VField keyword to identify the VSet and field number. |
| VFieldType | Stores the type (see [WaveType](/igorpro/commands/wavetype.md)) of the specified field in HDF_VFieldType. Use the Ref keyword and the VField keyword to identify the VSet and field number. |
| VNumFields | Stores in the variable HDF_VNumFields the number of fields in the Vset specified by the Ref keyword. |
| NumVGroups | Stores in HDF_NumVGroups the number of VGroups in the file. |
| LoneGroups | Stores in the variable HDF_NumLoneVGroups the number of lone VGroups in the file and stores their reference numbers in the wave HDF_LoneVGroup_Wave. |
| VGroupsRefs | Stores in the wave HDF_VGroupRefs the reference number of each VGroup in the file. |
| NumVObjects | Stores in the variable HDF_NumVObjects the number of tags and reference pairs in the file. |
| VGroupName | Stores in the string HDF_VGroupName the name of the VGroup specified by the Ref keyword. |
| VAllTagRefs | Stores in the waves HDF_VGTags and HDF_VGRefs the tag and reference number of each object in the VGroup specified by the Ref keyword. |
| VTagRef | Stores in the variables HDF_Tag and HDF_Ref the tag and reference number of the object specified by the VObject keyword in the VGroup specified by the Ref keyword. |
| <span class="table-cell-nowrap">VObject = *num*</span> | Specifies the number of the object in the VGroup to which the VTagRef keyword refers. *num*  must be in the range 0 to n-1 where n is the number of objects in the VGroup. |
| <span class="table-cell-nowrap">Tag2Text = *tagnum*</span> | If the /Q flag is omitted, this prints a string describing the specified tag. If the /Q flag is present, it stores the string in the string variable HDF_Tag_Text. |

### *Details* {#details}
HDFInfo sets the standard Igor file-loader output variables:

S_fileName	Set to the full path to the loaded file.

|  |  |
| --- | --- |
| V_Flag | Set to error code if any. This is not be reliable. |


### *Examples* {#examples}
In these examples, HDF is a symbolic path that points to a folder containing HDF files.

List the contents of an HDF File in the history window:

```igor
HDFInfo/P=HDF "sample.hdf"
```

List in the history window all elements having reference number=3:

```igor
HDFInfo/P=HDF Mode=2,Ref=3,"sample.hdf"
```

Store in the wave HDF_List all elements having tag number=302:

```igor
HDFInfo/P=HDF Mode=5,tag=302, "sample.hdf"
HDF_List is created by the operation. If a wave by that name already exists, it is overwritten.
```

Get the SDS information that contains the rank of the data, the number of elements in each dimension and the data type.

```igor
HDFInfo/P=HDF Ref=2,SDSInfo ,"sample.hdf"
Print HDF_SDS_Rank, HDF_SDS_Dimensions[0], HDF_SDS_NumType
```

Determine how many 24-bit images are in a file.

```igor
HDFInfo/P=HDF Num24BImages,"sample.hdf" ;
Print HDF_Num_24BImages
```

Determine the number of VGroups in a file.

```igor
HDFInfo/P=HDF NumVGroups,"sample.hdf"
Print HDF_NumVGroups
```

Determine the number of independent VGroups in a file.

```igor
HDFInfo/P=HDF LoneGroups,"sample.hdf"
Print HDF_NumLoneVGroups
Edit HDF_LoneVGroup_Wave
```


Get a wave containing the references of all VGroups in a file.

```igor
HDFInfo/P=HDF VGroupsRefs,"sample.hdf"
Edit HDF_VGroupRefs
```

Get the number of objects in VGroup reference 36.

```igor
HDFInfo/P=HDF Ref=36, NumVObjects, "sample.hdf"
Print HDF_NumVObjects
```

Get the the name of VGroup reference 36.

```igor
HDFInfo/P=HDF, Ref=36 VGroupName,"sample.hdf"
Print HDF_VGroupName
```

Get a wave containing all the tags for reference 36.

```igor
HDFInfo/P=HDF Ref=36, VAllTagRefs,"sample.hdf"
Edit HDF_VGTags, HDF_VGRefs
```

<div className="command-signature">

## <strong>HDFReadImage</strong>  [/P=<em>pathName</em> ] [ <em>keyword</em> =<em>value</em>, <em>keyword</em> =<em>value</em>, ]  [<em>fileNameStr</em> ] {#hdfreadimage}

</div>

The HDFReadImage operation reads 8-bit images and palettes as well as 24-bit images from the specified HDF file.

When used to load an 8-bit image, HDFReadImage creates a 2D wave named HDF_Image.

When used to load an 24-bit image as RGB, HDFReadImage creates a three 2D waves named HDF_24Red, HDF_24Green, and HDF_24Blue. They can be massaged into a 3-layer 3D wave for display with Igor's [NewImage](/igorpro/commands/newimage.md) operation. The examples below include a function that does this.

When used to load an 24-bit image as grayscale, HDFReadImage creates a 2D wave named HDF_24Y.

Use the Ref keyword to specify which image to read.

### *Parameters* {#hdfreadimage-parameters}
If *fileNameStr* is omitted or is "", HDFInfo displays an open-file dialog.

### *Flags* {#hdfreadimage-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for *fileNameStr.* |
| <span class="table-cell-nowrap">/Q</span> | Suppress text output to the history window. |

### *Keywords* {#hdfreadimage-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">Ref = *num*</span> | Read image of reference number=*num.* |
| RGB | Read a 24-bit per pixel image. |
| MakeGray | Convert the RGB into a Gray scale image based on the luminance using Y=0.299R+0.587G+0.114B. The resulting matrix wave is saved as HDF_24Y. When using the MakeGray keyword, you must also use the RGB keyword. |
| <span class="table-cell-nowrap">ImageName = *nameStr*</span> | Specifies the name to use for the image wave. *nameStr*  is a string expression. If a wave by that name already exists, the operation will overwrite it. If the ImageName keyword is omitted, the image wave will be named HDF_Image. |
| <span class="table-cell-nowrap">PalName = *nameStr*</span> | Read the palette associated with the specified image and store it in a newly created wave whose name is specified by the string expression *nameStr*.  If a wave by that name already exists, the operation will overwrite it. The HDF palette is converted into an IGOR RGB index wave of 3x256 entries having the range [0,65535]. |
| <span class="table-cell-nowrap">Mode = m</span> | 0: Reads the image specified by the Ref keyword into a signed 16-bit word wave. This is the default behavior if the Mode keyword is omitted. |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Not used.</td></tr><tr><td>2:</td><td>Not used. (Previously this meant &quot;get palette associated with the image&quot; but it did not work correctly. Use PalName=palNameStr instead.)</td></tr></tbody></table>
| Float |<table class="nested-table"><tbody><tr><td>4:</td><td>Stores image data as single-precision floating point. The associated palette is still read as signed 16-bit.</td></tr></tbody></table>
| Double |<table class="nested-table"><tbody><tr><td>8:</td><td>Stores image data as double-precision floating point. The associated palette is still read as signed 16-bit.</td></tr></tbody></table>
| PalOnly |<table class="nested-table"><tbody><tr><td>16:</td><td>Reads the specified palette only. Does not read the image.</td></tr></tbody></table>



### *Details* {#hdfreadimage-details}
HDFReadImage sets the standard Igor file-loader output variables:

|  |  |
| --- | --- |
| S_fileName | Set to the full path to the loaded file. |
| V_Flag | Set to error code if any. This is not be reliable. |

### *Examples* {#hdfreadimage-examples}
In these examples, HDF is a symbolic path that points to a folder containing HDF files.

Read the image whose reference number is 3 into a 2D wave named star and also read the image palette, if available, into a wave named "starPal":

```igor
HDFReadImage/P=HDF ref=3,ImageName="star",PalName="starPal","star.hdf"
Display the image just read using its palette.
NewImage star; ModifyImage star, cindex=starPal```
```

Read a 24-bit raster image whose reference number is 1.

```igor
HDFReadImage/P=HDF RGB, ref=1, "sample.hdf"
```

HDFReadImage loads a 24-bit image as three images, a red plane, a green plane and a blue plane. This function shows how you an merge these into one wave. The output wave is a 3D wave with three layers, scaled so that a full-on pixel has the value 65535. Igor's NewImage operation is able to display such a 3D wave as an image.

```igor
Function ConvertRGBPlanesToRGB3D(r, g, b, name)
    Wave r, g, b
    String name	// Name for new 3D wave.

    Variable width = DimSize(r, 0)
    Variable height = DimSize(r, 1)

    Make/O/W/U/N=(width,height,3) $name
    Wave w = $name

    ImageTransform/P=0/D=r setPlane w
    KillWaves/Z r

    ImageTransform/P=1/D=g setPlane w
    KillWaves/Z g

    ImageTransform/P=2/D=b setPlane w
    KillWaves/Z b

    // Scale so max is 65535
    w *= 65535/255
End
```

Convert the three planes just read into a 3D wave and display the image:

```igor
ConvertRGBPlanesToRGB3D(HDF_24Red, HDF_24Green, HDF_24Blue, "sample")
NewImage sample
KillWaves HDF_24Red, HDF_24Green, HDF_24Blue
```

<div className="command-signature">

## <strong>HDFReadSDS</strong>  [/P=<em>pathName</em> ] [ <em>keyword</em> =<em>value</em>, <em>keyword</em> =<em>value</em>, ]  [<em>fileNameStr</em> ] {#hdfreadsds}

</div>

The HDFReadSDS operation reads scienfitic data from a specified HDF file. It creates a wave named HDF_SDS_Wave to store the data.

### *Parameters* {#hdfreadsds-parameters}
If *fileNameStr* is omitted or is "", HDFInfo displays an open-file dialog.

### *Flags* {#hdfreadsds-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for *fileNameStr.* |
| <span class="table-cell-nowrap">/Q</span> | Suppresses text output to the history window. |

### *Keywords* {#hdfreadsds-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">Ref = *num*</span> | If *num* is non-negative, reads the SDS whose reference number is *num*. |
|  | If *num*  is negative, reads the SDS whose index is -*num*. For example, ref=-1 reads the first SDS in the file, ref=-2 reads the seconds SDS in the file, and so on. This is a workaround for an apparent bug in the HDF4 library SDreftoindex routine. If you have multiple SDS's in a file and you get the same one regardless of which reference number you specify, you can load them using negative numbers for *num*. |
| <span class="table-cell-nowrap">Dim = *m*</span> | Reads the specified dimension only. |
| <span class="table-cell-nowrap">SDSStart = *wave*</span> | Specifies the name of a wave that contains the starting point for each dimension. If omitted, the operation defaults to start at the first element of each dimension. |
| <span class="table-cell-nowrap">SDSCount = *wave*</span> | Specifies the name of a wave that contains the number of points to read in each dimension. If omitted, the operation reads all points. |
| <span class="table-cell-nowrap">SDSStride = *wave*</span> | Specifies the name of a wave that contains the size of a read stride in each dimension. If omitted, the stride is 1. |
|  | When stride wave is specified, it overrides the count wave if any, and the actual count is computed based on the dimensions of the data, the start wave and the stride size. |
| DimStrings | Read the dimension strings for the dimension specified by the Dim keyword and store them in the string variables HDF_SDS_Label, HDF_SDS_Units, HDF_SDS_Format. The operation creates the string variables if they do not already exist. |

### *Details* {#hdfreadsds-details}
The SDS is converted into an Igor wave whose dimensionality appears in the reverse order to that of the HDF format. The apparent dimensionality reversal is to assure that the fastest incrementing index in the data and in the Igor wave match.

HDFReadSDS sets the standard Igor file-loader output variables:

|  |  |
| --- | --- |
| S_fileName | Set to the full path to the loaded file. |
| V_Flag | Set to error code if any. This is not be reliable. |

### *Examples* {#hdfreadsds-examples}
In these examples, HDF is a symbolic path that points to a folder containing HDF files.

```igor
// Read the SDS whose reference number is 2, rename the wave and display it in a table.
HDFReadSDS/P=HDF Ref=2, "sample.hdf"
Rename HDF_SDS_Wave, sample1
Edit sample1

// Read the SDS whose reference number is 2 starting in each dimension at a point
// specified in startWave and reading the number of points specified in countWave.
// The data is stored in HDF_SDS_Wave.
HDFReadSDS/P=HDF Ref=2, SDSStart=startWave, SDSCount=countWave, "sample.hdf"

// Read the SDS whose reference number is 2 using a stride specified by the wave stride.
HDFReadSDS/P=HDF Ref=2, sdsstride=stride, "sample.hdf"

// Read the first two SDS's in the file
HDFReadSDS/P=HDF Ref=-1, "sample.hdf"   // -1 means first SDS in file
HDFReadSDS/P=HDF Ref=-2, "sample.hdf"   // -2 means second SDS in file
```

### *See Also* {#see-also}
SDS keywords for the [HDFInfo](/igorpro/extensions/file-loaders/hdf-loader/hdf-loader-operations.md#hdfinfo) operation.

<div className="command-signature">

## <strong>HDFReadVset</strong>  [/P=<em>pathName</em> ] [ <em>keyword</em> =<em>value</em>, <em>keyword</em> =<em>value</em>, ]  [<em>fileNameStr</em> ] {#hdfreadvset}

</div>

The HDFReadVset operation reads VData from a specified HDF file. The operation supports reading several fields of different data types.

Use the Ref, Record and VField keywords to specify which datum you want to access. HDFReadVSet returns the value of that datum in the variable HDF_V_Value.

### *Parameters* {#hdfreadvset-parameters}
If *fileNameStr* is omitted or is "" , HDFInfo displays an open-file dialog.

### *Flags* {#hdfreadvset-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for *fileNameStr.* |

### *Keywords* {#hdfreadvset-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">Ref = *num*</span> | Reads Vset whose reference number is *num .* |
| <span class="table-cell-nowrap">Record = *num*</span> | Specifies the VData record to read. The first record in the file is 0. |
| <span class="table-cell-nowrap">VField = *num*</span> | Specifies the number of the field to be read. The first field in the file is 0. |
| <span class="table-cell-nowrap">VInterlace = *val*</span> | Sets the interlace mode for accessing the Vset. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Full interlace</td></tr><tr><td>1:</td><td>No interlace</td></tr></tbody></table>
|  | By default, the interlace value is 1 so that a field corresponds directly to an IGOR wave. |

### *Details* {#hdfreadvset-details}
HDFReadVSet sets the standard Igor file-loader output variables:

|  |  |
| --- | --- |
| S_fileName | Set to the full path to the loaded file. |
| V_flag | Set to the number of waves loaded or to error code. |
| S_waveNames | Set to a semicolon separated list of wave names. Since this operation creates no waves, this string is set to empty. |

### *Examples* {#hdfreadvset-examples}
In these examples, HDF is a symbolic path that points to a folder containing HDF files.

Read field number 2 of record 0 from the Vset whose reference number is 3.

```igor
HDFReadVset/P=HDF Ref=3, record=0, vField=2, "sample.hdf"
```

### *See Also* {#hdfreadvset-see-also}
SDS keywords for the [HDFInfo](/igorpro/extensions/file-loaders/hdf-loader/hdf-loader-operations.md#hdfinfo) operation.