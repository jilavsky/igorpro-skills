---
description: "The StopMSTimer function frees up the timer associated with the timerRefNum and returns the number of elapsed microseconds since StartMSTimer was called for…"
slug: /commands/stopmstimer
---

<div className="command-signature">

## <strong>StopMSTimer</strong> (<em>timerRefNum</em>) {#stopmstimer}

</div>

The StopMSTimer function frees up the timer associated with the *timerRefNum* and returns the number of elapsed microseconds since StartMSTimer was called for this timer.

### *Parameters* {#parameters}
*timerRefNum* is the value returned by StartMSTimer or the special  values -1 or -2. If *timerRefNum* is not valid then StopMSTimer returns 0.

On Windows, passing -1 returns the clock frequency of the timer.

Passing -2 returns the time in microseconds since the computer was started.

### *Details* {#details}
If you want to make sure that all timers are free, call StopMSTimer ten times with *timerRefNum* equal to 0 through 9. It is OK to stop a timer that you never started.

### *Examples* {#examples}
How long does an empty loop take on your computer?


```igor
Function TestMSTimer()
	Variable timerRefNum
	Variable microSeconds
	Variable n
	timerRefNum = StartMSTimer
	if (timerRefNum == -1)
		Abort "All timers are in use"
	endif
	n=10000
	do
		n -= 1
	while (n > 0)
	microSeconds = StopMSTimer(timerRefNum)
	Print microSeconds/10000, "microseconds per iteration"
End
```

### *See Also* {#see-also}
[StartMSTimer](/igorpro/commands/startmstimer.md), [ticks](/igorpro/commands/ticks.md), [DateTime](/igorpro/commands/datetime.md)