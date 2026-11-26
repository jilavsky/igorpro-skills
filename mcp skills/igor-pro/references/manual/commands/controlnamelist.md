---
description: "The ControlNameList function returns a string containing a list of control names in the graph or panel window or subwindow identified by winNameStr."
slug: /commands/controlnamelist
---

<div className="command-signature">

## <strong>ControlNameList</strong> (<em>winNameStr</em> [, <em>listSepStr</em> [, <em>matchStr</em> ] ]) {#controlnamelist}

</div>

The ControlNameList function returns a string containing a list of control names in the graph or panel window or subwindow identified by *winNameStr*.

### *Parameters* {#parameters}
*winNameStr* can be "" to refer to the top graph or panel.

When identifying a subwindow with *winNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

The optional parameter *listSepStr* should contain a single ASCII character such as "," or ";" to separate the names; the default value is ";".

The optional parameter *matchStr* is some combination of normal characters and the asterisk wildcard character that matches anything. To use *matchStr*, *listSepStr* must also be used. See [stringmatch](/igorpro/commands/stringmatch.md) for wildcard details.

Only control names that satisfy the match expression are returned. For example, "*_tab0"  matches all control names that end with "_tab0". The default is "*", which matches all control names.

### *Examples* {#examples}

```igor
NewPanel
Button myButton
Checkbox myCheck
Print ControlNameList("")                   // prints "myButton;myCheck;"
Print ControlNameList("", ";", "*Check")    // prints "myCheck;"
```

### *See Also* {#see-also}
[StringFromList](/igorpro/commands/stringfromlist.md), [ListMatch](/igorpro/commands/listmatch.md), [ControlInfo](/igorpro/commands/controlinfo.md), [ControlUpdate](/igorpro/commands/controlupdate.md)