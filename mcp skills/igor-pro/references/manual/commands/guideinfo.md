---
description: "The GuideInfo function returns a string containing a semicolon-separated list of information about the named guide line in the named host window or subwindow."
slug: /commands/guideinfo
---

<div className="command-signature">

## <strong>GuideInfo</strong> (<em>winNameStr</em>, <em>guideNameStr</em>) {#guideinfo}

</div>

The GuideInfo function returns a string containing a semicolon-separated list of information about the named guide line in the named host window or subwindow.

### *Parameters* {#parameters}
*winNameStr* can be "" to refer to the top host window.

When identifying a subwindow with *winNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

*guideNameStr* is the name of the guide line for which you want information.

### *Details* {#details}
The returned string contains several groups of information. Each group is prefaced by a keyword and colon, and terminated with the semicolon. The keywords are as follows:


| Keyword | Information Following Keyword |
| --- | --- |
| NAME | Name of the guide. |
| WIN | Name of the window or subwindow containing the guide. |
| TYPE | The value associated with this keyword is either *User* or *Builtin*. A *User* type denotes a guide created by the DefineGuide operation, equivalent to dragging a new guide from an existing one. |
| HORIZONTAL | Either 0 for a vertical guide, or 1 for a horizontal guide. |
| POSITION | The position of the guide in points. This is the actual position relative to the left or top edge of the window, not the relative position specified to DefineGuide. |



The following keywords will be present only for user-defined guides:


| Keyword | Information Following Keyword |
| --- | --- |
| GUIDE1 | The guide is positioned relative to GUIDE1. |
| GUIDE2 | In some cases, the guide is positioned at a fractional position between GUIDE1 and GUIDE2. If the guide does not use GUIDE2, the value will be "". |
| RELPOSITION | The position relative to GUIDE1 (and GUIDE2 if applicable). This is the same as the *val* parameter in DefineGuide. The returned value is in units of points if only GUIDE1 is used, or a fractional value if both GUIDE1 and GUIDE2 are used. |

### *See Also* {#see-also}
[GuideNameList](/igorpro/commands/guidenamelist.md), [StringByKey](/igorpro/commands/stringbykey.md), [NumberByKey](/igorpro/commands/numberbykey.md), [DefineGuide](/igorpro/commands/defineguide.md)