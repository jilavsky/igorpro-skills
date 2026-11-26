---
description: "The PauseForUser operation pauses procedure function to allow the user to manually interact with a window."
slug: /commands/pauseforuser
---

<div className="command-signature">

## <strong>PauseForUser</strong>  [/C] <em>mainWindowName</em>  [, <em>targetWindowName</em> ] {#pauseforuser}

</div>

The PauseForUser operation pauses procedure function to allow the user to manually interact with a window. For example, you can call PauseForUser from a loop to allow the user to move the cursors on a graph. In this scenario, *targetWindowName* would be the name of the graph and *mainWindowName* would be the name of a control panel containing a message telling the user to adjust the cursors and then click, for example, the Continue button.

If *targetWindowName* is omitted then *mainWindowName* plays the role of target window.

PauseForUser works with graph, table, and panel windows only.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | Tells PauseForUser to return immediately after handling any pending events. See ***Details***. |

### *Details* {#details}
During execution of PauseForUser, only mouse and keyboard activity directed toward either *mainWindowName* or *targetWindowName* is allowed.

While waiting for user action, PauseForUser disables double-clicks and any contextual menus that can lead to dialogs in order to prevent changes on the command line. It also disables killing windows by clicking the close icon in the title bar unless the window was originally created with the /K=1 flag (kill with no dialog).

If /C is omitted, PauseForUser returns only when the main window has been killed.

If /C is present, PauseForUser handles any pending events, sets V_Flag to the truth the target window still exists, and then returns control to the calling user-defined function. Use PauseForUser/C in a loop if you need to do something while waiting for the user to finish interacting with the target window, such as updating a progress indicator.

As of Igor Pro 10.04, the Abort button in the status bar is shown while PauseForUser is waiting, so you can click it to abort the procedure that called PauseForUser.

As of Igor Pro 10.04, PauseForUser checks for events using the idle period set by [SetIdlePeriod](/igorpro/commands/setidleperiod.md).

As of Igor Pro 8.00, the PauseForUser operation is allowed only in user-defined functions. It returns an error if called from a macro or from the command line.

### *See Also* {#see-also}
[Pause for User](/igorpro/programming/interacting-with-the-user.md#pause-for-user)