---
description: "The Sleep operation puts Igor to sleep for a while. After the while is up, Igor continues execution."
slug: /commands/sleep
---

<div className="command-signature">

## <strong>Sleep</strong>  [ /A /W /B /C=<em>cursor</em>  /PROG={<em>cancelButtonTitleStr</em>, <em>continueButtonTitleStr</em>, <em>abortMode</em>} /Q/S /T ] <em>timeSpec</em> {#sleep}

</div>

The Sleep operation puts Igor to sleep for a while. After the while is up, Igor continues execution.

You could use Sleep, for example, to give an instrument time to perform an action or to allow a user to admire a graph before proceeding.

More advanced programmers may prefer to use a background task as an alternative. See [Background Tasks](/igorpro/advanced-topics.md#background-tasks).

### *Parameters* {#parameters}
The format of *timeSpec* depends on which flags, if any, are present.

If no flags are present, then *timeSpec* is in hh\:mm\:ss format and specifies the number of elapsed hours, minutes and seconds to sleep.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | *timeSpec* is an absolute time in 24 hour format (e.g., 16:00:00). |
| <span class="table-cell-nowrap">/A/W</span> | Wait until tomorrow if absolute time has passed. |
| <span class="table-cell-nowrap">/B</span> | Stop sleeping if the user clicks the mouse button. |
|  | The /B flag is ignored if you use the /PROG flag. |
| <span class="table-cell-nowrap">/C = *cursor*</span> | Controls what kind of cursor to display during sleep. |
|  |<table class="nested-table"><tbody><tr><td>*cursor*&nbsp;=-1:</td><td>No cursor change.</td></tr><tr><td>*cursor*&nbsp;=0:</td><td>Hour glass (default).</td></tr><tr><td>*cursor*&nbsp;=1:</td><td>Arrow.</td></tr><tr><td>*cursor*&nbsp;=2:</td><td>&quot;Click&quot;.</td></tr><tr><td>*cursor*&nbsp;=3:</td><td>Spinning beachball.</td></tr><tr><td>*cursor*&nbsp;=4:</td><td>Watch with spinning hands.</td></tr><tr><td>*cursor*&nbsp;=5:</td><td>Jacob&#39;s ladder.</td></tr><tr><td>*cursor*&nbsp;=6:</td><td>Displays a progress dialog instead of changing the cursor.</td></tr><tr><td>*cursor*&nbsp;=7:</td><td>Spinning arrows.</td></tr></tbody></table>
|  | *cursor* =\<any other value>\: watch. |
|  | *cursor* values 3 through 6 require Igor Pro 7.00 or later. |
|  | *cursor* values 7 requires Igor Pro 9.00 or later. |
|  | Under rare circumstances, cursors 0, 3, 4, and 5 may cause memory leaks. |
| <span class="table-cell-nowrap">/M = *message*</span> | If you use /C=6 or /PROG, the progress dialog displays *message* above the progress bar. By default the message reads "Sleeping". |
| <span class="table-cell-nowrap">/PROG = {*cancelButtonTitleStr*, *continueButtonTitleStr*, *abortMode*}</span> |  |
|  | Displays a progress dialog with user-settable titles for the Cancel and Continue buttons. |
|  | If you pass "" for *cancelButtonTitleStr*, the Cancel button is hidden. If you pass "" for *continueButtonTitleStr*, the Continue button is hidden. It is an error to pass "" for both buttons. |
|  | If *abortMode* is 0, the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations) and the Cancel button abort any running procedure code. If it is 1, the user abort key combinations and the Cancel button terminate the Sleep operation but user procedure code continues to run. |
|  | The /B and /Q flags are ignored if you use the /PROG flag. |
|  | See ***Displaying a Progress Dialog*** below for further information. |
| <span class="table-cell-nowrap">/Q</span> | Continue executing the procedure containing the Sleep operation even if the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations) were pressed. |
|  | The /Q flag is ignored if you use the /PROG flag. |
| <span class="table-cell-nowrap">/S</span> | *timeSpec* is a numeric expression in seconds. |
| <span class="table-cell-nowrap">/T</span> | *timeSpec* is a numeric expression in ticks. A tick is approximately 1/60 of a second. |

