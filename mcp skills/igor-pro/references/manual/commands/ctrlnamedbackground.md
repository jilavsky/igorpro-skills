---
description: "The CtrlNamedBackground operation creates and controls named background tasks."
slug: /commands/ctrlnamedbackground
---

<div className="command-signature">

## <strong>CtrlNamedBackground</strong>  <em>taskName</em> , <em>keyword</em>  = <em>value</em>  [, <em>keyword</em>  = <em>value</em> ...] {#ctrlnamedbackground}

</div>

The CtrlNamedBackground operation creates and controls named background tasks.

We recommend that you see [Background Tasks](/igorpro/advanced-topics.md#background-tasks) for an orientation before working with background tasks.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *taskName* | *taskName*  is the name of the background task or \_all\_ to control all named background tasks. You can use any valid standard Igor object name as the background task name. |
| <span class="table-cell-nowrap">burst [ = *b* ]</span> | Enable burst catch up mode (off by default, *b* =0). When on (*b* =1), the task is called at the maximum rate if a delay misses normal run times. |
| dialogsOK [=*d* ] | Use dialogsOK=1 to allow the background task to run when a dialog window is active. By default, dialogsOK=0 is in effect. See [Background Tasks and Dialogs](/igorpro/advanced-topics.md#background-tasks-and-dialogs) for details.<br>Setting dialogsOK to 1 can cause a crash if the background task does things the dialog does not expect. See [Background Tasks and Dialogs](/igorpro/advanced-topics.md#background-tasks-and-dialogs) for details.
| <span class="table-cell-nowrap">kill [ = *k* ]</span> | Stops and releases task memory for reuse (*k* =1; default) or continues (*k* =0). |
| <span class="table-cell-nowrap">noEvents = *mode*</span> | Controls Igor's event processing while a background task function is executing. The noEvents keyword was added in Igor Pro 8.04. |
|  | If your background task function uses a large fraction of available processor time, you may find that it is difficult to type on the command line or anywhere else. That is because Igor normally discards events that arrive while a user-defined function is running, causing events to be lost. This is the default mode of operation and corresponds to noEvents=0. |
|  | Using noEvents=1 causes Igor to postpone event handling until after the background task function returns which improves the reliability of the user interface. A consequence of using noEvents=1 is that you cannot abort a rogue background task function using [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations). |
|  | The noEvents keyword applies to all background tasks, including the unnamed background task. You should use \_all\_ for the *taskName* parameter. |
|  | *mode* defaults to 0 when Igor starts. The mode set using noEvents remains in effect until Igor quits. |
| <span class="table-cell-nowrap">period = *deltaTicks*</span> | Sets the minimum number of ticks (*deltaTicks* ) that must pass between background task invocations. *deltaTicks*  is truncated to an integer and clipped to a value greater than zero. See [Background Task Period](/igorpro/advanced-topics.md#background-task-period) for details. |
| <span class="table-cell-nowrap">proc = *funcName*</span> | Specifies name of a background user function (see Details below). |
| <span class="table-cell-nowrap">start [ = *startTicks* ]</span> | Starts when the tick count reaches *startTicks*. A task starts immediately without *startTicks*. |
| status | Returns background task information in the S_info string variable. |
| <span class="table-cell-nowrap">stop [ = *s* ]</span> | Stops the background task (*s* =1; default) or continues (*s* =0). |

### *Details* {#details}
The user function you specify via the proc keyword must have the following format:


```igor
Function myFunc(s)
	STRUCT WMBackgroundStruct &s
	...
```

The members of the `WMBackgroundStruct` are:

| Member | Description |
| --- | --- |
| char name[MAX_OBJ_NAME+1] | Background task name. |
| uint32 curRunTicks | Tick count when task was called. |
| int32 started | TRUE when `CtrlNamedBackground start` is issued. You may clear or set to desired value. |
| uint32 nextRunTicks | Precomputed value for next run but user functions may change this. |

You may also specify a user function that takes a user-defined STRUCT as long as the first elements of the structure match the `WMBackgroundStruct` or, preferably, if the first element is an instance of `WMBackgroundStruct`. Use the started field to determine when to initialize the additional fields. Your structure may not include any String, WAVE, NVAR, DFREF or other fields that reference memory that is not part of the structure itself.

If you specify a user-defined structure that matches the first fields rather than containing an instance of `WMBackgroundStruct`, then your function will fail if, in the future, the size of  the built-in structure changes. The value of `MAX_OBJ_NAME` is 255 but this may also change. It was changed from 31 to 255 in Igor Pro 8.00.

Your function should return zero unless it wants to stop in which case it should return 1.

You can call `CtrlNamedBackground` within your background function. You can even switch to a different function if desired.

Use the status keyword to obtain background task information via the S_info variable, which has the format:


```
NAME:name;PROC:fname;RUN:r;PERIOD:p;NEXT:n;QUIT:q;FUNCERR:e;
```

When parsing S_info, do not rely on the number of key-value pairs or their order. RUN, QUIT, and FUNCERR values are 1 or 0, NEXT is the tick count for the next firing of the task. QUIT is set to 1 when your function returns a nonzero value and FUNCERR is set to 1 if your function could not be used for some reason.

### *See Also* {#see-also}
See [Background Tasks](/igorpro/advanced-topics.md#background-tasks) for examples.

Also see the Background Task Demo experiment (choose File→Example Experiments→Programming→Background Task Demo).