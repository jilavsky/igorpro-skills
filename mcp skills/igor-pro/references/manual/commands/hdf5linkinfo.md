---
description: "The HDF5LinkInfo function stores information about an HDF5 link in the HDF5LinkInfoStruct structure pointed to by li."
slug: /commands/hdf5linkinfo
---

<div className="command-signature">

## <strong>HDF5LinkInfo</strong> (<em>locationID</em>, <em>pathStr</em>, <em>options</em>, <em>li</em>) {#hdf5linkinfo}

</div>

The HDF5LinkInfo function stores information about an HDF5 link in the HDF5LinkInfoStruct structure pointed to by *li*.

Before passing a structure to HDF5LinkInfo you must initialize it as shown in the example below.

The HDF5LinkInfo function was added in Igor Pro 9.00 for use by the HDF5 Browser. Most HDF5 users will never need to use it.

The function result is non-zero if an error occurred (typically a bad parameter) or zero if no error occurred.

HDF5LinkInfo cannot be called from Igor's command line or from a macro. It must be called from a user-defined function.

Because HDF5LinkInfo is a built-in function, you must assign the function result to a variable as shown in the example below.

### *Parameters* {#parameters}
*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*pathStr* is a string containing the HDF5 path to an object (group, dataset or named datatype). *pathStr* can be a full path or a partial path relative to *locationID*.

*options* is a bitwise parameter:


|  |  |
| --- | --- |
| Bit 0: | Suppress errors. Normally this should be set to zero so that if an error occurs (typically a bad parameter), Igor will display an error dialog. Set to 1 to suppress this normal error handling to handle errors yourself. |
|  | All other bits are reserved and must be set to zero. |

See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

*li* is a reference to an HDF5LinkInfoStruct structure.

### *Details* {#details}
See [HDF5LinkInfoStruct](/igorpro/programming/structures/hdf5linkinfostruct.md) for further information.

### *Example* {#example}

```igor
Function Example()
	STRUCT HDF5LinkInfoStruct li
	InitHDF5LinkInfoStruct(li)	// Initialize structure
	Variable fileID
	HDF5OpenFile /R fileID as "hd:Data:test.h5"
	int dummy = HDF5LinkInfo(fileID, "/GroupA/dataset0", 0, li)
	Print li
	HDF5CloseFile fileID
End
```

### *See Also* {#see-also}
[HDF5LinkInfoStruct](/igorpro/programming/structures/hdf5linkinfostruct.md)