---
description: "The PrintNotebook operation prints the named notebook window. notebookName is either kwTopWin for the top notebook window, the name of a notebook window or a…"
slug: /commands/printnotebook
---

<div className="command-signature">

## <strong>PrintNotebook</strong>  [/B=<em>hiResMethod</em> /P=(<em>startPage</em>,<em>endPage</em>)/S=<em>s</em>] <em>notebookName</em> {#printnotebook}

</div>

The PrintNotebook operation prints the named notebook window.

### *Parameters* {#parameters}
*notebookName* is either kwTopWin for the top notebook window, the name of a notebook window or a host-child specification (an hcSpec) such as Panel0#nb0. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on host-child specifications.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *hiResMethod*</span> | This flag is no longer supported and has no effect. |
|  |<table class="nested-table"><tbody><tr><td>*hiResMethod*&nbsp;=1:</td><td>Print HiRes PICTs using high resolution bitmaps.</td></tr><tr><td>*hiResMethod*&nbsp;=&nbsp;0:</td><td>Don&#39;t print HiRes PICTs using high resolution bitmaps.</td></tr><tr><td>*hiResMethod*&nbsp;=&nbsp;-1:</td><td>Print using the default method. Currently, this prints HiRes PICTs using high resolution bitmaps and is the same as method 1.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/P = (*startPage*,*endPage*)</span> | Specifies a page range to print. 1 is the first page. |
| /S=*selection* |<table class="nested-table"><tbody><tr><td>*selection*&nbsp;=&nbsp;0:</td><td>Print entire notebook (default).</td></tr><tr><td>*selection*&nbsp;=&nbsp;1:</td><td>Print selection only.</td></tr></tbody></table>

### *Details* {#details}
If no /B flag is given, the default method of handling HiRes PICTs is used (/B=1).

### *See Also* {#see-also}
[Notebooks](/igorpro/igor-basics/notebooks.md)

[PrintSettings](/igorpro/commands/printsettings.md), [PrintGraphs](/igorpro/commands/printgraphs.md), [PrintTable](/igorpro/commands/printtable.md), [PrintLayout](/igorpro/commands/printlayout.md)