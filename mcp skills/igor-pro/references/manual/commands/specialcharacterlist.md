---
description: "The SpecialCharacterList function returns a string containing a list of names of special characters in a formatted text notebook."
slug: /commands/specialcharacterlist
---

<div className="command-signature">

## <strong>SpecialCharacterList</strong> (<em>notebookNameStr</em>, <em>separatorStr</em>, <em>mask</em>, <em>flags</em>) {#specialcharacterlist}

</div>

The SpecialCharacterList function returns a string containing a list of names of special characters in a formatted text notebook.

### *Parameters* {#parameters}
If *notebookNameStr* is "", the top visible notebook is used. Otherwise n*otebookNameStr* contains either kwTopWin for the top notebook window, the name of a notebook window or a host-child specification (an hcSpec) such as Panel0#nb0. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on host-child specifications.

*separatorStr* should contain a single ASCII character, usually semicolon, to separate the names.

*mask* determines which types of special characters are included. *mask* is a bitwise parameter with values:

|  |  |
| --- | --- |
| 1: | Pictures including graphs, tables and layouts. |
| 2: | Notebook actions. |
| 4: | All other special characters such as dates and times. |

or a bitwise combination of the above for more than one type. See Setting Bit Parameters on page IV-16 for details about bit settings.

*flags* is a bitwise parameter. Pass 0 to include all special characters or 1 to include only selected special characters. All other bits are reserved and should be passed as zero.

### *Details* {#details}
Only formatted text notebooks have special characters. When called for a plain text notebook, SpecialCharacterList always returns "".

### *Examples* {#examples}

```igor
// Prints a list of all special characters in the top notebook.
Print SpecialCharacterList("", ";", -1, 0)

// Prints a list of notebook action characters in Notebook0.
Print SpecialCharacterList("Notebook0", ";", 2, 0)

// Prints a list of selected notebook action characters in Notebook0.
Print SpecialCharacterList("Notebook0", ";", 2, 1)
```

### *See Also* {#see-also}
[Notebook](/igorpro/commands/notebook.md), [NotebookAction](/igorpro/commands/notebookaction.md), [SpecialCharacterInfo](/igorpro/commands/specialcharacterinfo.md)