---
description: "The ParseFilePath function provides the ability to manipulate file paths and to extract sections of file paths."
slug: /commands/parsefilepath
---

<div className="command-signature">

## <strong>ParseFilePath</strong> (<em>mode</em>, <em>pathInStr</em>, <em>separatorStr</em>, <em>whichEnd</em>, <em>whichElement</em>) {#parsefilepath}

</div>

The ParseFilePath function provides the ability to manipulate file paths and to extract sections of file paths.

### *Parameters* {#parameters}
The meaning of the parameters depends on *mode*.

| mode | Information Returned |
| --- | --- |
| 0 | Returns the element specified by *whichEnd* and *whichElement*. |
|  | *whichEnd* is 0 to select an element relative to the beginning of *pathInStr*, 1 to select an element relative to the end. *whichElement* is zero-based. |
|  | Pass ":" if *pathInStr* is a Macintosh HFS path, "\\\\" if it is a Windows path. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details about Macintosh versus Windows paths. |
| 1 | Returns the entire *pathInStr*, up to but not including the element specified by *whichEnd* and *whichElement*. |
|  | *whichEnd* is 0 to select an element relative to the beginning of *pathInStr*, 1 to select an element relative to the end. *whichElement* is zero-based. |
|  | Pass ":" if *pathInStr* is a Macintosh HFS path, "\\\\" if it is a Windows path. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details about Macintosh versus Windows paths. |
| 2 | Returns the entire *pathInStr* with a trailing separator added if it is not already there. This is useful when you have a path to a folder and want to tack on a file name. |
|  | Pass ":" if *pathInStr* is a Macintosh HFS path, "\\\\" if it is a Windows path. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details about Macintosh versus Windows paths. |
|  | *whichEnd* and *whichElement* are ignored. Pass 0 for them. |
| 3 | Returns the last element of *pathInStr* with the extension, if any, removed. The extension is anything after the last dot in *pathInStr*. |
|  | *whichEnd* and *whichElement* are ignored. Pass 0 for them. |
| 4 | Returns the extension in *pathInStr* or "" if there is no extension. The extension is anything after the last dot in *pathInStr*. |
|  | Pass ":" if pathInStr is a Macintosh HFS path, "\\\\" if it is a Windows path. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details about Macintosh versus Windows paths. |
|  | *whichEnd* and *whichElement* are ignored. Pass 0 for them. |
| 5 | Returns the entire *pathInStr*, but converts it to a format determined by *separatorStr*. |
|  |<table class="nested-table"><tbody><tr><td>*separatorStr*&nbsp;=&nbsp;&quot;:&quot;</td><td>Converts the path to Macintosh HFS style if it is Windows style. Does nothing if it is already a Macintosh HFS path.</td></tr><tr><td>*separatorStr*&nbsp;=&nbsp;&quot;\\\\&quot;</td><td>Converts the path to Windows style if it is Macintosh style. Does nothing if it is already a Windows path.</td></tr><tr><td>*separatorStr*&nbsp;=&nbsp;&quot;\*&quot;</td><td>Converts the path to the native style of the operating system Igor is running on. Does nothing if it is already a native path.</td></tr><tr><td></td><td>For historical reasons, on Macintosh &quot;native&quot; means colon-separated HFS path, not UNIX path.</td></tr><tr><td>*separatorStr*&nbsp;=&nbsp;&quot;/&quot;</td><td>This mode is no longer supported..</td></tr><tr><td></td><td>This always returns &quot;&quot; on Windows.</td></tr></tbody></table>
|  | *whichEnd* and *whichElement* are ignored. Pass 0 for them. |
| 6 | Returns the UNC volume name ("\\\\Server\\Share") if *pathInStr* starts with a UNC volume name or "" if not. Pass "\*" for *separatorStr*. |
|  | *whichEnd* and *whichElement* are ignored. Pass 0 for them. |
| 7 | Returns the UNC server name ("Server" from "\\\\Server\\Share") if *pathInStr* starts with a UNC volume name or "" if not. Pass "\*" for *separatorStr*. |
|  | *whichEnd* and *whichElement* are ignored. Pass 0 for them. |
| 8 | Returns the UNC share name ("Share" from "\\\\Server\\Share") if *pathInStr* starts with a UNC volume name or "" if not. Pass "\*" for *separatorStr*. |
|  | *whichEnd* and *whichElement* are ignored. Pass 0 for them. |
| 9 | This mode is no longer supported and returns an error. |
|  | This mode was created in Igor Pro 7.00. |
| 10 | This mode is no longer supported and returns an error. |
|  | This mode was created in Igor Pro 7.00. |

