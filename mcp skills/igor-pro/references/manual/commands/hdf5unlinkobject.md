---
description: "The HDF5UnlinkObject operation unlinks the specified object (a group, dataset, datatype or link) from the HDF5 file."
slug: /commands/hdf5unlinkobject
---

<div className="command-signature">

## <strong>HDF5UnlinkObject</strong>  [ /Z ] <em>locationID</em>, <em>nameStr</em> {#hdf5unlinkobject}

</div>

The HDF5UnlinkObject operation unlinks the specified object (a group, dataset, datatype or link) from the HDF5 file.

Unlinking an object deletes the object from the file's hierarchy but does not free up the space in the file used by the object. The HDF Group provides a command-line utility program, h5repack, to compact HDF5 files.

If you have opened a group via HDF5CreateGroup or HDF5OpenGroup, you should close it via HDF5CloseGroup before calling HDF5UnlinkObject.

### *Parameters* {#parameters}
*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*nameStr* is a string containing the HDF5 path to the object to be unlinked.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Output Variables* {#output-variables}
HDF5UnlinkObject sets the following output variable:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |

### *See Also* {#see-also}
[HDF5CreateLink](/igorpro/commands/hdf5createlink.md)