---
description: "The GrepList function returns each list item in listStr that matches the regular expression regExprStr."
slug: /commands/greplist
---

<div className="command-signature">

## <strong>GrepList</strong> (<em>listStr</em>, <em>regExprStr</em> [,<em>reverse</em> [, <em>listSepStr</em>]]) {#greplist}

</div>

The GrepList function returns each list item in *listStr* that matches the regular expression *regExprStr*.

*ListStr* should contain items separated by *listSepStr* which typically is ";".

*regExprStr* is a regular expression such as is used by the UNIX grep(1) command. It is much more powerful than the wildcard syntax used for [ListMatch](/igorpro/commands/listmatch.md). See [Regular Expressions](/igorpro/programming/programming-techniques.md#regular-expressions) for *regExprStr* details.

*Reverse* is optional. If missing, it is taken to be 0.  If reverse is nonzero then the sense of the match is reversed. For example, if *regExprStr* is "^abc" and *reverse* is 1, then all list items that do **not** start with "abc" are returned.

*ListSepStr* is optional. If omitted it defaults to ";". In order to specify *listSepStr*, you must precede it with *reverse*.

### *Examples* {#examples}
To list ColorTables containing "Red", "red", or "RED" (etc):


```igor
Print GrepList(CTabList(),"(?i)red")	// case-insensitive matching
```

To list window recreation commands starting with "\tCursor":


```igor
Print GrepList(WinRecreation("Graph0", 0), "^\tCursor", 0 , "\r")
```

### *See Also* {#see-also}
[ListMatch](/igorpro/commands/listmatch.md), [Grep](/igorpro/commands/grep.md), [StringFromList](/igorpro/commands/stringfromlist.md), [WhichListItem](/igorpro/commands/whichlistitem.md)