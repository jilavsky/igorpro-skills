---
description: "The DuplicateDataFolder operation makes a copy of the source data folder and everything in it and places the copy at the specified location with the specified…"
slug: /commands/duplicatedatafolder
---

<div className="command-signature">

## <strong>DuplicateDataFolder</strong>  [ /O=<em>options</em> /Z ] <em>sourceDataFolderSpec</em>, <em>destDataFolderSpec</em> {#duplicatedatafolder}

</div>

The DuplicateDataFolder operation makes a copy of the source data folder and everything in it and places the copy at the specified location with the specified name.

### *Parameters* {#parameters}
*sourceDataFolderSpec* can be just the name of a child data folder in the current data folder, a partial path (relative to the current data folder) and name or an absolute path (starting from root) and name, or a data folder reference (DFREF) in a user-defined function.

*destDataFolderSpec* can be just a data folder name, a partial path (relative to the current data folder) and name or an absolute path (starting from root) and name. If just a data folder name is used then the new data folder is created in the current data folder, or a data folder reference (DFREF) in a user-defined function.

Depending on the syntax you use, DuplicateDataFolder may overwrite the data folder specified by *destDataFolderSpec* or it may copy the source data folder into the data folder specified by *destDataFolderSpec*. See **DuplicateDataFolder Destination** below for details.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/O = *options*</span> | Overwrites the destination data folder if it already exists. |
|  | The /O flag was added in Igor Pro 8.00. |
|  |<table class="nested-table"><tbody><tr><td>*options*&nbsp;=0:</td><td>Attempting to overwrite a data folder generates an error, as if you omitted /O.</td></tr><tr><td>*options*&nbsp;=1:</td><td>Completely overwrites the destination data folder. If the destination data folder exists, DuplicateDataFolder first deletes it if possible. If it cannot be deleted, for example because it contains a wave that is in use, DuplicateDataFolder generates an error. If the deletion succeeds, DuplicateDataFolder then copies the source to the destination.</td></tr><tr><td>*options*&nbsp;=2:</td><td>Merges the source data folder into the destination data folder. If an item in the source data folder exists in the destination data folder, DuplicateDataFolder overwrites it. Otherwise it copies it. Items in the destination data folder that do not exist in the source data folder remain in the destination data folder.</td></tr><tr><td>*options*&nbsp;=3:</td><td>Merges the source data folder into the destination data folder and then deletes items that are not in the source data folder if possible. If an item in the source data folder does not exist in the destination data folder, DuplicateDataFolder attempts to delete it from the destination data folder. If it cannot be deleted because it is in use, no error is generated.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Errors are not fatal - if an error occurs, procedure execution continues. You can check the V_flag output variable to see if an error occurred. |

### *Details* {#details}
An error is issued if the destination is contained within the source data folder.

A common use for a data folder reference variable is to create a copy of a data folder inside a free data folder:


```igor
DFREF dest = NewFreeDataFolder()
DuplicateDataFolder source, dest	// Copy of source in a free data folder
```

### *DuplicateDataFolder Destination* {#duplicatedatafolder-destination}
Depending on the syntax you use, DuplicateDataFolder may overwrite the data folder specified by *destDataFolderSpec* or it may copy the source data folder into the data folder specified by *destDataFolderSpec*. To explain this, we will assume that you have executed these commands:


```igor
KillDataFolder/Z root:
NewDataFolder/O root:DataFolderA
NewDataFolder/O root:DataFolderA:SubDataFolderA
NewDataFolder/O root:DataFolderB
```

This gives you a data hierarchy like this:


```igor
root
	DataFolderA
		SubDataFolderA
	DataFolderB
```

The following commands illustrate what DuplicateDataFolder does for a given syntax starting with that data hierarchy.


```igor
// 1. Literal dest without trailing colon: Overwrites DataFolderB with copy of DataFolderA named DataFolderB
DuplicateDataFolder/O=1 root:DataFolderA, root:DataFolderB
// 2. Literal dest with trailing colon: Copies DataFolderA into DataFolderB
DuplicateDataFolder/O=1 root:DataFolderA, root:DataFolderB:
// 3. Literal dest with explicit dest child name: Copies DataFolderA into DataFolderB with name Child
DuplicateDataFolder/O=1 root:DataFolderA, root:DataFolderB:Child
// 4. DFREF dest without trailing colon: Copies DataFolderA into DataFolderB
DFREF dest = root:DataFolderB
DuplicateDataFolder/O=1 root:DataFolderA, dest
// 5. DFREF dest with trailing colon: Generates error
DFREF dest = root:DataFolderB
DuplicateDataFolder/O=1 root:DataFolderA, dest:	// Error - trailing colon not allowed
// 6. DFREF dest with explicit dest child name: Copies DataFolderA into DataFolderB with name Child
DFREF dest = root:DataFolderB
DuplicateDataFolder/O=1 root:DataFolderA, dest:Child
```

### *Output Variables* {#output-variables}
DuplicateDataFolder sets the following output variable:


|  |  |
| --- | --- |
| V_flag | 0 if the operation succeeded, -1 if the destination data folder already existed, or a non-zero error code. The V_Flag output variable was added in Igor Pro 8.00. |

### *Examples* {#examples}

```igor
DuplicateDataFolder root:DF0,root:DF0Copy // Create a copy of DF0 named DF0Copy
```

### *See Also* {#see-also}
[MoveDataFolder](/igorpro/commands/movedatafolder.md), [Data Folders](/igorpro/igor-basics/data-folders.md), [Data Folder References](/igorpro/programming/programming.md#data-folder-references), [Free Data Folders](/igorpro/programming/programming.md#free-data-folders)