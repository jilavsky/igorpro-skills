---
description: "The SetIgorOption operation makes temporary changes to Igor Pro's behavior."
slug: /commands/setigoroption
---

<div className="command-signature">

## <strong>SetIgorOption</strong>  [<em>mainKeyword</em>,] <em>keyword</em>=<em>value</em> {#setigoroption}

</div>
<div className="command-signature">

## <strong>SetIgorOption</strong>  [<em>mainKeyword</em>,] <em>keyword</em>=? {#setigoroption}

</div>

The SetIgorOption operation makes temporary changes to Igor Pro's behavior. The behavior changes are of interest to advanced users only and last only until you end the Igor session.

The details of the syntax depend on the keyword and are documented where the alternate behaviors are described.

SetIgorOption is not compilable. To use it in a user-defined function, you need to use [Execute](/igorpro/commands/execute.md).

In most cases the current value of a setting can be read using the *keyword* =*?* syntax.

For example, the IndependentModuleDev keyword is used to enable editing of procedure files that implement independent modules:


```igor
SetIgorOption IndependentModuleDev=?; Print V_Flag  // Query
SetIgorOption IndependentModuleDev=1                // Set
```

Most SetIgorOption keywords are obscure and rarely of use. Here are the some of the more commonly-used SetIgorOption keywords:


|  |  |
| --- | --- |
| IndependentModuleDev | See [SetIgorOption IndependentModuleDev=1](/igorpro/advanced-topics.md#setigoroption-independentmoduledev-1) |
| PoundDefine | See [Conditional Compilation](/igorpro/programming/programming.md#conditional-compilation) |
| GraphicsTechnology | See [Graphics Technology](/igorpro/graphing/making-figures/graphics.md#graphics-technology) |
| PanelResolution | See [SetIgorOption PanelResolution](/igorpro/user-interface/platform-related-issues.md#setigoroption-panelresolution) |
| DisableThreadSafe | See [Debugging ThreadSafe Code](/igorpro/programming/debugging.md#debugging-threadsafe-code) |

It is rarely necessary, but you can find the more obscure applications using Help→Search Igor Files to search for "SetIgorOption".