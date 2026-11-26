---
description: "The HDF5CreateGroup operation creates an HDF5 group in the HDF5 file. It returns a group ID via groupID."
slug: /commands/hdf5creategroup
---

<div className="command-signature">

## <strong>HDF5CreateGroup</strong>  [ /Z ] <em>locationID</em>, <em>nameStr</em>, <em>groupID</em> {#hdf5creategroup}

</div>

The HDF5CreateGroup operation creates an HDF5 group in the HDF5 file. It returns a group ID via *groupID*.

If the specified group already exists, HDF5CreateGroup just returns a group ID via *groupID*.

You can close the group by calling HDF5CloseGroup when you are finished with it. If you do no close a group, it is closed when you close the file using HDF5CloseFile.

### *Parameters* {#parameters}
*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*nameStr* is a string containing the HDF5 path to the group to be created. This can be a full HDF5 path or a simple name or partial HDF5 path relative to *locationID*.

For example, to create a group named GroupA at the root level of the file, you would pass the HDF5 file ID as the *locationID* parameter and "GroupA" or "/GroupA" as the *nameStr* parameter.

To create a group named GroupB inside GroupA, you could pass any of the following:


```igor
locationID = any file or group ID and nameStr = "/GroupA/GroupB"
locationID = file ID and nameStr = "GroupA/GroupB"
locationID = GroupA ID and nameStr = "GroupB"
```

HDF5CreateGroup creates just one group. For example, if you pass "/GroupA/GroupB" as *locationID* then GroupA must already exist in the root. Otherwise HDF5CreateGroup returns an error.

*groupID* is the name of an Igor local variable or NVAR referencing a global variable. HDF5CreateGroup returns an HDF5 group ID number in the named variable. You pass this group ID to subsequent HDF5 operation and function calls and to HDF5CloseGroup when you are finished with the group. If for some reason the HDF5CreateGroup operation fails, *groupID* is set to zero.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/SIZE = *groupSize*</span> | *groupSize* is the suggested number of bytes to reserve to store the names which will be eventually added to the new group. This flag is for advanced HDF5 users only. *groupSize* is passed as the size_hint parameter to the HDF5 library's H5Gcreate function. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Output Variables* {#output-variables}
HDF5CreateGroup sets the following output variable:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |