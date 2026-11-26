---
description: "The HDF5TypeInfo function stores information about the datatype of a dataset or attribute in the HDF5DataTypeInfo structure referenced by dti."
slug: /commands/hdf5typeinfo
---

<div className="command-signature">

## <strong>HDF5TypeInfo</strong> (<em>locationID</em>, <em>datasetOrGroupNameStr</em>, <em>attributeNameStr</em>, <em>memberName</em>, <em>options</em>, <em>dti</em>) {#hdf5typeinfo}

</div>

The HDF5TypeInfo function stores information about the datatype of a dataset or attribute in the [HDF5DataTypeInfo](/igorpro/programming/structures/hdf5datatypeinfo.md) structure referenced by *dti*.

The HDF5TypeInfo function is for advanced users. For most purposes you do not need to call it.

Before passing the structure to HDF5TypeInfo you you must initialize it as shown in the example below.

The function result is non-zero if an error occurred (typically a bad parameter) or zero if no error occurred.

HDF5TypeInfo cannot be called from Igor's command line or from a macro. It must be called from a user-defined function.

Prior to Igor Pro 9.00, HDF5TypeInfo was implemented in an XOP and could be called without assigning its result to anything. It is now built-in so you must assign the function result to a variable as shown in the example below.

### *Parameters* {#parameters}
*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*datasetOrGroupNameStr* is the HDF5 path to the dataset or group of interest.

*attributeNameStr* is the name of the attribute of interest or "" if you want information about a dataset, not an attribute. If *datasetOrGroupNameStr* points to a group then *attributeNameStr* must be the name of an attribute because groups do not have datatypes.

If *memberName* is not "" then it specifies a member of the compound dataset or attribute of interest and HDF5TypeInfo returns information about the datatype of that member.

*options* is a bitwise parameter:


|  |  |
| --- | --- |
| Bit 0: | Suppress errors. Normally this should be set to zero so that if an error occurs (typically a bad parameter), Igor displays an error dialog. Set to 1 to suppress this normal error handling to handle errors yourself. |
| Bit 1: | If bit 1 is set then HDF5TypeInfo returns information about the base datatype of the datatype of interest. This would be used to get information about the base datatype of an array or enum dataset. |
|  | All other bits are reserved and must be set to zero. |

See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

*dti* is a reference to an [HDF5DatatypeInfo](/igorpro/programming/structures/hdf5datatypeinfo.md) structure. Before passing the structure to HDF5TypeInfo you you must initialize it by calling InitHDF5DatatypeInfo as shown in the example below. InitHDF5DatatypeInfo is defined in the "HDF5 Browser.ipf" procedure file which is automatically loaded when Igor is launched.

### *Example* {#example}

```igor
Function Example()
	STRUCT HDF5DatatypeInfo dti
	InitHDF5DatatypeInfo(dti)	// Initialize structure
	Variable fileID
	HDF5OpenFile /R fileID as "hd:Data:test.h5"
	int dummy = HDF5TypeInfo(fileID, "/sample", "", "", 0, dti)
	Print dti
	HDF5CloseFile fileID
End
```



### *See Also* {#see-also}
[HDF5DatatypeInfo](/igorpro/programming/structures/hdf5datatypeinfo.md), [HDF5CreateFile](/igorpro/commands/hdf5createfile.md), [HDF5OpenFile](/igorpro/commands/hdf5openfile.md), [HDF5LoadData](/igorpro/commands/hdf5loaddata.md)