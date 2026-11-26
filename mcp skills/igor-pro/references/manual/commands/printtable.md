---
description: "The PrintTable operation prints the named table window. winName is the window name of the table to print."
slug: /commands/printtable
---

<div className="command-signature">

## <strong>PrintTable</strong>  [ /P=(<em>startPage</em>,<em>endPage</em>) /S=<em>s</em> ] <em>winName</em> {#printtable}

</div>

The PrintTable operation prints the named table window.

### *Parameters* {#parameters}
*winName* is the window name of the table to print.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/P = (*startPage*,*endPage*) Specifies a page range to print. 1 is the first page.</span> |  |
|  | If /P is omitted all pages are printed unless /S is used. |
| /S=*selection* |<table class="nested-table"><tbody><tr><td>*selection*&nbsp;=&nbsp;0:</td><td>Print entire table (default).</td></tr><tr><td>*selection*&nbsp;=&nbsp;1:</td><td>Print selection only.</td></tr></tbody></table>

### *See Also* {#see-also}
[Tables](/igorpro/igor-basics/tables.md)

[PrintSettings](/igorpro/commands/printsettings.md), [PrintGraphs](/igorpro/commands/printgraphs.md), [PrintLayout](/igorpro/commands/printlayout.md), [PrintNotebook](/igorpro/commands/printnotebook.md)