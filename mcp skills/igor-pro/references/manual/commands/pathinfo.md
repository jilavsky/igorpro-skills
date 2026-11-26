---
description: "The PathInfo operation stores information about the named symbolic path in the following variables."
slug: /commands/pathinfo
---

<div className="command-signature">

## <strong>PathInfo</strong>  [/S  /SHOW ] <em>pathName</em> {#pathinfo}

</div>

The PathInfo operation stores information about the named symbolic path in the following variables:


|  |  |
| --- | --- |
| V_flag | 0 if the symbolic path does not exist, 1 if it does exist. |
| S_path | Full path using Macintosh path conventions (e.g., "hd:This:That:"). |

The path returned is a colon-separated path. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/S</span> | Presets the next otherwise undirected open or save file dialog to the given disk folder. This flag is ignored when PathInfo is called from a preemptive thread. |
| <span class="table-cell-nowrap">/SHOW</span> | Shows the folder, if it exists, in Windows Explorer. This flag is ignored when PathInfo is called from a preemptive thread. |

### *Details* {#details}
The use of PathInfo in a preemptive thread requires Igor Pro 8.00 or later.

### *Examples* {#examples}

```igor
// The following lines perform equivalent actions:
PathInfo/S myPath;Open refNum
Open/P=myPath refNum
// Show Igor's Preferences folder in the Finder/Windows Explorer.
String fullpath= SpecialDirPath("Preferences",0,0,0)
NewPath/O/Q tempPathName, fullpath
PathInfo/SHOW tempPathName
```

### *See Also* {#see-also}
[Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths)

[NewPath](/igorpro/commands/newpath.md), [GetFileFolderInfo](/igorpro/commands/getfilefolderinfo.md), [ParseFilePath](/igorpro/commands/parsefilepath.md), [SpecialDirPath](/igorpro/commands/specialdirpath.md)