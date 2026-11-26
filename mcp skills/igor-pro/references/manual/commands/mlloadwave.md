---
description: "The MLLoadWave operation loads data from the named Matlab MAT file into single 1D waves (vectors), multidimensional waves (matrices), numeric variables or…"
slug: /commands/mlloadwave
---

<div className="command-signature">

## <strong>MLLoadWave</strong>  [/Q/O/B/I/A[=<em>baseName</em>]/N[=<em>name</em>]/P=<em>pathName</em> /R/C/M[=<em>m</em>]/Y=<em>y</em>/T/E/V/S[=<em>s</em>]/G/Z] <em>fileNameStr</em> {#mlloadwave}

</div>

The MLLoadWave operation loads data from the named Matlab MAT file into single 1D waves (vectors), multidimensional waves (matrices), numeric variables or string variables.

For background information, including configuration instructions, see [Loading Matlab MAT Files](/igorpro/data/importing-and-exporting-data.md#loading-matlab-mat-files).

### *Parameters* {#parameters}
The file to be loaded is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If LoadWave cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

If *fileNameStr* is omitted or is "" or the /I flag is used, MLLoadWave displays an Open File dialog in which you locate the file to be loaded.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A[ = *name*]</span> | Assign wave names using "wave" or *name* , if present, as the name or base name. Skips names already in use. |
| <span class="table-cell-nowrap">/B</span> | This flag is obsolete and is ignored. Previously it was required to tell MLLoadWave the byte order of the data in the file. MLLoadWave now determines the byte order automatically. |
| <span class="table-cell-nowrap">/C</span> | Loads columns from a Matlab matrix into an Igor 1D wave. Use /R to load rows. |
| <span class="table-cell-nowrap">/E</span> | Skips empty Matlab matrices. |
| <span class="table-cell-nowrap">/G</span> | Tells Igor to make numeric and string variables global when called from a macro. When called from a user-defined function or from the command line, variables are always created as globals. |
| <span class="table-cell-nowrap">/I</span> | Interactive. Displays the Open File dialog to get the path to the file. |
| /M=*m* |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=1:</td><td>Loads an entire Matlab matrix into an Igor 1D wave. This is the default if you omit /M.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Loads an entire Matlab matrix into an Igor multidimensional wave.</td></tr><tr><td>*m*&nbsp;=3:</td><td>Loads an entire Matlab matrix into a transposed Igor multidimensional wave.</td></tr></tbody></table>
|  | /M by itself is equivalent to /M=1. |
|  | Starting with Igor Pro 8.00, after loading a matrix that results in an Mx1 2D wave, MLLoadWave automatically redimensions the wave as an M-row 1D wave. |
| <span class="table-cell-nowrap">/N[ = *name* ]</span> | Assign wave names using "wave" or *name* , if present, as the name or base name. Overwrites existing waves if the name is already in use. |
| <span class="table-cell-nowrap">/O</span> | Overwrites existing waves and variables in case of a name conflict. If /O is omitted, MLLoadWave chooses names that don’t conflict with existing objects. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the specified file or folder. *pathName* is the name of an existing Igor symbolic path. |
| <span class="table-cell-nowrap">/Q</span> | Be quiet. Suppresses normal diagnostic messages. |
| <span class="table-cell-nowrap">/R</span> | Loads rows from a Matlab matrix into an Igor 1D wave. Use /C to load columns. |
| /S=*s* |<table class="nested-table"><tbody><tr><td>s=1:</td><td>Skips Matlab string matrices.</td></tr><tr><td>s=2:</td><td>Loads Matlab string matrices into Igor string variables. This is the default if /S is omitted.</td></tr><tr><td>s=3:</td><td>Loads Matlab string matrices into Igor text waves.</td></tr></tbody></table>
|  | /S by itself is equivalent to /S=1. |
| <span class="table-cell-nowrap">/T</span> | Displays the loaded waves in a new table. |
| <span class="table-cell-nowrap">/V</span> | Skips Matlab numeric variables (numeric matrices with one element). |
| <span class="table-cell-nowrap">/Y = *y*</span> | Specifies the number type of the numeric waves to be created. The allowed codes for y are: |
|  |<table class="nested-table"><tbody><tr><td>2:</td><td>Single-precision floating point</td></tr><tr><td>4:</td><td>Double-precision floating point</td></tr><tr><td>8:</td><td>8-bit signed integer</td></tr><tr><td>16:</td><td>16-bit signed integer</td></tr><tr><td>32:</td><td>32-bit signed integer</td></tr><tr><td>72:</td><td>8-bit signed integer</td></tr><tr><td>80:</td><td>16-bit signed integer</td></tr><tr><td>96:</td><td>32-bit signed integer</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Interactive load. Displays a dialog presenting options for each Matlab matrix in the file. |

### *MLLoadWave Wave Naming* {#mlloadwave-wave-naming}
If neither /A, /A[=*name* ], /N, or N[=*name* ] is used then the waves names are taken from the matrix name, as stored in the Matlab file.

When loading 1D waves, the /N flag instructs MLLoadWave to automatically name new waves "wave" (or *name* if /N=*name* is used) plus a number. The number starts from zero and increments by one for each wave loaded from the file. When loading multidimensional waves, *name* is used without an appended number.

The /A flag is like /N except that MLLoadWave skips names already in use.

If you specify /M=2 (load matrix into matrix) or /M=3 (load matrix into transposed matrix), MLLoadWave uses the name without appending any digits. For example, if you have a 5x3 matrix in a file and you tell MLLoadWave to load it as a matrix using the name "mat", MLLoadWave will name the matrix "mat". However, if you tell MLLoadWave to load the matrix as 3 1D waves, it will use "mat0", "mat1" and "mat2".

If the name that MLLoadWave would use when creating a wave or variable is in use for an object of the same type and if you use the overwrite flag, then it will overwrite the existing object. If you do not tell MLLoadWave to overwrite, it will choose a non-conflicting name. If the conflict is with an object of a different type or with an operation or function, MLLoadWave will also choose a non-conflicting name.

### *Loading Strings from Matlab Files* {#loading-strings-from-matlab-files}
When loading Matlab strings into Igor, you can tell MLLoadWave to create Igor string variables or Igor text waves. For example, if you have a 2x8 string matrix, MLLoadWave can create two string variables (/S=2) or one text wave (/S=3) containing two elements.

When loading Matlab string data into an Igor wave, the Igor wave will be of dimension one less than the Matlab data set. This is because each element in a Matlab string data set is a single byte whereas each element in an Igor string wave is a string (any number of bytes).

### *Loading Numeric Variables from Matlab Files* {#loading-numeric-variables-from-matlab-files}
MLLoadWave loads numeric matrices with one element into Igor numeric variables. It loads all other numeric matrices into Igor waves.

When called from a macro, MLLoadWave creates local numeric and string variables unless you use the /G flag which tells it to create global variables. When called from the command line or from a user-defined function, MLLoadWave always creates global variables. Macros should be avoided in new programming.

### *Automatic Redimensioning from 2D to 1D* {#automatic-redimensioning-from-2d-to-1d}
Starting with Igor Pro 8.00, after loading a matrix that results in an Mx1 2D wave, MLLoadWave automatically redimensions the wave as an M-row 1D wave.

This automatic redimensioning not affect the naming of the wave. It is still named using the 2D rules explained above under *MLLoadWave Wave Naming.*

### *Loading 3D and 4D Data from Matlab Files* {#loading-3d-and-4d-data-from-matlab-files}
For a discussion of how MLLoadWave handles 3D and 4D Matlab data, see [Numeric Data Loading Modes](/igorpro/data/importing-and-exporting-data.md#numeric-data-loading-modes).

### *Specifying Loading Options for Each Matlab Matrix* {#specifying-loading-options-for-each-matlab-matrix}
The /Z flag instructs MLLoadWave to load each Matlab object (matrix, vector, variable, string) step by step. MLLoadWave presents a dialog for each Matlab object in the file. You can choose to load or skip the object. If you omit the /Z flag, MLLoadWave will load all objects in the file without presenting any dialogs.

### *Output Variables* {#output-variables}
MLLoadWave sets the following output variables:


|  |  |
| --- | --- |
| S_path | File system path to the folder containing the file. |
|  | This is a system file path (e.g., "hd:FolderA:FolderB:"), not an Igor symbolic path. The path uses Macintosh path syntax, even on Windows, and has a trailing colon. |
| S_fileName | Name of the loaded file. |
| V_Flag | Number of waves created. |
| V_Flag1 | Number of Matlab data sets (2D, 3D, or 4D) loaded. |
| V_Flag2 | Number of waves created. |
| V_Flag3 | Number of numeric variables created. |
| V_Flag4 | Number of string variables created. |
| S_waveNames | Semicolon-separated list of the loaded waves. |

Prior to MLLoadWave 5.50, the variables V_Flag1, V_Flag2, V_Flag3 and V_Flag4 were named V1_Flag, V2_Flag, V3_Flag and V4_Flag.

### *See Also* {#see-also}
[Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths)

See [Loading Matlab MAT Files](/igorpro/data/importing-and-exporting-data.md#loading-matlab-mat-files) for background information, including configuration instructions.