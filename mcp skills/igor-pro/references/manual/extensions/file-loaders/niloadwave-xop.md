---
description: "NILoadWave is an external operation that loads data from Nicolet Instruments files into Igor waves. At present, NILoadWave supports Nicolet WFT files only."
slug: /extensions/file-loaders/niloadwave-xop
---

NILoadWave is an external operation that loads data from Nicolet Instruments files into Igor waves. At present, NILoadWave supports Nicolet WFT files only. This version of NILoadWave requires Igor Pro 6.38 or later.

NILoadWave adds the following to Igor:

A menu item, Load Nicolet File, in the Load Waves submenu.

A command line operation, NILoadWave.

NILoadWave sets the standard Igor file-loader output variables:

|  |  |
| --- | --- |
| S_path | Set to the path leading to the folder containing the loaded file. This is a system file path (e.g., "hd:FolderA:FolderB:"), not an Igor symbolic path. The path uses Macintosh path syntax, even on Windows, and has a trailing colon. |
| S_fileName | Set to the name of the loaded file. |
| V_flag | Set to the number of waves loaded. |
| S_waveNames | Set to a semicolon-separated list of the loaded waves. |

When NILoadWave loads a file that contains multiple zones (timebases), it also creates an X wave against which the multi-zone data wave can be plotted. The V_flag variable does not take this X wave into account.

## Revision Notes {#revision-notes}

|  |  |
| --- | --- |
| 1.20 | Ported to Windows. This version requires Igor Pro 3.13 or later on Macintosh and Windows. |
| 1.21 | Added creation of the S_path file loader variable. |
| 1.30 | Revamped to allow NILoadWave to be called directly from a user function. |
| 1.31 | Fixed bug in Windows version that sometimes caused the Open File dialog to return error 12290 (invalid filename). |
| 1.32 | Supported long file names on Macintosh. |
| 1.50 | This version requires Igor Pro 6.38 or later. |
|  | Ported to 64 bits on Macintosh and Windows. |
| 1.51 | Recompiled with XOP Toolkit 7.01 to support Igor Pro 8 on 64-bit Macintosh. |


<div className="command-signature">

## <strong>NILoadWave</strong>  [/P=<em>pathName</em>  /D /A[=<em>baseName</em>] /N[=<em>baseName</em>] /O /I /Q] <em>fileNameStr</em> {#niloadwave}

</div>

The NILoadWave operation loads data from the Nicolet WFT file into one or more waves.

### *Parameters* {#parameters}
If the file to be loaded is not fully specified by *fileNameStr* and /P=*pathName*, or if the /I flag is used, NILoadWave displays an open file dialog.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for *fileNameStr. pathName* is the name of an Igor symbolic path that you create using the NewPath operation or the New Path dialog (Misc menu). |
| <span class="table-cell-nowrap">/D</span> | Creates double precision waves. If you omit /D, NILoadWave creates single precision waves. |
| <span class="table-cell-nowrap">/A</span> | Automatically assigns wave names of the form wave0, wave1. Skips names already in use. |
| <span class="table-cell-nowrap">/A = *baseName*</span> | Automatically assigns wave names of the form baseName0, baseName1. Skips names already in use. |
| <span class="table-cell-nowrap">/N</span> | Automatically assigns wave names of the form wave0, wave1. Overwrites existing waves. |
| <span class="table-cell-nowrap">/N = *baseName*</span> | Automatically assigns wave names of the form baseName0, baseName1. Overwrites existing waves. |
| <span class="table-cell-nowrap">/O</span> | Overwrites existing waves. |
| <span class="table-cell-nowrap">/I</span> | Forces NILoadWave to display a open file dialog that allows the user to interactively choose the file to be loaded. |
| <span class="table-cell-nowrap">/Q</span> | Suppresses the normal messages in the history area. |

### *Details* {#details}

If you fully specify the file, NILoadWave will load the file without displaying an open file dialog. You can fully specify the file using a symbolic path (/P flag) and a file name or using a full path for the file name.

NILoadWave will display an open file dialog if you use the /I flag or if you don't provide enough information to fully identify the file. For example, if the specified file does not exist or does not exist in the specified folder, NILoadWave will display an open file dialog.

Use /D to create double-precision waves. Otherwise, NILoadWave will create single-precision waves.

The /N flag instructs NILoadWave to automatically name new waves “wave” (or *baseName*  if /N=*baseName*  is used) plus a number. The number starts from zero and increments by one for each wave loaded from the file. If the resulting name conflicts with an existing wave, the existing wave is overwritten.

The /A flag is like /N except that Igor skips names already in use.

If you use neither the /A nor the /N flag, NILoadWave will attempt to use the waveform title, as stored in the Nicolet file, as a wave name. If necessary, NILoadWave will clean the title up and truncate it. If the resulting name is not suitable (e.g., it conflicts with the name of an Igor operation or function), or if the file contains no waveform title, NILoadWave will substitute a default name like wave0.

NILoadWave sets the standard Igor file-loader output variables:

|  |  |
| --- | --- |
| S_path | Set to the path leading to the folder containing the loaded file. This is a system file path (e.g., "hd:FolderA:FolderB:"), not an Igor symbolic path. The path uses Macintosh path syntax, even on Windows, and has a trailing colon. |
| S_fileName | Set to the name of the loaded file. |
| V_flag | Set to the number of waves loaded. |
| S_waveNames | Set to a semicolon-separated list of the loaded waves. |

When NILoadWave loads a file that contains multiple zones (timebases), it also creates an X wave against which the multi-zone data wave can be plotted. The V_flag variable does not take this X wave into account. The name of the X wave is the base name plus "_X".

### *Examples* {#examples}
This example loads a wave from a test file into a wave named wave0, overwriting wave0 if it already exists, and then displays the wave:

```igor
NewPath/O Nicolet, "Howard2:Nicolet Files"
NILoadWave/O/N=wave/P=Nicolet "1000 Point Waveform.wft"
Display wave0
```

This example does the same thing as the preceding example. However, in this case, the Nicolet file contains 3 zones (timebases). Therefore, NILoadWave automatically creates an X wave against which the data wave can be plotted. Also, this example uses a full path to identify the file rather than a symbolic path and file name.

```igor
NILoadWave/O/N=wave/P=Nicolet "Howard2:Nicolet Files:Three Zones.wft"
Display wave0 vs wave_X
```