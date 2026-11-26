---
description: "The DoUpdate operation updates windows and dependent objects. Call DoUpdate from an Igor procedure to force Igor to update any objects that need updating."
slug: /commands/doupdate
---

<div className="command-signature">

## <strong>DoUpdate</strong>  [ /E=<em>e</em>  /W=<em>targWin</em>  /SPIN=<em>ticks</em> ] {#doupdate}

</div>

The DoUpdate operation updates windows and dependent objects.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/E = *e*</span> | Used with /W, /E=1 marks window as a progress window that can accept mouse events while user code is executing. Currently, only control panel windows can be used as a progress window. |
|  | If another window is currently marked as a progress window, this will un-mark the other window. |
| <span class="table-cell-nowrap">/W = *targWin*</span> | Updates only the specified window. Does not update dependencies or do any other updating. |
|  | Currently, only graph and panel windows honor the /W flag. |
|  | V_Flag is set to the truth the window exists. See [Progress Windows](/igorpro/programming/interacting-with-the-user.md#progress-windows) for other values for V_Flag. |
| <span class="table-cell-nowrap">/SPIN = *ticks*</span> | Sets the delay between the start of a control procedure and the spinning beachball. *ticks* is the delay in ticks (60th of a second.) Unless used with the /W flag, /SPIN just sets the delay and an update is not done. |

### *Details* {#details}
Call DoUpdate from an Igor procedure to force Igor to update any objects that need updating. Igor updates any windows that need to be updated and also any objects (string variables, numeric variables, waves, controls) that depend on other objects that have changed since the last update. Page layout windows may not be immediately updated. For more information on page layout updates, see [Automatic Updating of Layout Objects](/igorpro/graphing/making-figures/page-layouts.md#automatic-updating-of-layout-objects).

Igor performs updates automatically if:

- No user-procedure is running.
- An interpreted procedure (Macro, Proc, Window type procedures) is running and PauseUpdate or DelayUpdate are not in effect.

Igor does not perform an automatic DoUpdate while a user-defined function is running. You can call DoUpdate from a user-defined function to force Igor to update.

### *See Also* {#see-also}
[DelayUpdate](/igorpro/commands/delayupdate.md), [PauseUpdate](/igorpro/commands/pauseupdate.md), [ResumeUpdate](/igorpro/commands/resumeupdate.md), [Progress Windows](/igorpro/programming/interacting-with-the-user.md#progress-windows)