---
description: "The GetWindowBrowserSelection function returns a semicolon seperated string that represents the selection in the Window Browser."
slug: /commands/getwindowbrowserselection
---

<div className="command-signature">

## <strong>GetWindowBrowserSelection</strong>  (<em>mode</em>) {#getwindowbrowserselection}

</div>

The GetWindowBrowserSelection function returns a semicolon seperated string that represents the selection in the Window Browser.

GetWindowBrowserSelection was added in Igor Pro 9.00.

### *Parameters* {#parameters}
*mode* specifies which selection should be returned:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">*mode* = 0:</span> | Returns the window names of the selected windows in the main window list. |
|  | Other values for *mode* are reserved for possible future use. |

### *Details* {#details}
If there is no selection, GetWindowBrowserSelection returns an empty string.

If the Window Browser is not open, GetWindowBrowserSelection returns an empty string and generates an error.

The order in which the selection is returned is undefined. If the order matters to you, you must sort the list yourself.

### *See Also* {#see-also}
[The Window Browser](/igorpro/igor-basics/using-igor.md#the-window-browser), [SortList](/igorpro/commands/sortlist.md)