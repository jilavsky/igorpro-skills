---
description: "The VariableList function returns a string containing a list of the names of global variables selected based on the matchStr and variableTypeCode parameters."
slug: /commands/variablelist
---

<div className="command-signature">

## <strong>VariableList</strong> (<em>matchStr</em>, <em>separatorStr</em>, <em>variableTypeCode</em> [, <em>dfr</em>]) {#variablelist}

</div>

The VariableList function returns a string containing a list of the names of global variables selected based on the *matchStr* and *variableTypeCode* parameters. The variables listed are all in the current data folder or the data folder specified by *dfr*.

### *Details* {#details}
For a variable name to appear in the output string, it must match *matchStr* and also must fit the requirements of *variableTypeCode*. *separatorStr* is appended to each variable name as the output string is generated.

The name of each variable is compared to *matchStr*, which is some combination of normal characters and the asterisk wildcard character that matches anything. For example:


|  |  |
| --- | --- |
| "\*" | Matches all variable names |
| "xyz" | Matches variable name xyz only |
| "\*xyz" | Matches variable names which end with xyz |
| "xyz\*" | Matches variable names which begin with xyz |
| "\*xyz\*" | Matches variable names which contain xyz |
| "abc\*xyz" | Matches variable names which begin with abc and end with xyz |
| *matchStr* may begin with the "!" character to return items that do not match the rest of *matchStr*. For example: |  |
| "!\*xyz" | Matches variable names which do not end with xyz. |

The "!" character is considered to be a normal character if it appears anywhere else, but there is no practical use for it except as the first character of *matchStr*.

*variableTypeCode* is used to further qualify the variable. The variable name goes into the output string only if it passes the match test and its type is compatible with *variableTypeCode*. *variableTypeCode* is one of:

|  |  |
| --- | --- |
| 2: | System variables (K0, K1 . . .) |
| 4: | Scalar variables |
| 5: | Complex variables |

*dfr* is an optional data folder reference: a data folder name, an absolute or relative data folder path, or a reference returned by, for example, [GetDataFolderDFR](/igorpro/commands/getdatafolderdfr.md). The *dfr* parameter requires Igor Pro 9.00 or later.

### *Examples* {#examples}

```igor
// Returns a list of all scalar variables.
VariableList("*",";",4)

// Returns a list of all complex variables except those whose names begin with "V_".
VariableList("!V_*", ";",5)

// Returns a list of all scalar variables in the root:MyData data folder.
VariableList("*",";",4,root:MyData)
```

### *See Also* {#see-also}
[StringList](/igorpro/commands/stringlist.md), [StringFromList](/igorpro/commands/stringfromlist.md), [WaveList](/igorpro/commands/wavelist.md), [DataFolderList](/igorpro/commands/datafolderlist.md)

[Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters)