---
description: "The KillDataFolder operation kills the specified data folder and everything in it including other data folders."
slug: /commands/killdatafolder
---

<div className="command-signature">

## <strong>KillDataFolder</strong>  [/Z] <em>dataFolderSpec</em> {#killdatafolder}

</div>

The KillDataFolder operation kills the specified data folder and everything in it including other data folders.

However, if *dataFolderSpec* is the name of a data folder reference variable that refers to a free data folder, the variable is cleared and the data folder is killed only if this is the last reference to that free data folder.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting (except for setting V_flag) and does not halt function execution. |

### *Parameters* {#parameters}
*dataFolderSpec* can be just the name of a child data folder in the current data folder, a partial path (relative to the current data folder) and name or an absolute path (starting from root) and name.

### *Details* {#details}
If specified data folder is the current data folder or contains the current data folder then Igor makes its parent the new current data folder.

For legacy reasons, a null data folder is taken to be the current data folder. This can happen when using a $ expression where the string might possibly evaluate to "".

It is legal to kill the root data folder. In this case the root data folder itself is not killed but everything in it is killed.

KillDataFolder generates an error if any of the waves involved are in use. In this case, nothing is killed. Execution ceases unless /Z is specified.

The variable V_flag is set to 0 when there is no error, otherwise it is an error code.

### *Examples* {#examples}

```igor
KillDataFolder foo 	// Kills  foo in the current data folder.
KillDataFolder :bar:foo 	// Kills  foo in bar in the current data folder.
String str= "root:foo"
KillDataFolder $str 	// Kills foo in the root data folder.
```

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [KillStrings](/igorpro/commands/killstrings.md), [KillVariables](/igorpro/commands/killvariables.md), [KillWaves](/igorpro/commands/killwaves.md)