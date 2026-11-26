---
description: "The StringList function returns a string containing a list of global string variables selected based on the matchStr parameter."
slug: /commands/stringlist
---

<div className="command-signature">

## <strong>StringList</strong> (<em>matchStr</em>, <em>separatorStr</em> [, <em>dfr</em>]) {#stringlist}

</div>

The StringList function returns a string containing a list of global string variables selected based on the *matchStr* parameter. The string variables listed are all in the current data folder or the data folder specified by *dfr*.

### *Details* {#details}
For a string variable name to appear in the output string, it must match *matchStr*. *separatorStr* is appended to each string variable name as the output string is generated.

The name of each string variable is compared to *matchStr*, which is some combination of normal characters and the asterisk wildcard character that matches anything. For example:


|  |  |
| --- | --- |
| "*" | Matches all string variable names |
| "xyz" | Matches name xyz only |
| "\*xyz" | Matches names which end with xyz |
| "xyz\*" | Matches names which begin with xyz |
| "\*xyz\*" | Matches names which contain xyz |
| "abc\*xyz" | Matches names which begin with abc and end with xyz |
| The returned list contains names only, without data folder paths. Thus, they are not suitable for accessing string variables outside the current or specified data folder. |  |
| *matchStr* may begin with the "!" character to return items that do not match the rest of *matchStr*. For example: |  |
| "!\*xyz" | Matches variable names which ***do not*** end with xyz. |

The "!" character is considered to be a normal character if it appears anywhere else, but there is no practical use for it except as the first character of *matchStr*.

*dfr* is an optional data folder reference: a data folder name, an absolute or relative data folder path, or a reference returned by, for example, [GetDataFolderDFR](/igorpro/commands/getdatafolderdfr.md). The *dfr* parameter requires Igor Pro 9.00 or later.

### *Examples* {#examples}

```igor
// Returns a list of all string variables in the current data folder.
StringList("*",";")

// Returns a list of all string variables in the current data folder
// whose names begin with "S_"
StringList("S_*", ";")
```

### *See Also* {#see-also}
[VariableList](/igorpro/commands/variablelist.md), [WaveList](/igorpro/commands/wavelist.md), [DataFolderList](/igorpro/commands/datafolderlist.md)