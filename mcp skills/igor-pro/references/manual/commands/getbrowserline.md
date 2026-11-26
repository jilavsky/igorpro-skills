---
description: "The GetBrowserLine function returns the zero-based line number of the data folder referenced by fullPathStr."
slug: /commands/getbrowserline
---

<div className="command-signature">

## <strong>GetBrowserLine</strong>  (<em>fullPathStr</em> [, <em>mode</em>]) {#getbrowserline}

</div>

The GetBrowserLine function returns the zero-based line number of the data folder referenced by *fullPathStr* .

If *fullPathStr* does not point to a data folder or points to a data folder that in a collapsed data folder in the Data Browser, GetBrowserLine returns -1.

### *Parameters* {#parameters}
*fullPathStr* is a string containing a full path to a data folder. It may be quoted or unquoted.

*mode* is an optional parameter that specifies which data browser the function applies to.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">*mode* = 0:</span> | Targets the modal data browser if it is visible, otherwise the regular data browser. This is the default value. |
| <span class="table-cell-nowrap">*mode* = 1:</span> | Targets the regular data browser. |
| <span class="table-cell-nowrap">*mode* = 2:</span> | Targets the modal data browser. |

See [CreateBrowser](/igorpro/commands/createbrowser.md) for a discussion of the regular versus the modal data browser.

### *See Also* {#see-also}

|  |
| --- |
| [The Data Browser](/igorpro/igor-basics/data-folders.md#the-data-browser), [CreateBrowser](/igorpro/commands/createbrowser.md), [ModifyBrowser](/igorpro/commands/modifybrowser.md), [GetBrowserSelection](/igorpro/commands/getbrowserselection.md) |