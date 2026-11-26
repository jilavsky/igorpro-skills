---
description: "The GetBrowserSelection function returns a string containing the full path, quoted if necessary, to a selected Data Browser item."
slug: /commands/getbrowserselection
---

<div className="command-signature">

## <strong>GetBrowserSelection</strong>  (<em>index</em> [, <em>mode</em>]) {#getbrowserselection}

</div>

The GetBrowserSelection function returns a string containing the full path, quoted if necessary, to a selected Data Browser item.

### *Parameters* {#parameters}
*index* is the zero-based index of the selected item of interest, starting from the top of the list. If *index* is out of range, GetBrowserSelection returns an empty string.

*mode* is an optional parameter that specifies which data browser the function applies to.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">*mode* = 0:</span> | Targets the modal data browser if it is visible, otherwise the regular data browser. This is the default value. |
| <span class="table-cell-nowrap">*mode* = 1:</span> | Targets the regular data browser. |
| <span class="table-cell-nowrap">*mode* = 2:</span> | Targets the modal data browser. |

See [CreateBrowser](/igorpro/commands/createbrowser.md) for a discussion of the regular versus the modal data browser.

### *Details* {#details}
If the Data Browser is not open, GetBrowserSelection returns an empty string and generates an error.

As a special case, passing -1 for *index* returns a comma separated string containing the settings of the three Data Browser checkboxes. If the Data Browser is not open, no error is generated. For example:


```igor
Print GetBrowserSelection(-1)
```

might produce


```
ShowWaves=1,ShowVars=0,ShowStrs=1
```

### *Example* {#example}

```igor
Function DisplaySelectedBrowserWaves()
	String name = GetBrowserSelection(0)
	if (strlen(name))
		Display $name
	endif

	Variable index=1
	do
		name = GetBrowserSelection(index)
		if (strlen(name) <= 0)
			break
		endif
		AppendToGraph $name
		index+=1
	while(1)
End
```

### *See Also* {#see-also}

[The Data Browser](/igorpro/igor-basics/data-folders.md#the-data-browser), [CreateBrowser](/igorpro/commands/createbrowser.md), [ModifyBrowser](/igorpro/commands/modifybrowser.md), [GetBrowserLine](/igorpro/commands/getbrowserline.md)