### *Details* {#details}
The Sleep operation does not let the user select menus, move cursors, run procedures, draw in graphs, or do any other interactive task.

Normally *timeSpec* specifies an amount of elapsed time. If the /A flag is present, then *timeSpec* is an absolute time when sleep is to end. If the specified absolute time has already passed, no sleep occurs unless you also use /W, which makes it wait until tomorrow.

If you specify time in hh\:mm\:ss format, you can also specify the time indirectly through a string variable. See the examples.

You can end sleep by pressing the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations). Normally when you do this, it aborts any procedure that is running. However, if you use the /Q flag, the procedure continues running normally.

### *Displaying a Progress Dialog* {#displaying-a-progress-dialog}
When you specify /C=6 or if you use the /PROG flag, Sleep displays a progress dialog with a progress bar showing how much of the sleep time has passed. The dialog displays a prompt which you can control using the /M flag.

If you use /PROG, then /Q and /B are ignored.

If you use /C=6, then /Q and /B have special meanings:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C = 6</span> | Progress dialog with Cancel button which aborts running procedures. |
|  | The Abort key combinations abort running user procedures. |
| <span class="table-cell-nowrap">/C = 6/B</span> | Progress dialog with Abort button which aborts running procedures. |
|  | The Abort key combinations abort running user procedures. |
| <span class="table-cell-nowrap">/C = 6/Q</span> | Progress dialog with Continue button which terminates the current sleep operation but allows procedures to continue. |
|  | Abort key combinations allow running procedures to continue. |
| <span class="table-cell-nowrap">/C = 6/B/Q</span> | Progress dialog with Continue and Abort buttons. The Continue button terminates the current sleep operation but allows procedures to continue. The Abort button aborts running procedures. |
|  | Abort key combinations allow running procedures to continue. |

If you use the /PROG flag, you can provide your own titles for the Cancel and Continue buttons.

### *Examples* {#examples}
These examples assume the current time is 4 PM:


```igor
Sleep 00:01:30              // sleeps for 1 minute, 30 seconds
Sleep/A 23:30:00            // sleeps until 11:30 PM
Sleep/A 03:00:00            // doesn't sleep at all because time is past
Sleep/A/W 03:00:00          // sleeps until 3 AM tomorrow
String str1 = "03:00:00"    // put wakeup call time in string
Sleep/A/W $str1             // sleeps until 3 AM tomorrow
Sleep/B/C=2/S/Q 60          // sleep 60 seconds, or until user clicks, and keep going (don't abort)
```

The following function creates a graph and then periodically updates the displayed data. By default, it sleeps for a number of seconds specified by the sleepTime parameter.


```igor
Function SleepDemo(sleepTime, displayProgressDialog)
	Variable sleepTime	// In seconds
	Variable displayProgressDialog	// 1 for progress dialog
	
	Make/N=200/O junk
	SetScale/I x 0, 2*pi, junk
	junk=sin(x)
	DoWindow/F SleepDemoGraph
	if (V_Flag == 0)
		Display/N=SleepDemoGraph junk
	endif
	DoUpdate
	
	try
		Variable i
		for (i = 0; i < 10; i+=1)
			if (displayProgressDialog)
				// Because the abortMode is 0, pressing the User Abort Key Combinations
				// or pressing the Done button generates an abort instead of merely
				// terminating the current Sleep call. 
				int abortMode = 0
				Sleep/S/PROG={"Done", "Continue", abortMode} sleepTime
			else
				// /B makes Sleep terminate if the user clicks.
				// Because the /Q flag is omitted, pressing the User Abort Key Combinations
				// or pressing Igor's Abort button generates an abort instead of merely
				// terminating the current Sleep call. 
				Sleep/S/C=2/B sleepTime
			endif
			junk = sin(x*(i+2))
			DoUpdate
		endfor
	catch
		Printf "An abort occurred with V_abortCode=%d\r", V_abortCode
	endtry
End
```