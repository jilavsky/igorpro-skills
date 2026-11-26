---
description: "The Open operation can, depending on the flags passed to it: Open an existing file to read data from (/R flag without /D)."
slug: /commands/open
---

<div className="command-signature">

## <strong>Open</strong>  [ /A /C=<em>creatorStr</em>  /D[=<em>mode</em> ] /F=<em>fileFilterStr</em>  /M=<em>messageStr</em>  /MULT=<em>m</em>  /P=<em>pathName</em> /R /T=<em>typeStr</em>  /Z[=<em>z</em>] ] <em>refNum</em>  [<em>as</em> <em>fileNameStr</em>] {#open}

</div>

The Open operation can, depending on the flags passed to it:


1.	Open an existing file to read data from (/R flag without /D).


2.	Open a file to append results to (/A flag without /D).


3.	Create a new file or overwrite an existing file to write results to (no /D, /R or /A flags).


4.	Display an Open File dialog (/D/R or /D/A flags with or without /MULT).


5.	Display a Save File dialog (/D flag without /R or /A).

### *Parameters* {#parameters}
*refNum* is the name of a numeric variable to receive the file reference number. *refNum* is set by Open if Open actually opens a file for reading or writing (cases 1, 2 and 3). You use *refNum* with the [FReadLine](/igorpro/commands/freadline.md), [FStatus](/igorpro/commands/fstatus.md), [FGetPos](/igorpro/commands/fgetpos.md), [FSetPos](/igorpro/commands/fsetpos.md), [FBinWrite](/igorpro/commands/fbinwrite.md), [FBinRead](/igorpro/commands/fbinread.md), [fprintf](/igorpro/commands/fprintf.md) and [wfprintf](/igorpro/commands/wfprintf.md) operations to read from or write to the file. When you're finished, pass *refNum* to the [Close](/igorpro/commands/close.md) operation to close the file.

Open does not set the file reference number when the /D flag is used (cases 4 and 5) but you must still supply a *refNum* parameter.

The targeted file is specified by a combination of the *pathName* parameter and the *fileNameStr* parameter. There are three ways to specify the targeted file:

1.	Symbolic path and simple file name:

	Use /P=*pathName* and *fileNameStr*, where *pathName* is the name of an Igor symbolic path (see [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths)) that points to the folder containing the file and *fileNameStr* is the name of the file.

2.	Symbolic path and partial path:

	Use /P=*pathName* and *fileNameStr*, where *pathName* is the name of an Igor symbolic path that points to the folder containing the file and *fileNameStr* is a partial path starting from the folder and leading to the file.

3.	Full path:

	Use just *fileNameStr*, where *fileNameStr* is a full path to the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

The targeted file is *fully specified* if *fileNameStr* is a full path or if both *pathName* and *fileNameStr* are present and not empty strings.

The targeted file is *not fully specified* in any of these cases:

*as fileNameStr* is omitted

*fileNameStr* is an empty string

*fileNameStr* is not a full path and no symbolic path is specified

### *Opening an Existing File For Reading Only* {#opening-an-existing-file-for-reading-only}
This covers cases 1 (/R without /D).

If the file is fully-specified but does not exist, an error is generated. If you want to detect and handle the error yourself, use the /Z flag.

If the file is not fully-specified, Open displays an Open File dialog.

If a file is opened, *refNum* is set to the file reference number.

### *Opening a File For Appending* {#opening-a-file-for-appending}
This covers cases 2 (/A without /D).

If the file is fully-specified and exists, it is opened for read/write and the current file position is moved to the end of the file.

If the file is fully-specified but does not exist, the file is created and opened for read/write.

If the file is not fully-specified, Open displays an Open File dialog.

If a file is opened, *refNum* is set to the file reference number.

### *Opening a File For Write* {#opening-a-file-for-write}
This covers case 3 (no /R, /A or /D).

If the targeted file exists, it is overwritten.

If the targeted file does not exist and it is fully-specified and targets a valid path, a new file is created.

If the file is fully-specified and targets an invalid path, an error is generated. If you want to detect and handle the error yourself, use the /Z flag.

If the file is not fully-specified, Open displays a Save File dialog.

If a file is opened, *refNum* is set to the file reference number.

### *Displaying an Open File Dialog To Select a Single File* {#displaying-an-open-file-dialog-to-select-a-single-file}
This covers cases 4 (/D with /R or /A).

Open does not actually open the file but just displays the Open File dialog.

If the user chooses a file in the Open File dialog, the S_fileName output string variable is set to a full path to the file. You can use this in subsequent commands. If the user cancels, S_fileName is set to "".

