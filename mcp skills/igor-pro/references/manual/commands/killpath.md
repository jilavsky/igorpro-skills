---
description: "The KillPath operation removes a path from the list of symbolic paths. KillPath is a newer name for the RemovePath operation."
slug: /commands/killpath
---

<div className="command-signature">

## <strong>KillPath</strong>  [/A/Z] <em>pathName</em> {#killpath}

</div>

The KillPath operation removes a path from the list of symbolic paths. KillPath is a newer name for the RemovePath operation.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Kills all symbolic paths in the experiment except for the built-in paths. Omit *pathName* if you use /A. |
| <span class="table-cell-nowrap">/Z</span> | Doesn't generate an error if a path to be killed is a built-in path or does not exist or is in use. To kill all paths in the experiment, use KillPath/A/Z. |

### *Details* {#details}
You can't kill the built-in paths "home" and "Igor".

A symbolic path is "in use" if the current experiment contains shared waves or notebooks loaded from the associated disk folder.

Prior to Igor Pro 9.00, the KillPath operation prevented killing a symbolic path used to a load shared wave if the shared wave file was in the current data folder. It now prevents killing a symbolic path used to load a shared wave in any data folder. Use the /Z flag to suppress error reporting if this change creates problems for you.

### *See Also* {#see-also}
[Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths), [NewPath](/igorpro/commands/newpath.md)