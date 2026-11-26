---
description: "The HDF5SaveGroup operation saves the contents of an Igor data folder in an HDF5 file."
slug: /commands/hdf5savegroup
---

<div className="command-signature">

## <strong>HDF5SaveGroup</strong>  [ <em>flags</em> ] <em>dataFolderSpec</em>, <em>locationID</em>, <em>nameStr</em> {#hdf5savegroup}

</div>

The HDF5SaveGroup operation saves the contents of an Igor data folder in an HDF5 file.

By default, HDF5SaveGroup saves all Igor waves, numeric variables and string variables in the specified data folder. The /L flag allows you to skip saving any of those object types.

HDF5SaveGroup writes Igor numeric and string variables as datasets with an "IGORVariable" attribute. See [Saving and Reloading Igor Data](/igorpro/data/igor-hdf5-guide.md#saving-and-reloading-igor-data) for details.

### *Parameters* {#parameters}
*dataFolderSpec* is the name of or path to the data folder to be saved. Use : for the current data folder and root: for the root data folder. See [Data Folder Syntax](/igorpro/igor-basics/data-folders.md#data-folder-syntax) for details, especially about quoting of liberal names.

*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*nameStr* is a string containing the name of an existing group into which data is to be saved. This can be a full HDF5 path or partial HDF5 path or simple name relative to *locationID*.

### *Flags* {#flags}

|  |
| --- |
| <span class="table-cell-nowrap">/COMP = {*minWaveElements, gzipLevel, shuffle*}</span> |

Specifies that compression is to be applied to numeric waves saved. The /COMP flag was added in Igor Pro 9.00.

*minWaveElements* is the minimum number of elements that a numeric wave must have to be eligible for compression. Waves with fewer than this many total elements are not compressed.

*gzipLevel* is a value from 0 to 9. 0 means no GZIP compression.

*shuffle* is 0 to turn shuffle off or 1 to turn shuffle on.

When compression is applied by HDF5SaveGroup, the entire wave is saved in one chunk. See [HDF5 Layout Chunk Size](/igorpro/data/igor-hdf5-guide.md#hdf5-layout-chunk-size) for background information and [HDF5SaveGroup Compression](/igorpro/data/igor-hdf5-guide.md#hdf5savegroup-compression) for details.

The compression specified by /COMP can be overridden by HDF5SaveDataHook.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CONT = *continue*</span> | Controls what happens if an error occurs while saving a particular dataset in the group. |
|  |<table class="nested-table"><tbody><tr><td>*continue*&nbsp;=&nbsp;0:</td><td>The HDF5SaveGroup operation stops and returns an error. The error is treated as fatal.</td></tr><tr><td>*continue*&nbsp;=&nbsp;1:</td><td>The HDF5SaveGroup operation prints an error message in the history area and then continues trying to save other datasets as if no error occurred. This is the default behavior if /CONT is omitted.</td></tr><tr><td>*continue*&nbsp;=&nbsp;2:</td><td>The HDF5SaveGroup operation continues trying to save other datasets as if no error occurred without printing an error message in the history.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/IGOR = *attributesMask*</span> | When saving a wave, this flag determines whether or not HDF5SaveGroup writes attributes to store wave properties such as units and scaling. See [HDF5SaveData](/igorpro/commands/hdf5savedata.md) for a description of *attributesMask*. |
| /TRAN=*transpose* |<table class="nested-table"><tbody><tr><td>*transpose*&nbsp;=&nbsp;0:</td><td>Normal save, no transpose (default).</td></tr><tr><td>*transpose*&nbsp;=&nbsp;1:</td><td>Multi-dimensional numeric waves are saved transposed. This works only when saving multi-dimensional, numeric (real or complex) waves and is ignored for 1D and text waves. See [HDF5 Images Versus Igor Images](/igorpro/data/igor-hdf5-guide.md#hdf5-images-versus-igor-images) for details.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/L = *saveFlags*</span> | *saveFlags* controls what kind of data objects are saved with a bit for each object type. See the ***saveFlags Bit Values*** table below for descriptions of each bit value. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details on bit settings. |
|  | To save multiple object types, sum the values shown in the *saveFlags* column. For example, *saveFlags*=1 saves just waves, *saveFlags*=7 saves all three object types. |
|  | HDF5SaveGroup writes Igor numeric and string variables as datasets with an "IGORVariable" attribute. See [Saving and Reloading Igor Data](/igorpro/data/igor-hdf5-guide.md#saving-and-reloading-igor-data) for details. |
|  | If /L is omitted, this acts like /L=7 meaning that all object types are saved. |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing group in case of a name conflict. If /O is omitted and the group already exists, HDF5SaveGroup returns an error. |
|  | When /O is used and a group is "overwritten", HDF5SaveGroup does a "mix-in overwrite". This means that any datasets with conflicting names are overwritten and any pre-existing datasets in the group that do not conflict with incoming datasets are left in place. |
|  | This deletes conflicting objects from the file's hierarchy but does not free up the space in the file used by the objects. The HDF Group provides a command-line utility program, h5repack, to compact HDF5 files. |
|  | To do a "normal overwrite", in which the entire group and all of its contents are replaced, you must unlink the group using [HDF5UnlinkObject](/igorpro/commands/hdf5unlinkobject.md) before calling HDF5SaveGroup. |
| <span class="table-cell-nowrap">/OPTS = *options*</span> | Controls aspects of saving data. |
|  | /OPTS requires Igor Pro 9.00 or later. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>If set, HDF5SaveGroup saves 64-bit integer data as 64-bit integer. If cleared, it saves 64-bit integer data as double-precision floating point.</td></tr></tbody></table>
|  | For backward compatibility, bit 0 defaults to 0. If you omit /OPTS, 64-bit integer data is saved as double-precision floating point. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;1:</td><td>If set, HDF5SaveData saves single-element datasets using a scalar dataspace. If cleared or if you omit /OPTS a simple dataspace is used. This bit applies to datasets only;  for attributes use the options parameter of the /A flag. Bit 1 requires Igor Pro 9.01 or later.</td></tr></tbody></table>
|  | All other bits are reserved and must be set to zero. |
| <span class="table-cell-nowrap">/R</span> | Recursively save subgroups. |
| <span class="table-cell-nowrap">/STRF = {*fixedLength*,*paddingMode*,*charset*}</span> |  |
|  | Controls the format in which string datasets and attributes are written. /STRF requires Igor Pro 9.00 or later. |
| The HDF5 library does not allow the creation of a zero-length fixed-length datatype. Consequently, starting with Igor Pro 9.02, Igor writes zero-length strings using a variable-length datatype regardless of the type specified by <span class="table-cell-nowrap">/STRF.</span> |  |
|  | See the HDF5SaveData documentation for /STRF and [HDF5 String Formats](/igorpro/data/igor-hdf5-guide.md#hdf5-string-formats) for details. |
| <span class="table-cell-nowrap">/T[ = *topLevelName* ]</span> | If /T=*topLevelName* is specified, HDF5SaveGroup creates a new group in the HDF5 file with the specified name and saves the contents of the data folder in the new group. |
|  | If just /T is specified, HDF5SaveGroup creates a new group using the name of the data folder being saved. |
|  | If /T is omitted or *topLevelName* is empty (""), the data is saved into the group specified by *locationID* and *nameStr* and no top-level group is created. |
| <span class="table-cell-nowrap">/VAR = *varMode*</span> | *varMode* = 0: When saving an Igor numeric or string variable, do not attach the IGORVariable attribute the dataset. |
|  | *varMode* = 1: When saving an Igor numeric or string variable, attach the IGORVariable attribute the dataset. This is the default setting. |
|  | See [Saving and Reloading Igor Data](/igorpro/data/igor-hdf5-guide.md#saving-and-reloading-igor-data) for a discussion of how the IGORVariable attribute is used. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *saveFlags Bit Values* {#saveflags-bit-values}

The following table details the accepted bit values when using the /L flag:

| saveFlags | Bit number | Saves this type of object |
| --- | --- | --- |
| 1 | 0 | Waves |
| 2 | 1 | Numeric variables |
| 4 | 2 | String variables |

### *Details* {#details}
HDF5SaveGroup writes multi-element datasets and attributes using a simple dataspace.

HDF5SaveGroup writes single-element datasets using a simple dataspace unless, in Igor Pro 9.01 or later, you set bit 1 of the options parameter of the /OPTS flag in which case it uses a scalar dataspace.

HDF5SaveGroup writes single-element attributes using a scalar dataspace unless you specify otherwise using the *options* parameter of the /A flag.

Igor Pro supports complex waves but HDF5 does not support complex datasets. Therefore, when saving a complex wave, HDF5SaveGroup writes the wave as if its number of rows were doubled. For details, see [Handling of Complex Waves](/igorpro/data/igor-hdf5-guide.md#handling-of-complex-waves).

The behavior of the [HDF5SaveGroup](/igorpro/commands/hdf5savegroup.md) operation when it is asked to save a wave reference or data folder reference wave depends on the /CONT flag. By default (/CONT=1), it prints a note in the history saying it cannot save the wave and then continues saving the rest of the objects in the data folder. If /CONT=0 is used, HDF5SaveGroup returns an error if asked to save a reference wave.

### *Output Variables* {#output-variables}
HDF5SaveGroup sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |
|  | As explained above, the /CONT flag determines whether an error in saving a particular dataset is considered a fatal error. V_flag reflects fatal errors only. |
| S_groupPaths | Set to a semicolon-separated list of the full paths to the HDF5 file groups encountered during the save. |
| S_dataFolderPaths | Set to a semicolon-separated list of the full paths to the data folders encountered during the save whether or not any objects were saved from those data folders. Each path ends with a colon. Liberal names in the paths are quoted. |
| S_objectPaths | Set to a semicolon-separated list of the full paths to the saved objects. Liberal names in the paths are quoted. |
|  | When saving recursively, you cannot count on the order of the object paths. The paths are added to the list in the order in which the objects are created but the innermost group's datasets may be loaded before those of outer groups. |

### *Example* {#example}

```igor
Function TestSaveGroup(dfPath)
	String dfPath		// e.g., "root:FolderA" or ":"

	Variable result = 0	// 0 means no error
	
	Variable fileID
	HDF5CreateFile/P=home /O /Z fileID as "Test.h5"
	if (V_flag != 0)
		Print "HDF5CreateFile failed"
		return -1
	endif

	HDF5SaveGroup /IGOR=-1 /O /R /Z $dfPath, fileID, "."
	if (V_flag != 0)
		Print "HDF5SaveGroup failed"
		result = -1
	endif
	
	HDF5CloseFile fileID

	return result
End
```

### *See Also* {#see-also}
[HDF5 Compression](/igorpro/data/igor-hdf5-guide.md#hdf5-compression), [HDF5SaveGroup Compression](/igorpro/data/igor-hdf5-guide.md#hdf5savegroup-compression)

[HDF5LoadData](/igorpro/commands/hdf5loaddata.md), [HDF5LoadGroup](/igorpro/commands/hdf5loadgroup.md), [HDF5SaveData](/igorpro/commands/hdf5savedata.md)

[HDF5CreateFile](/igorpro/commands/hdf5createfile.md), [HDF5OpenFile](/igorpro/commands/hdf5openfile.md), [HDF5CloseFile](/igorpro/commands/hdf5closefile.md), [HDF5FlushFile](/igorpro/commands/hdf5flushfile.md)

[HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md), [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md), [HDF5CloseGroup](/igorpro/commands/hdf5closegroup.md)

[Data Folders](/igorpro/igor-basics/data-folders.md)