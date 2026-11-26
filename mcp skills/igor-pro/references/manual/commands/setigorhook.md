---
description: "The SetIgorHook operation tells Igor to call a user-defined \"hook\" function at the following times."
slug: /commands/setigorhook
---

<div className="command-signature">

## <strong>SetIgorHook</strong>   [/K/L] [<em>hookType</em>  [=<em>procName</em> ] ] {#setigorhook}

</div>

The SetIgorHook operation tells Igor to call a user-defined "hook" function at the following times:

- After procedures have been successfully compiled ([AfterCompiledHook](/igorpro/advanced-topics.md#aftercompiledhook))
- After a file is opened ([AfterFileOpenHook](/igorpro/advanced-topics.md#afterfileopenhook))
- After the MDI frame window is resized on Windows ([AfterMDIFrameSizedHook](/igorpro/advanced-topics.md#aftermdiframesizedhook))
- After a window is created ([AfterWindowCreatedHook](/igorpro/advanced-topics.md#afterwindowcreatedhook))
- Before [the debugger](/igorpro/programming/debugging.md#the-debugger) is opened ([BeforeDebuggerOpensHook](/igorpro/advanced-topics.md#beforedebuggeropenshook))
- Before an experiment is saved ([BeforeExperimentSaveHook](/igorpro/advanced-topics.md#beforeexperimentsavehook))
- Before a file is opened ([BeforeFileOpenHook](/igorpro/advanced-topics.md#beforefileopenhook))
- Before a new experiment is opened ([IgorBeforeNewHook](/igorpro/advanced-topics.md#igorbeforenewhook))
- Before Igor quits ([IgorBeforeQuitHook](/igorpro/advanced-topics.md#igorbeforequithook))
- When a menu item is selected ([IgorMenuHook](/igorpro/advanced-topics.md#igormenuhook))
- During Igor's quit processing ([IgorQuitHook](/igorpro/advanced-topics.md#igorquithook))
- When Igor starts or a new experiment is created ([IgorStartOrNewHook](/igorpro/advanced-topics.md#igorstartornewhook))

The term "hook" is used as in the phrase "to hook into", meaning to intercept or to attach.

Hook functions are typically used by a sophisticated procedure package to make sure that the package's private data is consistent.

In addition to using SetIgorHook, you can designate hook functions using fixed function names (see [User-Defined Hook Functions](/igorpro/advanced-topics.md#user-defined-hook-functions)). The advantage of using SetIgorHook over fixed hook names is that you don't have to worry about name conflicts.

You can designate hook functions for specific windows using window hooks (see [SetWindow](/igorpro/commands/setwindow.md)).

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/K</span> | Removes *procName*  from the list of functions called for the *hookType* events. |
|  | If *procName* is not specified all *hookType*  functions are removed. |
|  | If *hookType* is not specified all functions are removed for all *hookType* events, returning Igor to the pre-SetIgorHook state. |
| <span class="table-cell-nowrap">/L</span> | Executes *procName* last. Without /L, a newly added hook function runs before previously registered hook functions. |
|  | A function that has been previously registered with SetIgorHook can be moved from being called first to being called last by calling SetIgorHook again with /L. |
|  | To move a function from being called last to being called first requires removing the hook function with /K and then calling SetIgorHook without /L. |

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *hookType* | Specifies one of the fixed-name hook function names: |
|  | [AfterCompiledHook](/igorpro/advanced-topics.md#aftercompiledhook) |
|  | [AfterFileOpenHook](/igorpro/advanced-topics.md#afterfileopenhook) |
|  | [AfterMDIFrameSizedHook](/igorpro/advanced-topics.md#aftermdiframesizedhook) |
|  | [AfterWindowCreatedHook](/igorpro/advanced-topics.md#afterwindowcreatedhook) |
|  | [BeforeDebuggerOpensHook](/igorpro/advanced-topics.md#beforedebuggeropenshook) |
|  | [BeforeExperimentSaveHook](/igorpro/advanced-topics.md#beforeexperimentsavehook) |
|  | [BeforeFileOpenHook](/igorpro/advanced-topics.md#beforefileopenhook) |
|  | [IgorBeforeNewHook](/igorpro/advanced-topics.md#igorbeforenewhook) |
|  | [IgorBeforeQuitHook](/igorpro/advanced-topics.md#igorbeforequithook) |
|  | [IgorMenuHook](/igorpro/advanced-topics.md#igormenuhook) |
|  | [IgorQuitHook](/igorpro/advanced-topics.md#igorquithook) |
|  | [IgorStartOrNewHook](/igorpro/advanced-topics.md#igorstartornewhook) |
|  | See the note below about these *hookType* names. |
|  | *hookType* is required unless the /K flag is specified. |
| *procName* | Names the user-defined hook function that is called for the *hookType* event. |

### *Details* {#details}
The parameters and return type of the user-defined function *procName* varies depending on the *hookType* it is registered for.

For example, a function registered for the AfterFileOpenHook type must have the same parameters and return type as the shown for the [AfterFileOpenHook](/igorpro/advanced-topics.md#afterfileopenhook) function as described in [User-Defined Hook Functions](/igorpro/advanced-topics.md#user-defined-hook-functions).

The *procName* function is ***called after*** any window-specific hook for these *hookTypes*, and the *procName* function ***is called before*** any other hook functions previously registered by calling SetIgorHook ***unless the /L flag is given***, in which case it still runs after window-specific hook functions, but also ***after*** all other previously registered hook functions.

The *procName* function should return a nonzero value (1 is typical) to prevent later functions from being called. Returning 0 allows successive functions to be called.

SetIgorHook does not work at Igor start or new experiment time, so SetIgorHook IgorStartOrNewHook is disallowed. Define a global or static fixed-name [IgorStartOrNewHook](/igorpro/advanced-topics.md#igorstartornewhook) function as described in [User-Defined Hook Functions](/igorpro/advanced-topics.md#user-defined-hook-functions).

The saved Igor experiment file remembers the SetIgorHooks that are in effect when the experiment is saved.

### *Hook Function Interactions* {#hook-function-interactions}
After all the SetIgorHook functions registered for *hookType* have run (and all have returned 0), any static fixed-name hook functions are called and then the (only) nonstatic fixed-name user-defined hook function, if any, is called. As an example, when a menu event occurs, Igor handles the event by calling routines in this order:


1.	The top window's hook function as set by SetWindow


2.	Any SetIgorHook-registered hook functions


3.	All of the fixed-named IgorMenuHook functions:
	- First any static IgorMenuHook functions (in any independent module)
	- Then the one-and-only non-static IgorMenuHook function (in only the ProcGlobal independent module)

|  |  |  |
| --- | --- | --- |
| 1. [SetWindow](/igorpro/commands/setwindow.md) event | 2. [SetIgorHook](/igorpro/commands/setigorhook.md) *hookType* | 3. User-defined Hook Function(s) |
| (called first) | (called second) | (called last) |
| enableMenu | IgorMenuHook | IgorMenuHook |
| menu | IgorMenuHook | IgorMenuHook |

:::note
Although you can technically use one of the fixed-name functions, as described in User-Defined Hook Functions, for procName, the result would be that the function will be called twice: once as a registered named hook function and once as the fixed-named hook function. That is, don't use SetIgorHook this way:
:::

```igor
SetIgorHook AfterFileOpenHook=AfterFileOpenHook		// NO
```

### *Variables* {#variables}
SetIgorHook returns information in the following variables:


|  |  |
| --- | --- |
| S_info | Semicolon-separated list of all current hook functions associated with *hookType*, listed in the order in which they are called. S_info includes the full independent module paths (e.g.,"ProcGlobal#MyMenuHook;MyIM#MyModule#MyMenuHook;"). |

### *Examples* {#examples}
This hook function invokes the Export Graphics menu item when Ctrl+C is selected for a graph, preventing Igor from performing the usual Copy.


```igor
SetIgorHook IgorMenuHook=CopyIsExportHook

Function CopyIsExportHook(isSelection,menuName,itemName,itemNo,win,wType)
    Variable isSelection
    String menuName,itemName
    Variable itemNo
    String win
    Variable wType

    Variable handledIt= 0
    if( isSelection && wType==1 )       // menu was selected, window is graph
        if( Cmpstr(menuName,"Edit")==0 && CmpStr(itemName,"Copy")==0 )
            DoIgorMenu "Edit", "Export Graphics"	// dialog instead
            handledIt= 1                // don't call other IgorMenuHook functions.
        endif
    endif
    return handledIt
End
```

To unregister CopyIsExportHook as a hook procedure:


```igor
SetIgorHook/K IgorMenuHook=CopyIsExportHook // unregister CopyIsExportHook
```

To discover which functions are associated with a *hookType*, use a command such as:


```igor
SetIgorHook IgorMenuHook    // inquire about names registered for IgorMenuHook
Print S_info                // list of functions
```

To remove (or "unregister") named hooks:


```igor
SetIgorHook/K                               // removes all hook functions for all hookTypes
SetIgorHook/K IgorMenuHook                  // removes all IgorMenuHook functions
SetIgorHook/K IgorMenuHook=CopyIsExportHook // removes only this hook function
```

### *See Also* {#see-also}
[SetWindow](/igorpro/commands/setwindow.md), [IgorStartOrNewHook](/igorpro/advanced-topics.md#igorstartornewhook), [User-Defined Hook Functions](/igorpro/advanced-topics.md#user-defined-hook-functions)

[Independent Modules](/igorpro/advanced-topics.md#independent-modules)