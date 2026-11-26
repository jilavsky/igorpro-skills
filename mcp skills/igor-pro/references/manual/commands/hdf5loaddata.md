---
description: "The HDF5LoadData operation loads a dataset or attribute from an HDF5 file."
slug: /commands/hdf5loaddata
---

<div className="command-signature">

## <strong>HDF5LoadData</strong>  [ /A=<em>attributeNameStr</em> /COMP={<em>mode</em>, <em>memberName</em>} /ENUM=<em>enumMode</em> /GRPH=<em>showInGraph</em> /IGOR=<em>attributesMask</em> /N=<em>name</em> /O /OPTS=<em>options</em> /Q /SLAB=<em>slabWave</em> /T=<em>showInTable</em> /TRAN=<em>transpose</em> /TYPE=<em>objectType</em> /VAR=<em>varMode</em> /Z ] <em>locationID</em>, <em>nameStr</em> {#hdf5loaddata}

</div>

The HDF5LoadData operation loads a dataset or attribute from an HDF5 file.

When loading most types of data, HDF5LoadData creates just one wave. When loading a variable-length dataset or attribute, one wave is created for each loaded element. When loading a compound dataset or attribute, one wave is created for each member loaded.

By default, the name of the loaded wave is a possibly cleaned up version of the name of the dataset or attribute being loaded. When loading variable-length data, the wave names consist of a base name and a number. When loading a compound dataset or attribute the wave names consist of a base name concatenated with a possibly cleaned up version of the member name.

