---
description: "The JCAMPLoadWave operation loads data from the named JCAMP-DX file into waves."
slug: /commands/jcamploadwave
---

<div className="command-signature">

## <strong>JCAMPLoadWave</strong>  /A[=<em>baseName</em> ] /D /H /I /N[=<em>baseName</em> ] /O /P=<em>pathName</em> /Q /R /V /W [ fileNameStr ] {#jcamploadwave}

</div>

The JCAMPLoadWave operation loads data from the named JCAMP-DX file into waves.

### *Parameters* {#parameters}
If *fileNameStr* is omitted or is "", or if the /I flag is used, JCAMPLoadWave presents an Open File dialog from which you can choose the file to load.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Automatically assigns arbitrary wave names using "wave" as the base name. Skips names already in use. |
| <span class="table-cell-nowrap">/A = *baseName*</span> | Same as /A but it automatically assigns wave names of the form *baseName0*, *baseName1*. |
| <span class="table-cell-nowrap">/D</span> | Creates double-precision waves. If omitted, JCAMPLoadWave creates single-precision waves. |
| <span class="table-cell-nowrap">/H</span> | Reads header information from JCAMP file. If you include /W, this information is stored in the wave note. If you include /V, it is stored in header variables. |
| <span class="table-cell-nowrap">/I</span> | Forces JCAMPLoadWave to display an Open File dialog even if the file is fully specified via /P and *fileNameStr* . |
| <span class="table-cell-nowrap">/N</span> | Same as /A except that, instead of choosing names that are not in use, it overwrites existing waves. |
| <span class="table-cell-nowrap">/N = *baseName*</span> | Same as /N except that Igor automatically assigns wave names of the form *baseName0*, *baseName1*. |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing waves in case of a name conflict. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for *fileNameStr.* *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/Q</span> | Suppresses the normal messages in the history area. |
| <span class="table-cell-nowrap">/R</span> | Reads data from file and creates Igor waves. |
| <span class="table-cell-nowrap">/V</span> | Set variables from header information if /H is also present. |
| <span class="table-cell-nowrap">/W</span> | Stores header information in the wave note if /R and /H are also present. |

### *Details* {#details}
The /N flag instructs Igor to automatically name new waves "wave" (or *baseName* if /N=*baseName* is used) plus a number. The number starts from zero and increments by one for each wave loaded from the file. If the resulting name conflicts with an existing wave, the existing wave is overwritten.

The /A flag is like /N except that Igor skips names already in use.

### *Output Variables* {#output-variables}
JCAMPLoadWave sets the standard Igor file-loader output variables:


|  |  |
| --- | --- |
| V_flag | Number of waves loaded or -1 if an error occurs during the file load. |
| S_fileName | Name of the file being loaded. |
| S_path | File system path to the folder containing the file. |
| S_waveNames | Semicolon-separated list of the names of loaded waves. |

S_path uses Macintosh path syntax (e.g., "hd:FolderA:FolderB:"), even on Windows. It includes a trailing colon.

When JCAMPLoadWave presents an Open File dialog and the user cancels, V_flag is set to 0 and S_fileName is set to "".

In addition, if the /V flag is used, variables are created corresponding to JCAMP-DX labels in the header. See [Variables Set By JCAMPLoadWave](/igorpro/data/importing-and-exporting-data.md#variables-set-by-jcamploadwave) for details.

### *Example* {#example}

```igor
Function LoadJCAMP(pathName, fileName)
	String pathName	// Name of Igor symbolic path or ""
	String fileName	// Full path, partial path or simple file name

	JCAMPLoadWave/P=$pathName fileName
	if (V_Flag == 0)
		Print "No waves were loaded"
		return -1
	endif
	
	NVAR VJC_NPOINTS
	Printf "Number of points: %d\r", VJC_NPOINTS
	
	SVAR SJC_YUNITS
	Printf "Y Units: %s\r", SJC_YUNITS

	return 0
End
```

### *See Also* {#see-also}
[Loading JCAMP Files](/igorpro/data/importing-and-exporting-data.md#loading-jcamp-files)