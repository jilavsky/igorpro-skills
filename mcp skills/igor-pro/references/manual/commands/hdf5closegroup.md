---
description: "The HDF5CloseGroup operation closes an HDF5 group that you opened via HDFCreateGroup or HDF5OpenGroup."
slug: /commands/hdf5closegroup
---

<div className="command-signature">

## <strong>HDF5CloseGroup</strong>  [ /Z ] <em>groupID</em> {#hdf5closegroup}

</div>

The HDF5CloseGroup operation closes an HDF5 group that you opened via HDFCreateGroup or HDF5OpenGroup.

If you do not call HDF5CloseGroup, any groups that you opened in a particular file are closed when you close the file using HDF5CloseFile.

### *Parameters* {#parameters}
*groupID* is the group ID that you received from HDFCreateGroup or HDF5OpenGroup.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Output Variables* {#output-variables}
HDF5CloseGroup sets the following output variable:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |