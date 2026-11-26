---
description: "The SaveTableCopy operation saves a copy of the data displayed in a table on disk."
slug: /commands/savetablecopy
---

<div className="command-signature">

## <strong>SaveTableCopy</strong>  [/A=<em>a</em> /I/M=<em>termStr</em> /N=<em>n</em> /O/P=<em>pathName</em> /S=<em>s</em> /T=<em>saveType</em> /F=<em>f</em>  /W=<em>winName</em>  /Z ] [<em>as</em> <em>fileNameStr</em> ] {#savetablecopy}

</div>

The SaveTableCopy operation saves a copy of the data displayed in a table on disk. The saved file can be an Igor packed experiment file, a tab-delimited text file, or a comma-separated values text file.

When saving as text, by default the data format matches the format shown in the table. This causes truncation if the underlying data has more precision than shown in the table. If you specify /F=1, SaveTableCopy uses as many digits as needed to represent the data with full precision.

The point column is never saved.

When saving 3D and 4D waves as text, only the visible layer is saved. To save the entirety of a 3D or 4D wave, use the [Save](/igorpro/commands/save.md) operation.

### *Parameters* {#parameters}
The file to be written is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If Igor cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *a*</span> | Appends data to the file rather than overwriting. |
|  |<table class="nested-table"><tbody><tr><td>*a*&nbsp;=0:</td><td>Does not append.</td></tr><tr><td>*a*&nbsp;=1:</td><td>Appends to the file with a blank line before the appended data.</td></tr><tr><td>*a*&nbsp;=2:</td><td>Appends to the file with no blank line before the appended data.</td></tr></tbody></table>
|  | /A applies when saving text files and is ignored when saving packed experiment files. |
|  | If the file does not exist, a new file is created and /A has no effect. |
| <span class="table-cell-nowrap">/COMP = {*minWaveElements, gzipLevel, shuffle*}</span> |  |
|  | Specifies that compression is to be applied to numeric waves saved when saving as an HDF5 packed experiment file. The /COMP flag was added in Igor Pro 9.00. |
|  | *minWaveElements* is the minimum number of elements that a numeric wave must have to be eligible for compression. Waves with fewer than this many total elements are not compressed. |
|  | *gzipLevel* is a value from 0 to 9. 0 means no GZIP compression. |
|  | *shuffle* is 0 to turn shuffle off or 1 to turn shuffle on. |
|  | When compression is applied by SaveTableCopy, the entire wave is saved in one chunk. See [HDF5 Layout Chunk Size](/igorpro/data/igor-hdf5-guide.md#hdf5-layout-chunk-size) for background information and [SaveExperiment Compression](/igorpro/data/igor-hdf5-guide.md#saveexperiment-compression) for details. |
| <span class="table-cell-nowrap">/F = *f*</span> | Controls the precision of saved numeric data when writing as text. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>Numeric data is written exactly as shown in the table. This may cause trunctation. This is the default behavior if /F is omitted.</td></tr><tr><td>*f*&nbsp;=1:</td><td>Numeric data is written with as many digits as needed to represent the data with full precision.</td></tr></tbody></table>
|  | The /F flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/I</span> | Presents a dialog from which you can specify file name and folder. |
| <span class="table-cell-nowrap">/M = *termStr*</span> | Specifies the terminator character or characters to use at the end of each line of text. The default is /M="\r\n"; it is used when /M is omitted. To use the Unix convention, just a linefeed, specify /M="\n". |
| <span class="table-cell-nowrap">/N = *n*</span> | Specifies whether to use column names, titles, or dimension labels. |
|  | *n* is a bitwise parameter with the bits defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Include column names or titles. The column title is included if it is not empty. If it is empty, the column name is included.</td></tr><tr><td>Bit&nbsp;1:</td><td>Include horizontal dimension labels if they are showing in the table.</td></tr></tbody></table>
|  | The default setting for *n* is 1. |
|  | All other bits are reserved and must be zero. |
| <span class="table-cell-nowrap">/O</span> | Overwrites file if it exists already. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to store the file in. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/S = *s*</span> | Saves all of the data in the table (*s* =0; default) or the selection only (*s* =1) |
|  | /S applies when saving text files and is ignored when saving packed experiment files. |
| <span class="table-cell-nowrap">/T = *saveType*</span> | Specifies the file format of the saved file. |
|  |<table class="nested-table"><tbody><tr><td>*saveType*&nbsp;=&nbsp;0:</td><td>Packed experiment file.</td></tr><tr><td>*saveType*&nbsp;=&nbsp;1:</td><td>Tab-delimited text file.</td></tr><tr><td>*saveType*&nbsp;=&nbsp;2:</td><td>Comma-separated values text file.</td></tr><tr><td>*saveType*&nbsp;=&nbsp;3:</td><td>Space-delimited values text file.</td></tr><tr><td>*saveType*&nbsp;=&nbsp;4:</td><td>HDF5 packed experiment file (requires Igor Pro 9 or later). If *fileNameStr* is specified, the file name extension must be &quot;.h5xp&quot;.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/W = *winName*</span> | *winName* is the name of the table to be saved. If /W is omitted or if *winName* is "", the top table is saved. |
| <span class="table-cell-nowrap">/Z</span> | Errors are not fatal and error dialogs are suppressed. See Details. |

### *Details* {#details}
The main uses for saving as a packed experiment are to save an archival copy of data or to prepare to merge data from multiple experiments (see [Merging Experiments](/igorpro/igor-basics/experiments-files-and-folders.md#merging-experiments)). The resulting experiment file preserves the data folder hierarchy of the waves displayed in the table starting from the "top" data folder, which is the data folder that encloses all waves displayed in the table. The top data folder becomes the root data folder of the resulting experiment file. Only the table and its waves are saved in the packed experiment file, not variables or strings or any other objects in the experiment.

SaveTableCopy does not know about dependencies. If a table contains a wave, wave0, that is dependent on another wave, wave1 which is not in the table, SaveTableCopy will save wave0 but not wave1. When the saved experiment is open, there will be a broken dependency.

The main use for saving as a tab or comma-delimited text file is for exporting data to another program.

When calling SaveTableCopy from a procedure, you should call DoUpdate before calling SaveTable copy. This insures that the table is up-to-date if your procedure has redimensioned or otherwise changed the number of points in the waves in the table.

SaveTableCopy sets the variable V_flag to 0 if the operation completes normally, to -1 if the user cancels, or to another nonzero value that indicates that an error occurred. If you want to detect the user canceling an interactive save, use the /Z flag and check V_flag after calling SaveTableCopy.

The [SaveData](/igorpro/commands/savedata.md) operation also has the ability to save a table to a packed experiment file. SaveData is more complex but a bit more flexible than SaveTableCopy.

### *Examples* {#examples}
This function saves all tables to a single tab-delimited text file.


```igor
Function SaveAllTablesToTextFile(pathName, fileName)
	String pathName	// Name of an Igor symbolic path.
	String fileName
	
	String tableName
	Variable index
	
	index = 0
	do
		tableName = WinName(index, 2)
		if (strlen(tableName) == 0)
			break
		endif
		
		SaveTableCopy/P=$pathName/W=$tableName/T=1/A=1 as fileName
		
		index += 1
	while(1)
End
```

### *See Also* {#see-also}
[SaveGraphCopy](/igorpro/commands/savegraphcopy.md), [SaveGizmoCopy](/igorpro/commands/savegizmocopy.md), [Merging Experiments](/igorpro/igor-basics/experiments-files-and-folders.md#merging-experiments), [SaveData](/igorpro/commands/savedata.md)