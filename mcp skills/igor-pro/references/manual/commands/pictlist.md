---
description: "The PICTList function returns a string containing a list of pictures based on matchStr and optionsStr parameters."
slug: /commands/pictlist
---

<div className="command-signature">

## <strong>PICTList</strong> (<em>matchStr</em>, <em>separatorStr</em>, <em>optionsStr</em>) {#pictlist}

</div>

The PICTList function returns a string containing a list of pictures based on *matchStr* and *optionsStr* parameters. See details below for information on listing pictures in graphs, panels, layouts, and the picture gallery.

### *Details* {#details}
For a picture name to appear in the output string, it must match *matchStr* and also must fit the requirements of *optionsStr*. *separatorStr* is appended to each picture name as the output string is generated.

The name of each picture is compared to *matchStr*, which is some combination of normal characters and the asterisk wildcard character that matches anything. For example:


|  |  |
| --- | --- |
| "*" | Matches all picture names. |
| "xyz" | Matches picture name xyz only. |
| "\*xyz" | Matches picture names which end with xyz. |
| "xyz\*" | Matches picture names which begin with xyz. |
| "\*xyz\*" | Matches picture names which contain xyz. |
| "abc\*xyz" | Matches picture names which begin with abc and end with xyz. |

*matchStr* may begin with the "!" character to return items that do not match the rest of *matchStr*. For example:


|  |  |
| --- | --- |
| "!\*xyz" | Matches picture names which do not end with xyz. |

The "!" character is considered to be a normal character if it appears anywhere else, but there is no practical use for it except as the first character of *matchStr*.

*optionsStr* is used to further qualify the picture.

Use "" accept all pictures in the Pictures Dialog that are permitted by *matchStr*.

Use the WIN: keyword to limit the pictures to the named or target window:


|  |  |
| --- | --- |
| "WIN:" | Consider all pictures that are displayed in the top graph, panel, or layout. |
| "WIN:*windowName*" | Consider all pictures that are displayed in the named graph, panel, or layout window. |

### *Examples* {#examples}

```igor
// Returns a list of all pictures in the Pictures Dialog.
PICTList("*",";","")

// Returns a list of all pictures displayed in the top panel, graph,  or layout.
PICTList("*", ";","WIN:")

// Returns a list of pictures whose names end in "_bkg" and which are displayed in Layout0.
PICTList("*_bkg", ";", "WIN:Layout0")
```

### *See Also* {#see-also}
The [ImageLoad](/igorpro/commands/imageload.md) operation for loading PICT and other image file types into waves, and the [PICTInfo](/igorpro/commands/pictinfo.md) function.

[Pictures](/igorpro/graphing/making-figures/graphics.md#pictures), [Pictures Dialog](/igorpro/user-interface/dialog-help.md#pictures-dialog), [StringFromList](/igorpro/commands/stringfromlist.md)