---
description: "The HDF5CreateFile operation creates a new HDF5 file or overwrites an existing HDF5 file if /O is used and then opens the file for read/write."
slug: /commands/hdf5createfile
---

<div className="command-signature">

## <strong>HDF5CreateFile</strong>  [ /I /O /P=<em>pathName</em> /Z ] <em>fileID</em> <em>as</em> <em>fileNameStr</em> {#hdf5createfile}

</div>

The HDF5CreateFile operation creates a new HDF5 file or overwrites an existing HDF5 file if /O is used and then opens the file for read/write.

If the file already exists and /O is omitted, an error is returned.

Since HDF5CreateFile opens the file after creating it, do not call HDFOpenFile.

After calling HDF5CreateFile, use [HDF5SaveData](/igorpro/commands/hdf5savedata.md) or [HDF5SaveGroup](/igorpro/commands/hdf5savegroup.md) to save data in the file. When you are finished with the file, call [HDF5CloseFile](/igorpro/commands/hdf5closefile.md).

### *Parameters* {#parameters}
*fileID* is the name of an Igor local variable or NVAR referencing a global variable. HDF5CreateFile returns an HDF5 file ID number in the named variable. You pass this file ID to subsequent HDF5 operation and function calls and to HDF5CloseFile when you are finished with the file. If for some reason the HDF5CreateFile operation fails, *fileID* is set to zero.

*fileNameStr* is a full path to the HDF5 file, or a file name or partial path relative to the Igor symbolic path specified via /P.

If *fileNameStr* is omitted or is "" or the /I flag is used, HDF5CreateFile displays an Open File dialog. HDF5CreateFile also displays an Open File dialog if the *fileNameStr* and *pathName* do not fully specify the file of interest.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/I</span> | Interactive. Displays the Open File dialog to get the file name and path. |
|  | If you use /I and want the user to be able to overwrite an existing file then you must also use /O. |
| <span class="table-cell-nowrap">/O</span> | Overwrite the file if it already exists. |
|  | If the file already exists and /O is omitted, an error is returned. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | *pathName* is the name of an Igor symbolic path that specifies the directory to look in for *fileNameStr.* |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Details* {#details}
When the current experiment is closed (via New Experiment, Open Experiment or Revert Experiment or by quitting Igor) Igor automatically closes all open HDF5 files.

### *Output Variables* {#output-variables}
HDFCreateFile sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |
| S_path | Set to the path leading to the folder containing the loaded file. This is a system file path (e.g., "hd:FolderA:FolderB:"), not an Igor symbolic path. The path uses Macintosh HFS path syntax, even on Windows, and has a trailing colon. |
| S_fileName | Set to the name of the loaded file. |

### *Examples* {#examples}

```igor
Variable fileID
HDF5CreateFile/P=<SymbolicPathName> fileID as "test.h5"
HDF5CreateFile fileID as "C:Data:test.h5"       // Windows using Mac path
HDF5CreateFile fileID as "C:\\Data\\test.h5"    // Windows using Windows path
```

### *See Also* {#see-also}
[HDF5OpenFile](/igorpro/commands/hdf5openfile.md), [HDF5CloseFile](/igorpro/commands/hdf5closefile.md), [HDF5FlushFile](/igorpro/commands/hdf5flushfile.md), [HDF5SaveData](/igorpro/commands/hdf5savedata.md), [HDF5SaveGroup](/igorpro/commands/hdf5savegroup.md), [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md), [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md), [HDF5CloseGroup](/igorpro/commands/hdf5closegroup.md)