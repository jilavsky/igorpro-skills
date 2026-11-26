---
description: "The HDF5OpenFile operation opens an existing HDF5 file for reading or for reading and writing."
slug: /commands/hdf5openfile
---

<div className="command-signature">

## <strong>HDF5OpenFile</strong>  [ /I /P=<em>pathName</em> /R /Z ] <em>fileID</em> [<em>as</em> <em>fileNameStr</em> ] {#hdf5openfile}

</div>

The HDF5OpenFile operation opens an existing HDF5 file for reading or for reading and writing.

HDF5OpenFile returns a file reference number via the *fileID* parameter. You pass this file ID to subsequent HDF5 operation and function calls.

When you are finished with the file you must call [HDF5CloseFile](/igorpro/commands/hdf5closefile.md).

To create a new HDF5 file you must call [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) instead of calling HDF5OpenFile.

### *Parameters* {#parameters}
*fileID* is the name of an Igor local variable NVAR referencing a global variable. HDF5OpenFile returns an HDF5 file ID in the named variable. You pass this file ID to subsequent HDF5 operation and function calls and to HDF5CloseFile when you are finished with the file. If for some reason the HDF5OpenFile operation fails, *fileID* is set to zero.

*fileNameStr* is a full path to the HDF5 file, or a file name or partial path relative to the Igor symbolic path specified via /P.

If *fileNameStr* is omitted or is "" or the /I flag is used, HDF5OpenFile displays an Open File dialog. HDF5OpenFile also displays an Open File dialog if the *fileNameStr* and *pathName* do not fully specify the file of interest.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/I</span> | Interactive. Displays the Open File dialog to get the file name and path. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | *pathName* is the name of an Igor symbolic path that specifies the directory to look in for *fileNameStr.* |
| <span class="table-cell-nowrap">/R</span> | Opens the file for read-only. If omitted, the file is opened for read/write. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Details* {#details}
If you do not intend to write to the file, use the /R flag. Otherwise you will get an error if you try to load a read-only file or one that is in a directory for which you do not have write permission.

When the current experiment is closed (via New Experiment, Open Experiment or Revert Experiment or by quitting Igor) Igor automatically closes all open HDF5 files.

HDFOpenFile sets the following output variables:

### *Output Variables* {#output-variables}

|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |
| S_path | Set to the path leading to the folder containing the loaded file. This is a system file path (e.g., "hd:FolderA:FolderB:"), not an Igor symbolic path. The path uses Macintosh HFS path syntax, even on Windows, and has a trailing colon. |
| S_fileName | Set to the name of the loaded file. |

### *Examples* {#examples}

```igor
Variable fileID
HDF5OpenFile /R fileID as "C:Data:test.h5"      // Windows using Macintosh path
HDF5OpenFile /R fileID as "C:\\Data\\test.h5"   // Windows using Windows path
HDF5CloseFile fileID
```

### *See Also* {#see-also}
[HDF5CreateFile](/igorpro/commands/hdf5createfile.md), [HDF5CloseFile](/igorpro/commands/hdf5closefile.md), [HDF5FlushFile](/igorpro/commands/hdf5flushfile.md), [HDF5LoadData](/igorpro/commands/hdf5loaddata.md), [HDF5LoadGroup](/igorpro/commands/hdf5loadgroup.md), [HDF5SaveData](/igorpro/commands/hdf5savedata.md), [HDF5SaveGroup](/igorpro/commands/hdf5savegroup.md), [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md), [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md), [HDF5CloseGroup](/igorpro/commands/hdf5closegroup.md)