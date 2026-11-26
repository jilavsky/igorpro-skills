---
description: "The MoveDataFolder operation removes the source data folder (and everything it contains) and places it at the specified location with the original name."
slug: /commands/movedatafolder
---

<div className="command-signature">

## <strong>MoveDataFolder</strong>  [ /O=<em>options</em> /Z ] <em>sourceDataFolderSpec</em>, <em>destDataFolderPath</em> {#movedatafolder}

</div>

The MoveDataFolder operation removes the source data folder (and everything it contains) and places it at the specified location with the original name.

### *Parameters* {#parameters}
*sourceDataFolderSpec* can be just the name of a child data folder in the current data folder, a partial path (relative to the current data folder) and name or an absolute path (starting from root) and name.

*destDataFolderPath* can be a partial path (relative to the current data folder) or an absolute path (starting from root).

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/O = *options*</span> | Overwrites the destination data folder if it already exists. |
|  | The /O flag was added in Igor Pro 8.00. |
|  |<table class="nested-table"><tbody><tr><td>*options*&nbsp;=1:</td><td>Completely overwrites the destination data folder. If the destination data folder exists, MoveDataFolder first deletes it if possible. If it cannot be deleted, for example because it contains a wave that is in use, MoveDataFolder generates an error. If the deletion succeeds, MoveDataFolder then copies the source to the destination. Then the source data folder is deleted.</td></tr><tr><td>*options*&nbsp;=2:</td><td>Merges the source data folder into the destination data folder. If an item in the source data folder exists in the destination data folder, MoveDataFolder overwrites it. Otherwise it copies it. Items in the destination data folder that do not exist in the source data folder remain in the destination data folder. Then the source data folder is deleted.</td></tr><tr><td>*options*&nbsp;=3:</td><td>Merges the source data folder into the destination data folder and then deletes items that are not in the source data folder if possible. If an item in the source data folder does not exist in the destination data folder, MoveDataFolder attempts to delete it from the destination data folder. If it cannot be deleted because it is in use, no error is generated. Then the source data folder is deleted.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Errors are not fatal - if an error occurs, procedure execution continues. You can check the V_flag output variable to see if an error occurred. |

### *Details* {#details}
MoveDataFolder generates an error if a data folder of the same name already exists at the destination unless the /O flag is used. When the /O flag is non-zero and the destination data folder already exists, MoveDataFolder is equivalent to DuplicateDataFolder followed by a KillDataFolder on the source.

### *Output Variables* {#output-variables}
MoveDataFolder sets the following output variable:


|  |  |
| --- | --- |
| V_Flag | 0 if the operation succeeded or a non-zero error code. The V_Flag output variable was added in Igor Pro 8.00. |

### *Examples* {#examples}

```igor
MoveDataFolder root:DF0, root:archive	// Move DF0 into archive
```

### *See Also* {#see-also}
[DuplicateDataFolder](/igorpro/commands/duplicatedatafolder.md), [Data Folders](/igorpro/igor-basics/data-folders.md)