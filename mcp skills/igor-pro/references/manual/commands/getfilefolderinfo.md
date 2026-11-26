---
description: "The GetFileFolderInfo operation returns and optionally prints information about a file or folder."
slug: /commands/getfilefolderinfo
---

<div className="command-signature">

## <strong>GetFileFolderInfo</strong>  [/CSET=<em>charset</em> /D /LANG=<em>lang</em> /P=<em>pathName</em> /Q /UTC[=<em>u</em>] /Z[=<em>z</em>]] [<em>fileOrFolderNameStr</em>] {#getfilefolderinfo}

</div>

The GetFileFolderInfo operation returns and optionally prints information about a file or folder.

### *Parameters* {#parameters}
*fileOrFolderNameStr* specifies the file (or folder) for which information is returned. It is optional if /P=*pathName* and /D are specified, in which case information about the directory associated with *pathName* is returned.

If you use a full or partial path for *fileOrFolderNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

Folder paths should not end with single [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators). See [MoveFolder](/igorpro/commands/movefolder.md)'s Details section.

If Igor cannot determine the location of the file from *fileOrFolderNameStr* and *pathName*, it displays a dialog allowing you to specify the file to be examined. Use /D to select a folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CSET = *charset*</span> | Specifies which file version information to return. *charset* = 0 means any character set, 1200 (0x4b0) means Unicode, 1252 means Windows-1252 ANSII encoding, and 932 (0x03a4) means Japanese Shift_JIS encoding. |
| <span class="table-cell-nowrap">/D</span> | When *pathName* and *fileOrFolderNameStr* do not specify an existing file or folder, use the Select Folder dialog rather than Open File dialog. |
| <span class="table-cell-nowrap">/LANG = *lang*</span> | Specifies which file version information to return. *language* = 0 means any language,1033 (0x406) means U.S. English, and 1041 (0x411) means  Japanese. |
| <span class="table-cell-nowrap">/OMIT[ = *bitMask* ]</span> | Omit specified checks and results to improve speed, mostly when retrieving information about files. |
|  | *bitMask* is a bitwise parameter that specifies which checks or results to omit. See the table under ***/OMIT Bitmask Settings*** for a description of the different bit values. For more information bit settings, see [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters). |
|  | Without =*bitMask,* the effective *bitMask* = 0xF (15); these speedups don't change the way shortcut files are treated (they're still resolved to the file or folder it points to, returning information about what is pointed to). |
|  | /OMIT was added for Igor 10. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for the file. *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/Q</span> | Don't print information to the history area. |
| <span class="table-cell-nowrap">/UTC[ = *u* ]</span> | If you include /UTC or /UTC=1, GetFileFolderInfo returns creation and modification dates in UTC (coordinated universal time). If you omit /UTC or specify /UTC=0, GetFileFolderInfo returns creation and modification dates in local time. |
|  | The default, used if you omit /UTC, is local time. |
|  | The /UTC flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevents procedure execution from aborting if GetFileFolderInfo tries to get information about a file or folder that does not exist. Use /Z if you want to handle this case in your procedures rather than having execution abort. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z at all.</td></tr><tr><td>/Z=1:</td><td>Used for getting information for a file or folder only if it exists. /Z alone has the same effect as /Z=1.</td></tr><tr><td>/Z=2:</td><td>Used for getting information for a file or folder if it exists and displaying a dialog if it does not exist.</td></tr></tbody></table>

### */OMIT Bitmask Settings* {#omit-bitmask-settings}

The following values are accepted by the /OMIT flag, and omit the following information:

| Bit # | *bitMask* Value | Omits |
| --- | --- | --- |
| 0 | 0x1 | S_creator |
| 1 | 0x2 | V_version, S_fileVersion |
| 2 | 0x4 | S_languageAndCharsetList, S_versionInfo |
| 3 | 0x8 | does not retrieve the actual case of the file name |
| 4 | 0x10 | does not resolve (follow) shortcut files |
| All | other bits are reserved and must be set to zero. |  |

### *Output Variables* {#output-variables}
GetFileFolderInfo returns information in the following output variables:

|  |  |
| --- | --- |
| V_Flag |<table class="nested-table"><tbody><tr><td>0:</td><td>File or folder was found.</td></tr><tr><td>-1:</td><td>User cancelled the Open File dialog.</td></tr><tr><td>Other:</td><td>An error occurred, such as the specified file or folder does not exist.</td></tr></tbody></table>
| S_Path | Full file system path to the specified file or folder using Macintosh path syntax. |
| V_isFile |<table class="nested-table"><tbody><tr><td>1:</td><td>*fileOrFolderNameStr* is a file.</td></tr></tbody></table>
| V_isFolder |<table class="nested-table"><tbody><tr><td>1:</td><td>*fileOrFolderNameStr* is a folder.</td></tr></tbody></table>
| V_isInvisible |<table class="nested-table"><tbody><tr><td>1:</td><td>file is hidden.</td></tr></tbody></table>
| V_isReadOnly | Set if the file is read-only. |
|  | V_isReadOnly is either 0 (writtable) or 1 (read-only). To set this manually, display the Properties window for the file and then check or uncheck the "read-only" checkbox. |
|  | V_isReadOnly tells you only about the property set in the Windows desktop. It does not tell you if you have write permission for the file or for the folder containing the file. If your goal is to determine if you can write to the file, the only way to do that is to try to write to it and catch any resulting error. |
| V_creationDate | Number of seconds since midnight on January 1, 1904 when the file or folder was first created in local time or UTC depending on the /UTC flag. Use [Secs2Date](/igorpro/commands/secs2date.md) to format the date as text. |
| V_modificationDate | Number of seconds since midnight on January 1, 1904 when the file or folder was last modified in local time or UTC depending on the /UTC flag. Use [Secs2Date](/igorpro/commands/secs2date.md) to format the date as text. |
| V_isAliasShortcut |<table class="nested-table"><tbody><tr><td>1:</td><td>File is a shortcut and S_aliasPath is also set.</td></tr></tbody></table>

If *fileOrFolderNameStr* does actually refer to a file (not a folder), GetFileFolderInfo returns additional information in the following variables:

|  |  |
| --- | --- |
| S_aliasPath | If the specified file is a shortcut, S_aliasPath is the full path to the target of the specified file. Otherwise it is "". |
|  | S_aliasPath uses Macintosh path syntax. When the source is a folder, it ends with a ":" character. |
| V_isStationery |<table class="nested-table"><tbody><tr><td>1:</td><td>The stationery bit is set and the file type is one of the stationery file types (.pxt, .uxt, .ift).</td></tr></tbody></table>
| S_fileType | The four-character file type code, such as 'TEXT' or 'IGsU' (packed experiment). These codes are fabricated by translating from the equivalent file name extensions, such as .txt and .pxp. |
| S_creator | The four-character creator code, such as 'IGR0' (Igor Pro creator code). |
|  | S_creator is set to 'IGR0' if the file name extensions is one of those registered to Igor Pro, such as .pxp or .bwav (but not .txt). For other registered extensions, S_creator is set to the full file path of the registered application. Otherwise it is set to "". |
| V_logEOF | The number of bytes in the file data fork. For other forks, use [Open](/igorpro/commands/open.md)/F and [FStatus](/igorpro/commands/fstatus.md). |
| V_version | Version number of the file. A file version such as 3.10.2.1 is returned as 4.021: use S_fileVersion to avoid the problem of the second digit overflowing into the first digit. |
|  |<table class="nested-table"><tbody><tr><td>&quot;0&quot;:</td><td>File version can&#39;t be determined, or the file can&#39;t be examined because it is already open.</td></tr></tbody></table>
| S_fileVersion | The file version as a string. |
|  | A file version such as 3.10.2.1 is returned as "3.10.2.1". |
|  |<table class="nested-table"><tbody><tr><td>&quot;0.0.0.0&quot;:</td><td>File version can&#39;t be determined.</td></tr></tbody></table>
| S_languageAndCharsetList |  |
|  | A string list of combined language and charset hexadecimal values created from the file's resource `VS_VERSIONINFO` structure's VarFileInfo list "version info" translations. |
|  | Each number in the list is a combination of the language code and charset that serves as a selector for which `VERSIONINFO` to return in S_versionInfo. Each number encodes the language into the most significant 16 bits and the character set ("charset") into the least signficant 16 bits. |
|  | For example, the language code for U.S. English is 1033 (0x0409) and the Unicode charset is 1200 (0x04b0). If that were the only translation provided for the version information, S_languageAndCharsetList would be "040904b0;". |
| S_versionInfo | A sorted keyword-value string list of all the keys and values in the file's `VERSIONINFO` string data. |
|  | This is the information displayed in the Windows Explorer's Properties dialog's Details or Version tab. Usually only executable files (*.exe, *.dll) contain `VERSIONINFO` resources. |
|  | Some files have more than one language/charset translation for version information. A particular translation can be retrieved into S_versionInfo by specifying /LANG and/or /CSET. |
|  | The version keys and values for the first translation in the file's version information is returned when /LANG and /CSET are not specified, or when no match for /LANG and/or /CSET is found and there is only one translation. |
|  | Two additional key/value pairs "Language:*languageNum*;" and "Charset:*charsetNum*;" are included in S_versionInfo. These describe which translation's file version information was returned in S_versionInfo. The "Language" and "Charset" values might not match the requested language and charset or S_languageAncCharsetList if the file's version resource was not properly constructed. |
|  | See [Using Keyword-Value Packed Strings](/igorpro/programming/programming-techniques.md#using-keyword-value-packed-strings) and the [ListToTextWave](/igorpro/commands/listtotextwave.md) function. |

### *Details* {#details}
You can change some of the file information by using [SetFileFolderInfo](/igorpro/commands/setfilefolderinfo.md).

Shortcuts have ".lnk" file name extensions that are hidden on the desktop. Prior to Igor Pro 9, *fileOrFolderNameStr* was required to include the ".lnk" extension. For consistency with operations such as NewPath and OpenNotebook, in Igor Pro 9.00 and later, it is optional. When *fileOrFolderNameStr* refers to a shortcut, the S_path output variable includes the ".lnk" extension.

### *Examples* {#examples}

```igor
// Setup: create symbolic path name for path to my Documents folder
NewPath/O/Q Documents, SpecialDirPath("Documents", 0, 1, 0) // 1=Windows style path

// Print the modification date of a file in my Documents folder
GetFileFolderInfo/P=Documents/Z "Experiment.pxp" // an Igor experiment file in Documents folder
if (V_Flag == 0 && V_isFile) 	// file exists
	Print Secs2Date(V_modificationDate,0), Secs2Time(V_modificationDate,0)
endif

// Determine if a folder exists
//    Note double backslash separators in the Windows-style path.
//    See the "Path Separators" help topic.
GetFileFolderInfo/Z "C:\\Users\\jim\\Documents\\Subfolder"
if (V_Flag == 0 && V_isFolder)
	Print "Folder Exists!"
endif

// Find out where a shortcut points to
GetFileFolderInfo/P=Documents/Z "Another Experiment.pxp - Shortcut"
if (V_Flag == 0 && V_isAliasShortcut)
	Print S_aliasPath // "C:Users:jim:Documents:Subfolder:Another Experiment.pxp"
	String winPath = ParseFilePath(5, S_aliasPath, "\\", 0, 0) // Windows-style path
	Print winPath // "C:\Users\jim\Documents\Subfolder\Another Experiment.pxp"
endif

// List Igor's own VS_VERSIONINFO file version available translations and version details
GetFileFolderInfo/Q SpecialDirPath("Igor Executable", 0, 0, 0) + "Igor64.exe"
if (V_Flag == 0)
    Print S_languageAndCharsetList	// "040904b0;041104b0;"
    Print S_versionInfo // "Charset:1200;CompanyName:WaveMetrics;FileDescription:Igor Pro;
                        // FileVersion:10.0.1.29291;InternalName:Igor;Language:1033;
                        // LegalCopyright:Copyright (c) 1988-2025, WaveMetrics;
                        // ProductName:Igor Pro;ProductVersion:10.0.1.29291;"
endif
```

### *See Also* {#see-also}
[SetFileFolderInfo](/igorpro/commands/setfilefolderinfo.md), [PathInfo](/igorpro/commands/pathinfo.md), [FStatus](/igorpro/commands/fstatus.md), [IndexedFile](/igorpro/commands/indexedfile.md), [Secs2Date](/igorpro/commands/secs2date.md), [ParseFilePath](/igorpro/commands/parsefilepath.md), [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators),

[https://docs.microsoft.com/en-us/windows/win32/menurc/versioninfo-resource](https://docs.microsoft.com/en-us/windows/win32/menurc/versioninfo-resource)