Igor numeric and string variables saved in an HDF5 file via HDF5SaveData and HDF5SaveGroup are marked with an "IGORVariable" attribute. When HDFLoadData loads such a dataset, it creates an Igor variable instead of creating a wave. See [Saving and Reloading Igor Data](/igorpro/data/igor-hdf5-guide.md#saving-and-reloading-igor-data) for details. All other datasets are loaded into waves.

### *Parameters* {#parameters}
*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*nameStr* is a string containing the name of the dataset to be loaded or, if /A=*attributeNameStr* is supplied, the name of the group, dataset or named datatype which owns the attribute. When loading an attribute attached to a group or named datatype, you must use the /TYPE flag to specify the type of object that *nameStr* refers to.

*nameStr* can contain a full HDF5 path or a partial HDF5 path or simple name relative to *locationID*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *attributeNameStr*</span> | If present, the named attribute is loaded. If absent or if *attributeNameStr* is "", a dataset is loaded. |
|  | If /A is present, *nameStr* is the name of a group or dataset or named datatype to which the attribute is attached. When loading an attribute attached to a group or named datatype, you must use the /TYPE flag to tell HDFLoadData what type of object *nameStr* refers to. |
| <span class="table-cell-nowrap">/COMP = {*mode*, *memberName*}</span> |  |
|  | /COMP controls how compound data is loaded into Igor. |
|  | If *mode* is 0, HDF5LoadData attempts to load all members of the compound data. In this case, *memberName* must be "". The /CONT flag controls what happens if an error occurs during the load of any particular member. |
|  | When *mode* is 0, HDF5LoadData creates wave names of the form \<dataName\>_\<fieldName\> where \<dataName\> is the name of the dataset or attribute or the name you specified via /N and \<fieldName\> is the name of a field in the compound data. If necessary, HDF5LoadData truncates either \<dataName\> or \<fieldName\> or both. It then alters the resulting names if necessary to ensure that the same name is not used twice. |
|  | If *mode* is 1, a single member of each element of the compound data is loaded into an Igor Pro wave. *memberName* must be the name of the member to be loaded. *memberName* is case sensitive. |
|  | If the /COMP flag is omitted this is the same as /COMP={0, ""}. |
|  | See [HDF5 Compound Data](/igorpro/data/igor-hdf5-guide.md#hdf5-compound-data) for details. |
| <span class="table-cell-nowrap">/CONT = *continue*</span> | Controls what happens if an error occurs while loading all of the members of a compound dataset or attribute. This happens if, for example, a compound dataset contains a member whose type is not supported by HDF5LoadData (see [Igor HDF5 Limitations](/igorpro/data/igor-hdf5-guide.md#igor-hdf5-limitations)). |
|  |<table class="nested-table"><tbody><tr><td>*continue*&nbsp;=&nbsp;0:</td><td>The HDF5LoadData operation stops and returns an error. The error is treated as fatal.</td></tr><tr><td>*continue*&nbsp;=&nbsp;1:</td><td>The HDF5LoadData operation prints an error message in the history area and then continues trying to load other members as if no error occurred. This is the default behavior if /CONT is omitted.</td></tr><tr><td>*continue*&nbsp;=&nbsp;2:</td><td>The HDF5LoadData operation continues trying to load other members as if no error occurred without printing an error message in the history.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/ENUM = *enumMode*</span> | enumMode = 0: The integer enum data is loaded into a signed long wave. |
|  | enumMode = 1: The names associated with the integer enum data are loaded into a text wave. |
|  | See [Loading HDF5 Enum Data](/igorpro/data/igor-hdf5-guide.md#loading-hdf5-enum-data) for details. |
| <span class="table-cell-nowrap">/GRPH = *showInGraph*</span> | *showInGraph =* 0: Do not show loaded wave in a new graph. This is the default behavior. |
|  |<table class="nested-table"><tbody><tr><td>*showInGraph&nbsp;=*&nbsp;1:</td><td>Show loaded wave in a new graph.</td></tr><tr><td>*showInGraph&nbsp;=*&nbsp;2:</td><td>Append loaded wave to top graph. If there are no graphs, a new graph is created as if *showInGraph* were 1.</td></tr><tr><td>*showInGraph&nbsp;=*&nbsp;3:</td><td>Same as *showInGraph* = 1 except if the loaded wave existed prior to the call to HDF5LoadData in which case it acts like *showInGraph* = 0.</td></tr><tr><td>*showInGraph&nbsp;=*&nbsp;4:</td><td>Same as *showInGraph* = 2 except if the loaded wave existed prior to the call to HDF5LoadData in which case it acts like *showInGraph* = 0.</td></tr></tbody></table>
|  | The /GRPH flag is ignored when HDF5LoadData is called from a preemptive thread. |
| <span class="table-cell-nowrap">/IGOR = *attributesMask*</span> | When loading a dataset, this flag determines whether or not HDF5LoadData looks for attributes written by HDF5SaveData which store wave properties such as units and scaling. |
|  | If *attributesMask* is 0, HDF5LoadData does not look for IGOR-related attributes. If the /IGOR flag is omitted it behaves like /IGOR=0. |
|  | If *attributesMask* is -1, HDF5LoadData looks for all IGOR-related attributes. This is recommended if you intend to load the data back into Igor which was previously written out by HDFSaveData. |
|  | Otherwise *attributesMask* is a bitwise mask. The meaning of each bit is explained in the documentation for [HDF5SaveData](/igorpro/commands/hdf5savedata.md). |
|  | If you use the HDF5LoadData /SLAB keyword, HDF5LoadData does not attempt to set wave scaling or wave dimension label properties even if *attributesMask* calls for them. |
|  | Looking for IGOR-related attributes in a file not written by HDF5SaveData does no harm but slightly slows HDF5LoadData down. |
| <span class="table-cell-nowrap">/N = *name*</span> | *name* is the name to be used for the loaded wave. If /N is omitted, the name used is a possibly cleaned up version of the name of the dataset or attribute. |
|  | When loading most types of datasets or attributes, just one wave is created. |
|  | When loading a variable-length dataset or attribute, one wave is created for each loaded element. In this case, *name* is treated as a base name. For details see [HDF5 Variable-Length Data](/igorpro/data/igor-hdf5-guide.md#hdf5-variable-length-data). |
|  | When loading a single member of a compound dataset, *name* is the name to be used for the loaded wave. When loading all members of a compound dataset or attribute, *name* is used as a base name. See [HDF5 Compound Data](/igorpro/data/igor-hdf5-guide.md#hdf5-compound-data) for details. |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing waves in case of a name conflict. If /O is omitted, HDF5LoadData chooses wave names that don't conflict with existing objects. |
| <span class="table-cell-nowrap">/OPTS = *options*</span> | Controls aspects of loading data. |
|  | /OPTS requires Igor Pro 9.00 or later. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>If set, HDF5LoadData loads 64-bit integer data as 64-bit integer. If cleared, it loads 64-bit integer data as double-precision floating point.</td></tr><tr><td>Bit&nbsp;1:</td><td>If set, HDF5LoadData checks each loaded text wave and sets the wave&#39;s text data text encoding to binary if any element contains control characters other than carriage-return, linefeed, and tab. If cleared, no check for binary is done.</td></tr></tbody></table>
|  | Bit 1 defaults to 0. If you load string datasets that contain binary data, we recommend that you use /OPTS with bit 1 set. See [Text Waves Containing Binary Data](/igorpro/igor-basics/text-encodings.md#text-waves-containing-binary-data) for background information. |
|  | For backward compatibility, bit 0 defaults to 0. If you omit /OPTS, 64-bit integer data is loaded as double-precision floating point. |
|  | All other bits are reserved and must be set to zero. |
| <span class="table-cell-nowrap">/Q</span> | Be quiet. Suppresses normal diagnostic messages. |
| <span class="table-cell-nowrap">/SLAB = *slabWave*</span> | Used to load a subset of a dataset. |
|  | *slabWave* is a two-dimensional, numeric wave with exactly four columns and a number of rows greater than or equal to the number of dimensions in the dataset being loaded. *slabWave* defines a hyperslab used during the load. |
|  | When loading an attribute, /SLAB is ignored. |
|  | See [HDF5 Dataset Subsets](/igorpro/data/igor-hdf5-guide.md#hdf5-dataset-subsets) for details. |
| /T=*showInTable* |<table class="nested-table"><tbody><tr><td>*showInTable&nbsp;=*&nbsp;0:</td><td>Do not show loaded wave in table.</td></tr><tr><td>*showInTable&nbsp;=*&nbsp;1:</td><td>Show loaded wave in a new table.</td></tr><tr><td>*showInTable&nbsp;=*&nbsp;2:</td><td>Append loaded wave to top table.</td></tr></tbody></table>
|  | If *showInTable* is 2 but there are no tables, a new table is created as if *showInTable* were 1. |
|  | The /T flag is ignored when HDF5LoadData is called from a preemptive thread. |
| /TRAN=*transpose* |<table class="nested-table"><tbody><tr><td>*transpose*&nbsp;=&nbsp;0:</td><td>Normal load, no transpose (default).</td></tr><tr><td>*transpose*&nbsp;=&nbsp;1:</td><td>Transposes the multi-dimensional numeric data after loading. This works only when loading data into multi-dimensional, numeric (real or complex) waves and is ignored for 1D and text waves. See [HDF5 Images Versus Igor Images](/igorpro/data/igor-hdf5-guide.md#hdf5-images-versus-igor-images) for details.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/TYPE = *objectType*</span> | *objectType* specifies the type of the object referenced by *nameStr*. This is required only if you are loading an attribute. It tells HDF5LoadData the type of object to which the attribute is attached. |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Group</td></tr><tr><td>2:</td><td>Dataset (default)</td></tr><tr><td>3:</td><td>Named datatype</td></tr></tbody></table>
| <span class="table-cell-nowrap">/VAR = *varMode*</span> | *varMode* = 0: Load the dataset into a wave even if it is marked with the IGORVariable attribute. This is provided for the convenience of the HDF5 Browser and is probably of no use otherwise. |
|  | *varMode* = 1: Look for the IGORVariable attribute and, if it is present, load the dataset into an Igor numeric or string variable. This is the default setting. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Output Variables* {#output-variables}
HDF5LoadData sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |
| S_waveNames | Set to a semicolon-separated list of the loaded waves. |

### *Example* {#example}

```igor
Function Example(datasetName)
	String datasetName

	Variable fileID
	HDF5OpenFile /R /Z fileID as ""	// Displays a dialog
	if (V_flag == 0)	// User selected a file?
		HDF5LoadData /O fileID, datasetName
		HDF5CloseFile fileID
	endif
End
```

### *See Also* {#see-also}
[HDF5CreateFile](/igorpro/commands/hdf5createfile.md), [HDF5OpenFile](/igorpro/commands/hdf5openfile.md), [HDF5CloseFile](/igorpro/commands/hdf5closefile.md), [HDF5FlushFile](/igorpro/commands/hdf5flushfile.md), [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md), [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md), [HDF5CloseGroup](/igorpro/commands/hdf5closegroup.md)

See [HDF5 Compound Data](/igorpro/data/igor-hdf5-guide.md#hdf5-compound-data) for information on loading compound data (structures).

See [HDF5 Images Versus Igor Images](/igorpro/data/igor-hdf5-guide.md#hdf5-images-versus-igor-images) for special considerations when loading images.

See [HDF5 Bitfield Data](/igorpro/data/igor-hdf5-guide.md#hdf5-bitfield-data) for details on bitfield data.

See [Loading HDF5 Enum Data](/igorpro/data/igor-hdf5-guide.md#loading-hdf5-enum-data) for details on enum data.

See [HDF5 Opaque Data](/igorpro/data/igor-hdf5-guide.md#hdf5-opaque-data) for details on opaque data.

See [HDF5 Variable-Length Data](/igorpro/data/igor-hdf5-guide.md#hdf5-variable-length-data) for details on variable-length data.

See [Loading HDF5 Reference Data](/igorpro/data/igor-hdf5-guide.md#loading-hdf5-reference-data) for details on loading reference data.

See [HDF5 Dataset Subsets](/igorpro/data/igor-hdf5-guide.md#hdf5-dataset-subsets) for details on using hyperslabs.

See [HDF5 Array Data](/igorpro/data/igor-hdf5-guide.md#hdf5-array-data) for a discussion of loading datasets whose elements consist of arrays.

See [HDF5 Attributes](/igorpro/data/igor-hdf5-guide.md#hdf5-attributes) for a discussion of loading attributes of groups and datasets.