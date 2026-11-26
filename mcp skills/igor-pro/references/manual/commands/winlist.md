---
description: "The WinList function returns a string containing a list of windows selected based on the matchStr and optionsStr parameters."
slug: /commands/winlist
---

<div className="command-signature">

## <strong>WinList</strong> (<em>matchStr</em>, <em>separatorStr</em>, <em>optionsStr</em>) {#winlist}

</div>

The WinList function returns a string containing a list of windows selected based on the *matchStr* and *optionsStr* parameters.

### *Details* {#details}
For a window name to appear in the output string, it must match *matchStr* and also must fit the requirements of *optionsStr*. *separatorStr* is appended to each window name as the output string is generated.

The name of each window is compared to *matchStr*, which is some combination of normal characters and the asterisk wildcard character that matches anything. For example:


|  |  |
| --- | --- |
| "\*" | Matches all window names. |
| "xyz" | Matches window name xyz only. |
| "\*xyz" | Matches window names which end with xyz. |
| "xyz\*" | Matches window names which begin with xyz. |
| "\*xyz\*" | Matches window names which contain xyz. |
| "abc\*xyz" | Matches window names which begin with abc and end with xyz. |
| *matchStr* may begin with the "!" character to return items that do not match the rest of *matchStr*. For example: |  |
| "!\*xyz" | Matches window names which ***do not*** end with xyz. |

The "!" character is considered to be a normal character if it appears anywhere else, but there is no practical use for it except as the first character of *matchStr*.

*optionsStr* is used to further qualify the window. The acceptable values for *optionsStr* are:


|  |  |
| --- | --- |
| "" | Consider all windows. |
| "WIN:*windowTypes* " | Consider windows that match windowTypes. |
| "WIN:" | the target window. |
| "INCLUDE:*includeTypes* " | Consider procedure windows that match *includeTypes*. Using INCLUDE: implies WIN:128. |
| "INDEPENDENTMODULE:1" | Consider procedure windows that are part of any independent module as well as those that are not. Matching windows names are actually the window titles followed by " [\<independent module name\>]". |
|  | Using INDEPENDENTMODULE: implies WIN:128. |
| "INDEPENDENTMODULE:0" | Consider procedure windows only if they are not part of any independent module. Matching windows names are actually the window titles, which for an external file includes the file extension, such as "WMMenus.ipf". |
|  | Using INDEPENDENTMODULE: implies WIN:128. |
| "FLT:1" | Return only panels that were created with [NewPanel](/igorpro/commands/newpanel.md)/FLT=1. Specifying "FLT" also implies "WIN:64". |
|  | Omit FLT or use "FLT:0" to return windows that do not float (and most do not). |
| "FLT:2" | Return only panels that were created with [NewPanel](/igorpro/commands/newpanel.md)/FLT=2. Specifying "FLT" also implies "WIN:64". |
| "VISIBLE:1" | Return only visible windows (ignore hidden windows). |

*windowTypes* is a literal number. The window name goes into the output string only if it passes the match test and its type is compatible with *windowTypes*. *windowTypes* is a bitwise parameter:

|  |  |
| --- | --- |
| 1: | Graphs |
| 2: | Tables |
| 4: | Layouts |
| 16: | Notebooks |
| 64: | Panels |
| 128: | Procedure windows |
| 512: | Help windows |
| 4096: | XOP target windows |
| 16384: | Camera windows in Igor Pro 7.00 and later |
| 65536: | Gizmo windows in Igor Pro 7.00 and later |

See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

Procedure windows and help windows don't have names. WinList returns the window title instead.

*includeTypes* is also a literal number. The window name goes into the output string only if it passes the match test and its type is compatible with *includeTypes*. *includeTypes* is one of:

|  |  |
| --- | --- |
| 1: | Procedure windows that are not #included. |
| 2: | Procedure windows included by #include "*someFileName*" |
| 4: | Procedure windows included by #include <*someFileName*> |

or a bitwise combination of the above for more than one type of inclusion.

You can combine the `WIN`, `INCLUDE` and `INDEPENDENTMODULE` options by separating them with a comma.

When the `INDEPENDENTMODULE` option is used, the title of any procedure window that is part of an independent module will be followed by " [\<independent module name\>]". For example, if a procedure file contains:


```igor
#pragma IndependentModule=myIndependentModule
#include <Axis Utilities>
```

A call to WinList like this:


```igor
String list = WinList("* [myIndependentModule]", ";", "INDEPENDENTMODULE:1")
```

will store "Axis Utilities.ipf [myIndependentModule];" in the list string, along with any other procedure windows that are part of that independent module.

When the `INDEPENDENTMODULE` option is omitted, the returned procedure window titles do not include any independent module name suffix, and the procedure files "visible" to WinList depend on the setting of `SetIgorOption independentModuleDev` (which must be done after opening the experiment):

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">`SetIgorOption independentModuleDev = 0`</span> | Consider procedure windows only if they are not part of any independent module and if they are not hidden (using #pragma hide, for example). |
| <span class="table-cell-nowrap">`SetIgorOption independentModuleDev = 1`</span> | Consider all procedure windows including those in independent modules or hidden. |

### *Examples* {#examples}

```igor
// Returns a list of all existing non-floating windows.
String list = WinList("*",";","")

// Returns a list of all graph and table windows.
String list = WinList("*", ";","WIN:3")

// Returns a list of graphs whose names start with "Result_".
String list = WinList("Result_*", ";", "WIN:1")

// Returns a list of all floating panel windows.
String list = WinList("*", ";","WIN:64,FLT:1,FLT:2")

// Returns a list of all #included procedure windows.
String list = WinList("*", ";","INCLUDE:6")

// Returns a list of all graphs and #included procedure windows.
String list = WinList("*", ";","WIN:1,INCLUDE:6")
```

### *See Also* {#see-also}
[Independent Modules](/igorpro/advanced-topics.md#independent-modules), [WinType](/igorpro/commands/wintype.md) [ChildWindowList](/igorpro/commands/childwindowlist.md)