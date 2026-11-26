---
description: "The HDF5FlushFile operation flushes an HDF5 file previously opened by HDF5OpenFile or HDF5CreateFile. If /A is used, it flushs all open HDF5 files."
slug: /commands/hdf5flushfile
---

<div className="command-signature">

## <strong>HDF5FlushFile</strong>  [/A /Z ] <em>fileID</em> {#hdf5flushfile}

</div>

The HDF5FlushFile operation flushes an HDF5 file previously opened by HDF5OpenFile or HDF5CreateFile. If /A is used, it flushs all open HDF5 files.

Flushing a file writes all modified data associated with the file to disk. This is usually not necessary as the file is automatically flushed when it is closed. In situations where you are writing data to a file over a long period of time, you may want to flush the file so that the data is preserved in the event of a power failure or crash.

### *Parameters* {#parameters}
*fileID* is the file ID number returned by [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md).

If /A is used, *fileID* is ignored but must still be present. You can pass zero in this case.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Flush all open HDF5 files. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Output Variables* {#output-variables}
HDF5FlushFile sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |

### *Example* {#example}

```igor
Variable fileID
HDF5OpenFile /R fileID as "hd:Data:test.h5"
// ... write to file ...
HDF5FlushFile fileID
// ... some time later
HDF5CloseFile fileID
```

### *See Also* {#see-also}
[HDF5CreateFile](/igorpro/commands/hdf5createfile.md), [HDF5OpenFile](/igorpro/commands/hdf5openfile.md), [HDF5CloseFile](/igorpro/commands/hdf5closefile.md)