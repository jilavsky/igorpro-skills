---
description: "The HDF5CloseFile operation closes an HDF5 file previously opened by HDF5OpenFile or HDF5CreateFile. If /A is used, it closes all open HDF5 files."
slug: /commands/hdf5closefile
---

<div className="command-signature">

## <strong>HDF5CloseFile</strong>  [ /A /Z ] <em>fileID</em> {#hdf5closefile}

</div>

The HDF5CloseFile operation closes an HDF5 file previously opened by HDF5OpenFile or HDF5CreateFile. If /A is used, it closes all open HDF5 files.

HDF5CloseFile also closes any groups that you opened via HDF5CreateGroup or HDF5OpenGroup but did not close via HDF5CloseGroup.

### *Parameters* {#parameters}
*fileID* is the file ID number returned by [HDF5OpenFile](/igorpro/commands/hdf5openfile.md).

If /A is used, *fileID* is ignored but must still be present. You can pass zero in this case.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Close all open HDF5 files. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Details* {#details}
When the current experiment is closed (via New Experiment, Open Experiment or Revert Experiment or by quitting Igor) Igor automatically closes all open HDF5 files.

### *Output Variables* {#output-variables}
HDF5CloseFile sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |

### *Example* {#example}

```igor
Variable fileID
HDF5OpenFile /R fileID as "hd:Data:test.h5"
HDF5CloseFile fileID
```

### *See Also* {#see-also}
[HDF5CreateFile](/igorpro/commands/hdf5createfile.md), [HDF5OpenFile](/igorpro/commands/hdf5openfile.md), [HDF5FlushFile](/igorpro/commands/hdf5flushfile.md), [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md), [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md), [HDF5CloseGroup](/igorpro/commands/hdf5closegroup.md)