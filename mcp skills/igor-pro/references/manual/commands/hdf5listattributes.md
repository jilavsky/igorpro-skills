---
description: "The HDF5ListAttributes operation returns a list of attributes associated with the object specified by locationID and nameStr."
slug: /commands/hdf5listattributes
---

<div className="command-signature">

## <strong>HDF5ListAttributes</strong>  [ /SEP=<em>separatorStr</em> /TYPE=<em>type</em> /Z ] <em>locationID</em>, <em>nameStr</em> {#hdf5listattributes}

</div>

The HDF5ListAttributes operation returns a list of attributes associated with the object specified by *locationID* and *nameStr*. The information is returned in the string variable S_HDF5ListAttributes. By default the list is semicolon-separated.

The /TYPE flag specifies the type of object referenced by *nameStr*.

### *Parameters* {#parameters}
*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*nameStr* is a string containing the HDF5 path to the group to be opened. This can be a full HDF5 path or a simple name or partial HDF5 path relative to *locationID*.

You must include the /TYPE flag if *nameStr* refers to a group or named datatype. If /TYPE is omitted, *nameStr* is assumed to refer to a dataset.

For example, to list the attributes of the root level of the file, you would pass the HDF5 file ID as the *locationID* parameter and "." as the *nameStr* parameter, and you would include the /TYPE=1 flag.

To list the attributes of the group "/images", you could pass the HDF5 file ID as the *locationID* parameter and "/images" as the *nameStr* parameter or you could pass an HDF5 group ID obtained from HDF5CreateGroup or HDF5OpenGroup as the *locationID* parameter and "." as the *nameStr* parameter. You would include the /TYPE=1 flag.

To list the attributes of a dataset named "image1" in the group "/images", you could pass the HDF5 file ID as the *locationID* parameter and "/images/image1" as the *nameStr* parameter or you could pass an HDF5 group ID obtained from HDF5CreateGroup or HDF5OpenGroup as the *locationID* parameter and "image1" as the *nameStr* parameter. You would include the /TYPE=2 flag or omit the /TYPE flag.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/SEP = *separatorStr*</span> |  |
|  | *separatorStr* is a one-byte string that specifies the list separator to use for S_HDF5ListAttributes. If you omit /SEP, the separator is semicolon. See **HDF5ListAttributes Separator** below for details. The /SEP flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | *type* specifies the type of object referenced by *locationID* and *nameStr* : |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>*locationID* and *nameStr* reference a group</td></tr><tr><td>2:</td><td>*locationID* and *nameStr* reference a dataset (default)</td></tr><tr><td>3:</td><td>*locationID* and *nameStr* reference a named datatype</td></tr></tbody></table>
|  | If /TYPE is omitted, *locationID* and *nameStr* are assumed to reference a dataset. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Output Variables* {#output-variables}
HDF5ListAttributes sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |
| S_HDF5ListAttributes | Set to a list of attribute names. By default the list separator is semicolon. See **HDF5ListAttributes Separator** below for details. |

### *HDF5ListAttributes Separator* {#hdf5listattributes-separator}
By default, S_HDF5ListAttributes is semicolon-separated. This is fine except for the very rare case where an HDF5 attribute name includes a semicolon character. If you want to handle that very rare case, you can use /SEP="\r" to specify carriage-return as the list separator. The /SEP flag requires Igor Pro 9.00 or later.

### *See Also* {#see-also}
[HDF5AttributeInfo](/igorpro/commands/hdf5attributeinfo.md), [HDF5 Attributes](/igorpro/data/igor-hdf5-guide.md#hdf5-attributes)