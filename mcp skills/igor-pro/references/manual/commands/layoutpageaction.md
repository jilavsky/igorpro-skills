---
description: "The LayoutPageAction operation adds, deletes, reorders, or adjusts the sizes of layout pages."
slug: /commands/layoutpageaction
---

<div className="command-signature">

## <strong>LayoutPageAction</strong>  [/W=<em>winName</em> ] [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#layoutpageaction}

</div>

The LayoutPageAction operation adds, deletes, reorders, or adjusts the sizes of layout pages.

The LayoutPageAction operation was added in Igor Pro 7.00.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| appendPage | Appends a new page. |
| <span class="table-cell-nowrap">insertPage = *page*</span> | Inserts a new page before *page*. |
|  | Page numbers start from 1. Pass 0 for *page*  to insert before the first page. |
| <span class="table-cell-nowrap">page = *page*</span> | Makes *page*  the active page. |
|  | Page numbers start from 1. |
| <span class="table-cell-nowrap">deletePage = *page*</span> | Deletes *page* . This action cannot be undone. |
|  | Page numbers start from 1. |
| <span class="table-cell-nowrap">reorderPages = {*anchorPage, page1, ...*}</span> |  |
|  | Reorders the pages so that *page1* and any others appear before *anchorPage*, in the same order as their appearance in the command. |
|  | Page numbers start from 1. |
| <span class="table-cell-nowrap">size = (*width, height* )</span> | Sets the global page dimensions for the layout to *width*  and *height*, specified in units of points. |
| <span class="table-cell-nowrap">size(*page*) = (*width, height* )</span> |  |
|  | Sets the dimensions of *page*  to *width*  and *height*, specified in units of points. |
|  | Using this keyword with *page*  set to -1 modifies the global page dimensions for the layout. |
| <span class="table-cell-nowrap">margins = (*leftMargin, topMargin, rightMargin, bottomMargin* )</span> |  |
|  | Sets the global page margins for the layout to the specified values, expressed in units of points. |
| <span class="table-cell-nowrap">margins(*page*) = (*leftMargin, topMargin, rightMargin, bottomMargin* )</span> |  |
|  | Sets the margins of specified page to these values, expressed in units of points. |
|  | Page numbers start from 1. |
|  | Passing -1 for *page*  sets the global margins for the layout. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Modifies the named layout. When omitted, the actions affect the top layout. |

### *Details* {#details}
The layout as a whole has a size and margins. These are called "global" dimensions and govern all pages by default. You can set the global dimensions using the size and margins keyword without specifying a particular page.

You can override the dimensions for a given page using *size(page)*  and *margins(page)*  to specify custom dimensions.

Use *size(page)=(0,0)* to revert the specified page to the global layout dimensions. This reverts both the page size and its margins.

### *See Also* {#see-also}
[Page Layouts](/igorpro/graphing/making-figures/page-layouts.md), [NewLayout](/igorpro/commands/newlayout.md), [ModifyLayout](/igorpro/commands/modifylayout.md)