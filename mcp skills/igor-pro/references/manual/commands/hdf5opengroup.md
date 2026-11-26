---
description: "The HDF5OpenGroup operation opens an existing HDF5 group in the HDF5 file."
slug: /commands/hdf5opengroup
---

<div className="command-signature">

## <strong>HDF5OpenGroup</strong>  [ /Z ] <em>locationID</em>, <em>nameStr</em>, <em>groupID</em> {#hdf5opengroup}

</div>

The HDF5OpenGroup operation opens an existing HDF5 group in the HDF5 file.

It returns a group ID via *groupID*.

You can close the group by calling HDF5CloseGroup when you are finished with it. If you do no close a group, it is closed when you close the file using HDF5CloseFile.

### *Parameters* {#parameters}
*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*nameStr* is a string containing the HDF5 path to the group to be opened. This can be a full HDF5 path or a simple name or partial HDF5 path relative to *locationID*.

For example, to open a group named GroupA at the root level of the file, you would pass the HDF5 file ID as the *locationID* parameter and "GroupA" or "/GroupA" as the *nameStr* parameter.

To open a group named GroupB inside GroupA, you could pass any of the following:


```igor
locationID = any file or group ID and nameStr = "/GroupA/GroupB"
locationID = file ID and nameStr = "GroupA/GroupB"
locationID = GroupA ID and nameStr = "GroupB"
```

*groupID* is the name of an Igor local variable or NVAR referencing a global variable. HDF5OpenGroup returns an HDF5 group ID number in the named variable. You pass this group ID to subsequent HDF5 operation and function calls and to HDF5CloseGroup when you are finished with the group. If for some reason the HDF5OpenGroup operation fails, *groupID* is set to zero.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Output Variables* {#output-variables}
HDF5OpenGroup sets the following output variable:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |