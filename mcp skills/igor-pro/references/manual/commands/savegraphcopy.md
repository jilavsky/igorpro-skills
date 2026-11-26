---
description: "The SaveGraphCopy operation saves a graph and its waves in an Igor packed experiment file."
slug: /commands/savegraphcopy
---

<div className="command-signature">

## <strong>SaveGraphCopy</strong>  [/COMP={<em>minWaveElements</em>, <em>gzipLevel</em>, <em>shuffle</em>} /I /O /P=<em>pathName</em> /T=<em>saveType</em> /W=<em>winName</em> /Z ] [<em>as</em> <em>fileNameStr</em> ] {#savegraphcopy}

</div>

The SaveGraphCopy operation saves a graph and its waves in an Igor packed experiment file.

### *Parameters* {#parameters}
The file to be written is specified by *fileNameStr*  and /P=*pathName*  where *pathName*  is the name of an Igor symbolic path. *fileNameStr*  can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If Igor cannot determine the location of the file from *fileNameStr*  and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/COMP = {*minWaveElements, gzipLevel, shuffle*}</span> |  |
|  | Specifies that compression is to be applied to numeric waves saved when saving as an HDF5 packed experiment file. The /COMP flag was added in Igor Pro 9.00. |
|  | *minWaveElements* is the minimum number of elements that a numeric wave must have to be eligible for compression. Waves with fewer than this many total elements are not compressed. |
|  | *gzipLevel* is a value from 0 to 9. 0 means no GZIP compression. |
|  | *shuffle* is 0 to turn shuffle off or 1 to turn shuffle on. |
|  | When compression is applied by SaveGraphCopy, the entire wave is saved in one chunk. See [HDF5 Layout Chunk Size](/igorpro/data/igor-hdf5-guide.md#hdf5-layout-chunk-size) for background information and [SaveExperiment Compression](/igorpro/data/igor-hdf5-guide.md#saveexperiment-compression) for details. |
| <span class="table-cell-nowrap">/I</span> | Presents a dialog from which you can specify file name and folder. |
| <span class="table-cell-nowrap">/O</span> | Overwrites file if it exists already. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to store the file in. *pathName*  is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/T = *saveType*</span> | Specifies the file format of the saved file. |
|  |<table class="nested-table"><tbody><tr><td>*saveType*&nbsp;=&nbsp;0:</td><td>Packed experiment file.</td></tr><tr><td>*saveType*&nbsp;=&nbsp;1:</td><td>HDF5 packed experiment file. If *fileNameStr* is specified, the file name extension must be &quot;.h5xp&quot;.</td></tr></tbody></table>
|  | The /T flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/W = *winName*</span> | *winName*  is the name of the graph to be saved. If /W is omitted or if *winName*  is "", the top graph is saved. |
| <span class="table-cell-nowrap">/Z</span> | Errors are not fatal and error dialogs are suppressed. See Details. |

### *Details* {#details}
The main uses for saving as a packed experiment are to save an archival copy of data or to prepare to merge data from multiple experiments (see [Merging Experiments](/igorpro/igor-basics/experiments-files-and-folders.md#merging-experiments)). The resulting experiment file preserves the data folder hierarchy of the waves displayed in the graph starting from the "top" data folder, which is the data folder that encloses all waves displayed in the graph. The top data folder becomes the root data folder of the resulting experiment file. Only the graph, its waves, dashed line settings, and any pictures used in the graph are saved in the packed experiment file, not procedures, variables, strings or any other objects in the experiment.

SaveGraphCopy does not work well with graphs containing controls. First, the controls may depend on waves, variables or FIFOs (for chart controls) that SaveGraphCopy will not save. Second, controls typically rely on procedures which are not saved by SaveGraphCopy.

SaveGraphCopy does not know about dependencies. If a graph contains a wave, wave0, that is dependent on another wave, wave1 which is not in the graph, SaveGraphCopy will save wave0 but not wave1. When the saved experiment is open, there will be a broken dependency.

SaveGraphCopy sets the variable V_flag to 0 if the operation completes normally, to -1 if the user cancels, or to another nonzero value that indicates that an error occurred. If you want to detect the user canceling an interactive save, use the /Z flag and check V_flag after calling SaveGraphCopy.

The [SaveData](/igorpro/commands/savedata.md) operation also has the ability to save data from a graph to a packed experiment file. SaveData is more complex but a bit more flexible than SaveGraphCopy.

### *Examples* {#examples}
This function saves all graphs in the experiment to individual packed experiment files.


```igor
Function SaveAllGraphsToPackedFiles(pathName)
	String pathName	// Name of an Igor symbolic path.
	
	String graphName
	Variable index
	
	index = 0
	do
		graphName = WinName(index, 1)
		if (strlen(graphName) == 0)
			break
		endif

		String fileName
		sprintf fileName, "%s.pxp", graphName
		
		SaveGraphCopy/P=$pathName/W=$graphName as fileName
		
		index += 1
	while(1)
End
```

### *See Also* {#see-also}
[SaveTableCopy](/igorpro/commands/savetablecopy.md), [SaveGizmoCopy](/igorpro/commands/savegizmocopy.md), [SaveData](/igorpro/commands/savedata.md), [Merging Experiments](/igorpro/igor-basics/experiments-files-and-folders.md#merging-experiments)