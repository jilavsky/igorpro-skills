---
description: "The GuideNameList function returns a string containing a semicolon-separated list of guide names from the named host window or subwindow."
slug: /commands/guidenamelist
---

<div className="command-signature">

## <strong>GuideNameList</strong> (<em>winNameStr</em>, <em>optionsStr</em>) {#guidenamelist}

</div>

The GuideNameList function returns a string containing a semicolon-separated list of guide names from the named host window or subwindow.

### *Parameters* {#parameters}
*winNameStr* can be "" to refer to the top host window.

When identifying a subwindow with *winNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

*optionsStr* is used to further qualify the list of guides. It is a string containing keyword-value pairs separated by commas. Use "" to list all guides. Available options are:


|  |  |
| --- | --- |
| TYPE:*type* |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=&nbsp;BuiltIn:</td><td>List only built-in guides.</td></tr><tr><td>*type*&nbsp;=&nbsp;User:</td><td>List only user-defined guides, those created by the [DefineGuide](/igorpro/commands/defineguide.md) operation or by manually dragging a new guide from an existing one.</td></tr></tbody></table>
| HORIZONTAL:*h* |<table class="nested-table"><tbody><tr><td>*h*&nbsp;=&nbsp;0:</td><td>List only non-horizontal (that is, vertical) guides.</td></tr><tr><td>*h*&nbsp;=&nbsp;1:</td><td>List only horizontal guides.</td></tr></tbody></table>

### *Example* {#example}

```igor
String list = GuideNameList("Graph0", "TYPE:Builtin,HORIZONTAL:1")
```

### *See Also* {#see-also}
[DefineGuide](/igorpro/commands/defineguide.md), [GuideInfo](/igorpro/commands/guideinfo.md)