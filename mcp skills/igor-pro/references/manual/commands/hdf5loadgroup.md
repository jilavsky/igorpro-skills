---
description: "The HDF5LoadGroup operation loads an HDF5 group and its datasets into an Igor Pro data folder. It optionally recursively loads subgroups and their datasets."
slug: /commands/hdf5loadgroup
---

<div className="command-signature">

## <strong>HDF5LoadGroup</strong>  [ /CONT=<em>continue</em> /ENUM=<em>enumMode</em> /IGOR=<em>attributesMask</em> /IMAG=<em>lookForFormalImages</em> /L=<em>loadFlags</em> /N=<em>name</em> /O /ORDR=<em>order</em> /OPTS=<em>options</em> /R[=<em>mode</em> ] /T[=<em>topLevelName</em> ] /TRAN=<em>transpose</em> /VAR=<em>varMode</em> /Z ] <em>dataFolderSpec</em>, <em>locationID</em>, <em>nameStr</em> {#hdf5loadgroup}

</div>

The HDF5LoadGroup operation loads an HDF5 group and its datasets into an Igor Pro data folder. It optionally recursively loads subgroups and their datasets.

When recursively loading subgroups, HDF5LoadGroup ignores links.

HDF5LoadGroup is less flexible than [HDF5LoadData](/igorpro/commands/hdf5loaddata.md). HDF5LoadGroup does not load attributes. It is also lacking many of the flags supported by HDF5LoadData.

The name of each data folder created is a possibly cleaned up version of the name of the corresponding group in the HDF5 file.