### *Details* {#details}
When dealing with Windows paths, you need to be aware that Igor treats the backslash character as an escape character. When you want to put a backslash in a literal string, you need to use two backslashes. See [Escape Sequences in Strings](/igorpro/programming/commands.md#escape-sequences-in-strings) and [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details.

On Windows two types of file paths are used: drive-letter paths and UNC ("Universal Naming Convention") paths. For example:


```igor
// This is a drive-letter path.
C:\Program Files\WaveMetrics\Igor Pro Folder\WaveMetrics Procedures

// This is a UNC path.
\\BigServer\SharedApps\Igor Pro Folder\WaveMetrics Procedures
```

In this example, ParseFilePath considers the volume name to be C: in the first case and \\\\BigServer\\SharedApps in the second. The volume name is treated as one element by ParseFilePath, except for modes 7 and 8 which permit you to extract the components of the UNC volume name.

Except for the leading backslashes in UNC path, ParseFilePath modes 0 and 1 internally strip any leading or trailing separator (as defined by the *separatorStr* parameter) from *pathInStr* before it starts parsing. So if you pass ":Igor Pro Folder:WaveMetrics Procedures:", it is the same as if you had passed "Igor Pro Folder:WaveMetrics Procedures".

If there is no element corresponding to *whichElement* and *mode* is 0, ParseFilePath returns "".

If there is no element corresponding to *whichElement* and *mode* is 1, ParseFilePath returns the entire *pathInStr*.

### *Examples* {#examples}

```igor
// Macintosh path convention (colon separators)
PathInfo Igor // Get full path to installed Igor Pro Folder, in Mac format
String macPath = S_Path
Print macPath	// prints "C:Program Files:WaveMetrics:Igor Pro 10 Folder:"

// Extract first element.
Print ParseFilePath(0, macPath, ":", 0, 0)	// Prints "C"

// Demonstrate how ParseFilePath ensures path ends with path separator
macPath = RemoveEnding(macPath,":") // removes ending separator

// Make sure the given path ends with a separator and concatenate file name.
macPath = ParseFilePath(2, macPath, ":", 0, 0)
macPath += "AFile.txt"
Print macPath // prints "C:Program Files:WaveMetrics:Igor Pro 10 Folder:AFile.txt"

// convert Mac to Windows path convention (backslashes separators)
String winPath = ParseFilePath(5, macPath, "\\", 0, 0)
Print winPath // Prints "C:\Program Files\WaveMetrics\Igor Pro 10 Folder\AFile.txt"

// Extract first element.
Print ParseFilePath(0, winPath, "\\", 0, 0)	// Prints "C:"

// Extract third element.
Print ParseFilePath(0, winPath, "\\", 0, 2)	// Prints "WaveMetrics"

// Extract last element.
Print ParseFilePath(0, winPath, "\\", 1, 0)	// Prints "AFile.txt"

// Extract next to last element.
Print ParseFilePath(0, winPath, "\\", 1, 1)	// Prints "Igor Pro 10 Folder"

// Extract the file name without extension.
Print ParseFilePath(3, winPath, "\\", 0, 0)	// Prints "AFile"

// Extract the extension.
Print ParseFilePath(4, winPath, "\\", 0, 0)	// Prints "txt"
```

### *See Also* {#see-also}
[RemoveEnding](/igorpro/commands/removeending.md), [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators)