---
description: "The SaveGizmoCopy operation saves a Gizmo window and its waves in an Igor packed experiment file."
slug: /commands/savegizmocopy
---

<div className="command-signature">

## <strong>SaveGizmoCopy</strong>  [/COMP={<em>minWaveElements</em>, <em>gzipLevel</em>, <em>shuffle</em>} /I /O /P=<em>pathName</em> /T=<em>saveType</em> /W=<em>winName</em> /Z ] [<em>fileNameStr</em> ] {#savegizmocopy}

</div>

The SaveGizmoCopy operation saves a Gizmo window and its waves in an Igor packed experiment file.

SaveGizmoCopy was added in Igor Pro 8.00.

### *Parameters* {#parameters}
The file to be written is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If Igor cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/COMP = {*minWaveElements, gzipLevel, shuffle*}</span> |  |
|  | Specifies that compression is to be applied to numeric waves saved when saving as an HDF5 packed experiment file. The /COMP flag was added in Igor Pro 9.00. |
|  | *minWaveElements* is the minimum number of elements that a numeric wave must have to be eligible for compression. Waves with fewer than this many total elements are not compressed. |
|  | *gzipLevel* is a value from 0 to 9. 0 means no GZIP compression. |
|  | *shuffle* is 0 to turn shuffle off or 1 to turn shuffle on. |
|  | When compression is applied by SaveGizmoCopy, the entire wave is saved in one chunk. See [HDF5 Layout Chunk Size](/igorpro/data/igor-hdf5-guide.md#hdf5-layout-chunk-size) for background information and [SaveExperiment Compression](/igorpro/data/igor-hdf5-guide.md#saveexperiment-compression) for details. |
| <span class="table-cell-nowrap">/I</span> | Presents a dialog from which you can specify output file name and folder. |
| <span class="table-cell-nowrap">/O</span> | Overwrites output file if it exists already. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to store the file in. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/T = *saveType*</span> | Specifies the file format of the saved file. |
|  |<table class="nested-table"><tbody><tr><td>*saveType*&nbsp;=&nbsp;0:</td><td>Packed experiment file.</td></tr><tr><td>*saveType*&nbsp;=&nbsp;1:</td><td>HDF5 packed experiment file. If *fileNameStr* is specified, the file name extension must be &quot;.h5xp&quot;.</td></tr></tbody></table>
|  | The /T flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/W = *winName*</span> | *winName* is the name of the Gizmo window to be saved. If /W is omitted or if *winName* is "", the top Gizmo window is saved. |
| <span class="table-cell-nowrap">/Z</span> | Ignore errors. |

### *Details* {#details}
The main uses for saving as a packed experiment are to save an archival copy of data or to prepare to merge data from multiple experiments (see [Merging Experiments](/igorpro/igor-basics/experiments-files-and-folders.md#merging-experiments)). The resulting experiment file preserves the data folder hierarchy of the waves used in the Gizmo window starting from the root data folder. Only the Gizmo window, its waves as well as the objects on Gizmo's object list and attribute list are saved in the packed experiment file. Associated procedures including hook functions are not saved.

SaveGizmoCopy does not know about dependencies. If a Gizmo window contains a wave, wave0, that is dependent on another wave, wave1 which is not used in the Gizmo window, SaveGizmoCopy will save wave0 but not wave1. When the saved experiment is open, there will be a broken dependency.

SaveGizmoCopy sets the variable V_flag to 0 if the operation completes normally, to -1 if the user cancels, or to another nonzero value that indicates that an error occurred. If you want to detect the user canceling an interactive save, use the /Z flag and check V_flag after calling SaveGizmoCopy.

### *See Also* {#see-also}
[SaveGraphCopy](/igorpro/commands/savegraphcopy.md), [SaveTableCopy](/igorpro/commands/savetablecopy.md), [SaveData](/igorpro/commands/savedata.md), [Merging Experiments](/igorpro/igor-basics/experiments-files-and-folders.md#merging-experiments)