See the documentation for the /D, /F and /M flags and then read [Displaying an Open File Dialog](/igorpro/programming/interacting-with-the-user.md#displaying-an-open-file-dialog) for details.

*refNum* is left unchanged.

### *Displaying an Open File Dialog To Select Multiple Files* {#displaying-an-open-file-dialog-to-select-multiple-files}
This covers cases 4 (/D with /R or /A) with the /MULT=1 flag.

Open does not actually open the file but just displays the Open File dialog.

If the user chooses one or more files in the Open File dialog, the S_fileName output string variable is set to a carriage-return-delimited list of full paths to one or more files. You can use this in subsequent commands. If the user cancels, S_fileName is set to "".

See the documentation for the /D, /F, /M and /MULT flags and then read [Displaying a Multi-Selection Open File Dialog](/igorpro/programming/interacting-with-the-user.md#displaying-a-multi-selection-open-file-dialog) for details.

*refNum* is left unchanged.

### *Displaying a Save File Dialog* {#displaying-a-save-file-dialog}
This covers cases 5 (/D without /R or /A).

Open does not actually open the file but just displays the Save File dialog.

If the user chooses a file in the Save File dialog, the S_fileName output string variable is set to a full path to the file. You can use this in subsequent commands. If the user cancels, S_fileName is set to "".

See the documentation for the /D, /F and /M flags and then read [Displaying a Save File Dialog](/igorpro/programming/interacting-with-the-user.md#displaying-a-save-file-dialog) for details.

*refNum* is left unchanged.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Opens an existing file for appending or, if the file does not exist, creates a new file and opens it for appending. |
| <span class="table-cell-nowrap">/C = *creatorStr*</span> | Specifies the file creator code. This is ignored. |
| For opening an existing file, creator defaults to "????" which means "any creator". For creating a new file, *creatorStr* defaults to "IGR0" which is Igor's creator code. |  |
| <span class="table-cell-nowrap">/D[ = *mode* ]</span> | Specifies dialog-only mode. |
|  |<table class="nested-table"><tbody><tr><td>/D:</td><td>A dialog is always displayed.</td></tr><tr><td>/D=1:</td><td>Same as /D.</td></tr><tr><td>/D=2:</td><td>A dialog is displayed only if  *pathName* and *fileNameStr* do not specify a valid file.</td></tr></tbody></table>
|  | Use this mode to allow the user to choose a file to be opened by a subsequent operation, such as [LoadWave](/igorpro/commands/loadwave.md). |
|  | With /D or /D=1, open presents a dialog from which the user can select a file but does not actually open the file. Instead, Open puts the full path to the file into the string variable S_fileName. |
|  | /D=2 does the same thing except that it skips the dialog if  *pathName* and *fileNameStr* specify a valid file. In this case, if *pathName* and *fileNameStr* refer to a shortcut, the target of the shortcut is returned. |
|  | If the user clicks the Cancel button, S_fileName is set to an empty string. |
|  | Use Open/D/R to bring up an Open File dialog. See [Displaying an Open File Dialog](/igorpro/programming/interacting-with-the-user.md#displaying-an-open-file-dialog) for details. |
|  | Use Open/D/R/MULT=1 to bring up an Open File dialog to select multiple files. See [Displaying a Multi-Selection Open File Dialog](/igorpro/programming/interacting-with-the-user.md#displaying-a-multi-selection-open-file-dialog) for details. |
|  | Use Open/D to bring up a Save File dialog. See [Displaying a Save File Dialog](/igorpro/programming/interacting-with-the-user.md#displaying-a-save-file-dialog) for details. |
|  | See [Using Open in a Utility Routine](/igorpro/programming/interacting-with-the-user.md#using-open-in-a-utility-routine) for an example using /D=2. |
| <span class="table-cell-nowrap">/F = *fileFilterStr*</span> | /F provides control over the file filter menu in the Open File dialog. See [Open File Dialog File Filters](/igorpro/programming/interacting-with-the-user.md#open-file-dialog-file-filters) and [Save File Dialog File Filters](/igorpro/programming/interacting-with-the-user.md#save-file-dialog-file-filters) for details. |
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Prompt message text in the dialog used to select the file, if any. |
| <span class="table-cell-nowrap">/MULT = *m*</span> | Use /D/R/MULT=1 to display a multi-selection Open File dialog. |
|  | /D/R/MULT=0 or just /D/R displays a single-selection Open File dialog. |
|  | /MULT=1 is allowed only if /D or /D=1 and /R are specified. |
|  | See [Displaying a Multi-Selection Open File Dialog](/igorpro/programming/interacting-with-the-user.md#displaying-a-multi-selection-open-file-dialog) for details. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/R</span> | The file is opened read only. |
| <span class="table-cell-nowrap">/T = *typeStr*</span> | This file type setting is no longer supported. |
|  | /F should be used instead of /T. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevents aborting of procedure execution if an error occurs, for example if the procedure tries to open a file that does not exist for reading. Use /Z if you want to handle this case in your procedures rather than having execution abort. |
|  | When using /Z, /Z=1, or /Z=2, V_flag is set to 0 if no error occurred or to a nonzero value if an error did occur. |
|  | Do not use /Z with /D. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z.</td></tr><tr><td>/Z=1:</td><td>Suppresses normal error reporting. When used with /R, it opens the file if it exists. /Z alone has the same effect as /Z=1.</td></tr><tr><td>/Z=2:</td><td>Suppresses normal error reporting. When used with /R, it opens the file if it exists or displays a dialog if it does not exist.</td></tr></tbody></table>

### *Details* {#details}
When Open returns, if a file was actually opened, the *refNum* parameter will contain a file reference number that you can pass to other operations to read or write data. If the file was not opened because of an error or because the user canceled or because /D was used, *refNum* will be unchanged.

If you use /R (open for read), Open opens an existing file for reading only.

If you use /A, Open opens an existing file for appending. If the file does not exist, it is created and then opened for appending.

If both /R and /A are omitted then Open creates and opens a file. If the specified file does not already exist, Open creates it and opens it for writing. If the file does already exist then Open opens it and sets the current file position to the start of the file. The current file position determines where in the file data will be written. Thus, you will be overwriting existing data in the file.

:::warning
If you open an existing file for writing (you do not use /R) then you will overwrite or truncate existing data in the file. To avoid this, open for read (use /R) or open for append (use /A).
:::

### *Output Variables* {#output-variables}

|  |  |
| --- | --- |
| The Open operation returns information in the following variables: |  |
| V_flag | Set only when the /Z flag is used. |
|  | V_flag is set to zero if the file was opened, to -1 if Open displayed a dialog (because the file was not fully-specified) and the user cancelled, and to some nonzero value if an error occurred. |
| S_fileName | Stores the full path to the file that was opened. |
|  | If /MULT=1 is used, S_fileName is a carriage-return-separated list of full paths to one or more files. |
|  | If an error occurred or if the user canceled, S_fileName is set to an empty string. |

When using /D, the value of V_flag is undefined. Do not use /Z with /D. Use S_fileName to determine if the user selected a file or canceled.

### *Examples* {#examples}
This example function illustrates using Open to open a text file from which data will be read. The function takes two parameters: an Igor symbolic path name and a file name. If either of these parameters is an empty string, the Open operation will display a dialog allowing the user to choose the file. Otherwise, the Open operation will open the file without displaying a dialog.


```igor
Function DemoOpen(pathName, fileName)
	String pathName	// Name of symbolic path or "" for dialog.
	String fileName	// File name, partial path, full path or "" for dialog.
	Variable refNum
	String str

	// Open file for read.
	Open/R/Z=2/P=$pathName refNum as fileName

	// Store results from Open in a safe place.
	Variable err = V_flag
	String fullPath = S_fileName

	if (err == -1)
		Print "DemoOpen cancelled by user."
		return -1
	endif

	if (err != 0)
		DoAlert 0, "Error in DemoOpen"
		return err
	endif

	Printf "Reading from file \"%s\". First line is:\r", fullPath
	FReadLine refNum, str	// Read first line into string variable
	Print str
	Close refNum
	return 0
End
```

### *See Also* {#see-also}
[Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths)

[Close](/igorpro/commands/close.md), [FBinRead](/igorpro/commands/fbinread.md), [FBinWrite](/igorpro/commands/fbinwrite.md), [FReadLine](/igorpro/commands/freadline.md)

[FGetPos](/igorpro/commands/fgetpos.md), [FSetPos](/igorpro/commands/fsetpos.md), [FStatus](/igorpro/commands/fstatus.md)

[fprintf](/igorpro/commands/fprintf.md), [wfprintf](/igorpro/commands/wfprintf.md)

[Displaying an Open File Dialog](/igorpro/programming/interacting-with-the-user.md#displaying-an-open-file-dialog), [Displaying a Multi-Selection Open File Dialog](/igorpro/programming/interacting-with-the-user.md#displaying-a-multi-selection-open-file-dialog), [Open File Dialog File Filters](/igorpro/programming/interacting-with-the-user.md#open-file-dialog-file-filters)

[Displaying a Save File Dialog](/igorpro/programming/interacting-with-the-user.md#displaying-a-save-file-dialog), [Save File Dialog File Filters](/igorpro/programming/interacting-with-the-user.md#save-file-dialog-file-filters)

[Using Open in a Utility Routine](/igorpro/programming/interacting-with-the-user.md#using-open-in-a-utility-routine)

[Open Load File Demo](#igor-pxp/Examples/Programming/Load__File__Demo.pxp)