Igor numeric and string variables saved in an HDF5 file via HDF5SaveData and HDF5SaveGroup are marked with an "IGORVariable" attribute. When HDFLoadGroup loads such a dataset, it creates an Igor variable instead of creating a wave. See [Saving and Reloading Igor Data](/igorpro/data/igor-hdf5-guide.md#saving-and-reloading-igor-data) for details. All other datasets are loaded into waves.

When loading most types of datasets, HDF5LoadGroup creates just one wave. When loading a variable-length dataset one wave is created for each loaded element. When loading a compound dataset, one wave is created for each member loaded.

By default, the name of each loaded object is a possibly cleaned up version of the name of the corresponding dataset. When loading a variable-length dataset which requires more than one wave to be loaded, the wave names consist of a base name and a number. When loading a compound dataset the wave names consist of a base name concatenated with a possibly cleaned up version of the member name.

### *Parameters* {#parameters}
*dataFolderSpec* is the name of or path to the data folder into which the HDF5 data is to be loaded. Use : for the current data folder and root: for the root data folder.

*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*nameStr* is a string containing the name of the group to be loaded. This can be a full HDF5 path or partial HDF5 path or simple name relative to *locationID*. To load the root group, pass the file ID as the *locationID* parameter and pass "." as the *nameStr* parameter.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CONT = *continue*</span> | Controls what happens if an error occurs while loading a particular dataset in the group. This happens if, for example, the group contains a dataset that HDF5LoadGroup cannot load because it does not support the datatype of that dataset (see [Igor HDF5 Limitations](/igorpro/data/igor-hdf5-guide.md#igor-hdf5-limitations)). |
|  |<table class="nested-table"><tbody><tr><td>*continue*&nbsp;=&nbsp;0:</td><td>The HDF5LoadGroup operation stops and returns an error. The error is treated as fatal.</td></tr><tr><td>*continue*&nbsp;=&nbsp;1:</td><td>The HDF5LoadGroup operation prints an error message in the history area and then continues trying to load other datasets as if no error occurred. This is the default behavior if /CONT is omitted.</td></tr><tr><td>*continue*&nbsp;=&nbsp;2:</td><td>The HDF5LoadGroup operation continues trying to load other datasets as if no error occurred without printing an error message in the history.</td></tr></tbody></table>
| /ENUM=*enumMode* |<table class="nested-table"><tbody><tr><td>*enumMode*&nbsp;=&nbsp;0:</td><td>The integer enum data is loaded into a signed long wave.</td></tr><tr><td>*enumMode*&nbsp;=&nbsp;1:</td><td>The names associated with the integer enum data are loaded into a text wave.</td></tr></tbody></table>
|  | See [Loading HDF5 Enum Data](/igorpro/data/igor-hdf5-guide.md#loading-hdf5-enum-data) for details. |
| <span class="table-cell-nowrap">/IGOR = *attributesMask*</span> | When loading a dataset, this flag determines whether or not HDF5LoadGroup looks for attributes written by HDF5SaveData or HDF5SaveGroup which store wave properties such as units and scaling. |
|  | If *attributesMask* is 0, HDF5LoadGroup does not look for IGOR-related attributes. If the /IGOR flag is omitted it behaves like /IGOR=0. |
|  | If *attributesMask* is -1, HDF5LoadGroup looks for all IGOR-related attributes. This is recommended if you intend to load the data back into Igor which was previously written out by HDFSaveData or HDF5SaveGroup. |
|  | Otherwise *attributesMask* is a bitwise mask. The meaning of each bit is explained in the documentation for [HDF5SaveData](/igorpro/commands/hdf5savedata.md). |
|  | Looking for IGOR-related attributes in a file not written by HDF5SaveData does not harm but slightly slows HDF5LoadGroup down. |
| <span class="table-cell-nowrap">/IMAG = *lookForFormalImages*</span> |  |
|  | *lookForFormalImages* = 0: HDF5LoadGroup does not check to see if a dataset is a formal image as specified by the HDF5 Image and Palette Specification and therefore loads 2D datasets as regular images. This is the default if /IMAG is omitted. |
|  | *lookForFormalImages* = 1: HDF5LoadGroup does check to see if a dataset is a formal image as specified by the HDF5 Image and Palette Specification and loads such datasets as formal images. See [HDF5 Images Versus Igor Images](/igorpro/data/igor-hdf5-guide.md#hdf5-images-versus-igor-images) for details. |
|  | When /IMAG=1 is used with a formal image that includes a palette dataset stored in the same group as the image dataset, the palette dataset is loaded twice. It is loaded once when HDF5LoadGroup loads the image dataset. At this point the wave created for the palette is named the same as the image dataset with a suffix of "Pal". The palette is loaded a second time when HDF5LoadGroup encounters the palette dataset. This time it is named according to the name of the palette dataset. If this duplication causes a problem then the only recourse is to load the formal images one at a time using HDF5LoadImage. |
| <span class="table-cell-nowrap">/L = *loadFlags*</span> | *loadFlags* controls what kind of data objects are loaded with a bit for each object type. See the ***Load Flags*** table below for acceptable values. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details on bit settings. |
|  | To load multiple object types, sum the values shown in the *loadFlags* column. For example, `loadFlags=1` loads just waves while `loadFlags=7` loads all three object types. |
|  | HDF5LoadGroup normally loads datasets into waves. See [Saving and Reloading Igor Data](/igorpro/data/igor-hdf5-guide.md#saving-and-reloading-igor-data) for details on when it loads datasets into variables. |
|  | If /L is omitted, this acts like /L=7 meaning that all object types are loaded. |
| <span class="table-cell-nowrap">/N = *name*</span> | *name* is the name to be used for the loaded waves. If /N is omitted, each name is a possibly cleaned up version of the name of the corresponding dataset. Note that *name* is not a string. |
|  | When loading most types of datasets, just one wave is created. When loading a variable-length dataset, one wave is created for each loaded element. In this case, *name* is treated as a base name. For details see [HDF5 Variable-Length Data](/igorpro/data/igor-hdf5-guide.md#hdf5-variable-length-data). |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing data folders and waves in case of name conflicts. If /O is omitted, HDF5LoadGroup chooses names that don't conflict with existing objects. |
|  | When /O is used and a data folder is "overwritten", HDF5LoadGroup does a "mix-in overwrite". This means that any waves with conflicting names are overwritten and any pre-existing waves in the data folder that do not conflict with incoming waves are left in place. |
|  | To do a "normal overwrite", in which the entire data folder and all of its contents are replaced, you must delete the data folder using [KillDataFolder](/igorpro/commands/killdatafolder.md) before calling HDF5LoadGroup. |
| <span class="table-cell-nowrap">/OPTS = *options*</span> | Controls aspects of loading data. |
|  | /OPTS requires Igor Pro 9.00 or later. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>If set, HDF5LoadGroup loads 64-bit integer data as 64-bit integer. If cleared, it loads 64-bit integer data as double-precision floating point.</td></tr></tbody></table>
|  | For backward compatibility, bit 0 defaults to 0. If you omit /OPTS, 64-bit integer data is loaded as double-precision floating point. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;1:</td><td>If set, HDF5LoadGroup checks each loaded text wave and sets the wave&#39;s text data text encoding to binary if any element contains control characters other than carriage-return, linefeed, and tab. If cleared, no check for binary is done.</td></tr></tbody></table>
|  | Bit 1 defaults to 0. If you load string datasets that contain binary data, we recommend that you use /OPTS with bit 1 set. See [Text Waves Containing Binary Data](/igorpro/igor-basics/text-encodings.md#text-waves-containing-binary-data) for background information. |
|  | All other bits are reserved and must be set to zero. |
| <span class="table-cell-nowrap">/ORDR = *order*</span> | Controls the order of loading of objects. |
|  |<table class="nested-table"><tbody><tr><td>*order*&nbsp;=0:</td><td>Load objects in alphabetic order. This is the default if you omit /ORDR.</td></tr><tr><td>*order*&nbsp;=1:</td><td>Load objects in creation order if possible or using alphabetic order otherwise.</td></tr></tbody></table>
|  | In order to load objects in creation order, the objects' group must include creation-order information. Most HDF5 files do not include creation-order information. However, HDF5 files written by Igor Pro 9 or later include creation-order information and so are loaded in creation order if you use /ORDR=1. |
| <span class="table-cell-nowrap">/R[ = *mode* ]</span> | Controls recursion of the HDF5LoadGroup operation. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not recursive. This is the default if you omit /R.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Recursive. Does not load the same group more than once. Same as /R by itself.</td></tr><tr><td>*mode*&nbsp;=2:</td><td>Recursive. Does load the same group more than once.</td></tr></tbody></table>
|  | See ***HDF5LoadGroup Recursion Modes*** below for further information. |
| <span class="table-cell-nowrap">/T[ = *topLevelName* ]</span> | If /T=*topLevelName* is specified, HDF5LoadGroup creates a new data folder in the current data folder with the specified name and places the loaded data in the new data folder. |
|  | If just /T is specified, HDF5LoadGroup creates a new data folder in the current data folder using a possibly cleaned up version of the name of the group being loaded. If the group being loaded is the root group ("/"), a possibly cleaned up version of the file name (without the extension) is used. |
|  | If /T is omitted, the data is loaded into the current data folder and no top-level data folder is created. |
| /TRAN=*transpose* |<table class="nested-table"><tbody><tr><td>*transpose*&nbsp;=&nbsp;0:</td><td>Normal load, no transpose (default).</td></tr><tr><td>*transpose*&nbsp;=&nbsp;1:</td><td>Transposes multi-dimensional numeric data after loading. This works only when loading data into multi-dimensional, numeric (real or complex) waves and is ignored for 1D and text waves. See [HDF5 Images Versus Igor Images](/igorpro/data/igor-hdf5-guide.md#hdf5-images-versus-igor-images) for details.</td></tr></tbody></table>
| /VAR=*varMode* |<table class="nested-table"><tbody><tr><td>*varMode*&nbsp;=&nbsp;0:</td><td>Load the dataset into a wave even if it is marked with the IGORVariable attribute. This is provided for the convenience of the HDF5 Browser and is probably of no use otherwise.</td></tr><tr><td>*varMode*&nbsp;=&nbsp;1:</td><td>Look for the IGORVariable attribute and, if it is present, load the dataset into an Igor numeric or string variable. This is the default setting.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Load Flags* {#load-flags}
The following table details acceptable values for the /L flag:

| loadFlags | Bit number | Loads this type of object |
| --- | --- | --- |
| 1 | 0 | Waves |
| 2 | 1 | Numeric variables |
| 4 | 2 | String variables |

### *Output Variables* {#output-variables}
HDF5LoadGroup sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |
|  | As explained above, the /CONT flag determines whether an error in loading a particular dataset is considered a fatal error. V_flag reflects fatal errors only. |
| S_groupPaths | Set to a semicolon-separated list of the full paths to the HDF5 file groups encountered during the load. |
| S_dataFolderPaths | Set to a semicolon-separated list of the full paths to the data folders encountered during the load whether or not any waves were created in those data folders. Each path ends with a colon. Liberal names in the paths are quoted. |
| S_objectPaths | Set to a semicolon-separated list of the full paths to the loaded objects. Liberal names in the paths are quoted. |
|  | When loading recursively, you cannot count on the order of the object paths. The object paths are added to the list in the order in which the objects are created but the innermost group's datasets may be loaded before those of outer groups. |

### *HDF5LoadGroup Recursion Modes* {#hdf5loadgroup-recursion-modes}
If you use /R, /R=1 (same as /R) or /R=2, HDF5LoadGroup loads the group specified by *locationID* and *nameStr* and any subgroups.

Because an HDF5 file is a "directed graph", not a strict hierarchy, it is possible for a given group to appear multiple times at different locations in the file. /R=1 loads a given group only once and skips it if it appears elsewhere in the file. /R=2 loads a given group each time it appears in the file, creating duplicate Igor data folders.

### *HDF5LoadGroup and Non-Hierarchical File Arrangements* {#hdf5loadgroup-and-non-hierarchical-file-arrangements}
This section deals with HDF5 file organizations that are not hierarchical. This advanced material is of interest only in relatively rare cases and can be skipped for most purposes.

In an HDF5 file, a given group can appear more than once because HDF5 files are "directed graphs", not strict hierarchies. This is explained in the HDF5 User Guide chapter on groups.

When an HDF5 group is created, a hard link to it is automatically created in its parent group. This type of object creation results in a hierarchy - a tree structure in which there is just one path to any given group.

To create a non-hierarchical file, in which there is more than one path to one or more groups, you need to add a hard or soft link to a group. Most files do not have such links.

In this example, LinkToGroupA is a hard link that points to /GroupA:


```igor
/ (root)
	GroupA
		dataset0
		GroupB
	LinkToGroupA
		dataset0
		GroupB
```

GroupA now appears twice: once at location "/GroupA" and again at location "/LinkToGroupA".

HDF5LoadGroup/R=1 does not load LinkToGroupA because it points to an already-loaded group. You wind up with data folder root:GroupA only.

HDF5LoadGroup/R=2 does load LinkToGroupA. You wind up with data folders root:GroupA and root:LinkToGroupA. root:LinkToGroupA is a duplicate of root:GroupA:.

### *HDF5LoadGroup and Circular References* {#hdf5loadgroup-and-circular-references}
It is possible to add a hard or soft link to a group such that the link points to the group itself or to its ancestor. This creates a circular reference. Most HDF5 files do not have circular references.

HDF5LoadGroup detects circular references and does not load a group that creates one. This is true of both HDF5LoadGroup/R=1 and HDF5LoadGroup/R=2

### *See Also* {#see-also}
[HDF5CreateFile](/igorpro/commands/hdf5createfile.md), [HDF5OpenFile](/igorpro/commands/hdf5openfile.md), [HDF5CloseFile](/igorpro/commands/hdf5closefile.md), [HDF5FlushFile](/igorpro/commands/hdf5flushfile.md), [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md), [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md), [HDF5CloseGroup](/igorpro/commands/hdf5closegroup.md)

See [HDF5 Compound Data](/igorpro/data/igor-hdf5-guide.md#hdf5-compound-data) for information on loading compound data (structures).

See [HDF5 Images Versus Igor Images](/igorpro/data/igor-hdf5-guide.md#hdf5-images-versus-igor-images) for special considerations when loading images.

See [HDF5 Bitfield Data](/igorpro/data/igor-hdf5-guide.md#hdf5-bitfield-data) for details on bitfield data.

See [Loading HDF5 Enum Data](/igorpro/data/igor-hdf5-guide.md#loading-hdf5-enum-data) for details on enum data.

See [HDF5 Opaque Data](/igorpro/data/igor-hdf5-guide.md#hdf5-opaque-data) for details on opaque data.

See [HDF5 Variable-Length Data](/igorpro/data/igor-hdf5-guide.md#hdf5-variable-length-data) for details on variable-length data.

See [HDF5 Dataset Subsets](/igorpro/data/igor-hdf5-guide.md#hdf5-dataset-subsets) for details on using hyperslabs.

See [HDF5 Array Data](/igorpro/data/igor-hdf5-guide.md#hdf5-array-data) for a discussion of loading datasets whose elements consist of arrays.

See [HDF5 Attributes](/igorpro/data/igor-hdf5-guide.md#hdf5-attributes) for a discussion of loading attributes of groups and datasets.