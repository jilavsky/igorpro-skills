---
description: "The ListMatch function returns each list item in listStr that matches matchStr."
slug: /commands/listmatch
---

<div className="command-signature">

## <strong>ListMatch</strong> (<em>listStr</em>, <em>matchStr</em> [, <em>listSepStr</em> ]) {#listmatch}

</div>

The ListMatch function returns each list item in *listStr* that matches *matchStr*.

*ListStr* should contain items separated by *listSepStr* which typically is ";".

You may include asterisks in *matchStr* as a wildcard character. Note that matching is case-insensitive. See [stringmatch](/igorpro/commands/stringmatch.md) for wildcard details.

*ListSepStr* is optional. If omitted it defaults to ";".

### *See Also* {#see-also}
[GrepList](/igorpro/commands/greplist.md), [stringmatch](/igorpro/commands/stringmatch.md), [StringFromList](/igorpro/commands/stringfromlist.md), [WhichListItem](/igorpro/commands/whichlistitem.md)