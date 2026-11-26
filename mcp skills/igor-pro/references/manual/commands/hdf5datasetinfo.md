---
description: "The HDF5DatasetInfo function stores information about the dataset such as its rank, dimension sizes and type in the HDF5DataInfo structure referenced by di."
slug: /commands/hdf5datasetinfo
---

<div className="command-signature">

## <strong>HDF5DatasetInfo</strong> (<em>locationID</em>, <em>datasetNameStr</em>, <em>options</em>, <em>di</em>) {#hdf5datasetinfo}

</div>

The HDF5DatasetInfo function stores information about the dataset such as its rank, dimension sizes and type in the [HDF5DataInfo](/igorpro/programming/structures/hdf5datainfo.md) structure referenced by *di*.

Before passing the structure to HDF5DatasetInfo you you must initialize it as shown in the example below.

The function result is non-zero if an error occurred (typically a bad parameter) or zero if no error occurred.

HDF5DatasetInfo cannot be called from Igor's command line or from a macro. It must be called from a user-defined function.

Prior to Igor Pro 9.00, HDF5DatasetInfo was implemented in an XOP and could be called without assigning its result to anything. It is now built-in so you must assign the function result to a variable as shown in the example below.

### *Parameters* {#parameters}
*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*datasetNameStr* is the HDF5 path to the dataset of interest.

For example, to obtain information about a dataset at the root level of the file, you would pass the HDF5 file ID as the *locationID* parameter and "/\<dataset\>" as the *datasetNameStr* parameter, where \<dataset\> is the name of the dataset.

To obtain information about a dataset in the group "/images", you could pass the HDF5 file ID as the *locationID* parameter and "/images/\<dataset\>" as the *datasetNameStr* parameter or you could pass an HDF5 group ID obtained from HDF5CreateGroup or HDF5OpenGroup as the *locationID* parameter and "\<dataset\>" as the *datasetNameStr* parameter.

*options* is a bitwise parameter:


|  |  |
| --- | --- |
| Bit 0: | Suppress errors. Normally this should be set to zero so that if an error occurs (typically a bad parameter), Igor displays an error dialog. Set to 1 to suppress this normal error handling to handle errors yourself. |
| Bit 1: | Get array information. Used for H5T_ARRAY class data only. Returns an error if called for other classes of data. |
|  | Returns information about the array base type of the dataset rather than about the dataset itself. For example, if the dataset is class H5T_ARRAY and consists of 10 rows, and if the array is a 5x4 array of signed 32-bit integers, with bit 1 set, HDF5DatasetInfo returns 5x4 (instead of 10) as the dimensionality and H5T_INTEGER (instead of H5T_ARRAY) as the class. |
|  | All other bits are reserved and must be set to zero. |
| Bit 2: | Returns extended information regarding layout, chunking, and compression filters for use by advanced HDF5 users. See [HDF5DataInfo](/igorpro/programming/structures/hdf5datainfo.md) for details. |
|  | This bit requires Igor Pro 9.00 or later. |

See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

*di* is a reference to an [HDF5DataInfo](/igorpro/programming/structures/hdf5datainfo.md) structure. Before passing the structure to HDF5DatasetInfo you you must initialize it by calling InitHDF5DataInfo as shown in the example below. InitHDF5DataInfo is defined in the "HDF5 Browser.ipf" procedure file which is automatically loaded when Igor is launched.

### *Example* {#example}

```igor
Function Example()
	STRUCT HDF5DataInfo di
	InitHDF5DataInfo(di)	// Initialize structure
	Variable fileID
	HDF5OpenFile /R fileID as "hd:Data:test.h5"
	int dummy = HDF5DatasetInfo(fileID, "/sample", 0, di)
	Print di
	HDF5CloseFile fileID
End
```

### *See Also* {#see-also}
[HDF5DataInfo](/igorpro/programming/structures/hdf5datainfo.md), [HDF5CreateFile](/igorpro/commands/hdf5createfile.md), [HDF5OpenFile](/igorpro/commands/hdf5openfile.md), [HDF5LoadData](/igorpro/commands/hdf5loaddata.md)