---
description: "The GetRTStackInfo function returns information about \"runtime stack\" (the chain of macros and functions that are executing)."
slug: /commands/getrtstackinfo
---

<div className="command-signature">

## <strong>GetRTStackInfo</strong> (<em>selector</em>) {#getrtstackinfo}

</div>

The GetRTStackInfo function returns information about "runtime stack" (the chain of macros and functions that are executing).

### *Details* {#details}
If *selector* is 0, GetRTStackInfo returns a semicolon-separated list of the macros and procedures that are executing. This list is the same you would see in the debugger's stack list.

The currently executing macro or function is the last item in the list, the macro or function that started execution is the first item in the list.

If *selector* is 1, it returns the name of the currently executing function or macro.

If *selector* is 2, it returns the name of the calling function or macro.

If *selector* is 3, GetRTStackInfo returns a semicolon-separated list of routine names, procedure file names and line numbers. This is intended for advanced debugging by advanced programmers only.

For example, if RoutineA in procedure file ProcA.ipf calls RoutineB in procedure file ProcB.ipf and RoutineB calls GetRTStackInfo(3), it will return:


```
RoutineA,ProcA.ipf,7;RoutineB,ProcB.ipf,12;
```

The numbers 7 and 12 would be the actual numbers of the lines that were executing in each routine. Line numbers are zero-based.

When called from a function started by [MultiThread](/igorpro/programming/keywords/other-programming-keywords.md#multithread) or [ThreadStart](/igorpro/commands/threadstart.md) the runtime stack information begins with the function that started threaded execution.

In future versions of Igor, *selector* may request other kinds of information.

### *Main Thread Example* {#main-thread-example}

```igor
Function Called()
	Print "Called by " + GetRTStackInfo(2) + "()"
	Print "Routines in calling chain: " + GetRTStackInfo(0)
End

Function Calling()
	Called()
End

Macro StartItUp()
	Calling()
End

// Executing StartItUp() prints:
  Called by Calling()
  Routines in calling chain: StartItUp;Calling;Called;
```

### *MultiThread Example* {#multithread-example}

```igor
Macro BeginMultiThread(code)
	Variable code=3
	BeginMultiThreadFunc(code)
End
	
Function BeginMultiThreadFunc(Variable code)	
	Make/O/N=4/T/FREE textWave
	MultiThread textWave = tsworker(code)
	Print textWave[0]
End

ThreadSafe Function/S tsworker(Variable code)
	String str= tssubr(code)
	return str
End

ThreadSafe Function/S tssubr(Variable code)
	String str= GetRTStackInfo(code)
	return str
End

// Executing BeginMultiThread(3) prints details for only the two threaded routines:
	tsworker,TSExample,16;tssubr,TSExample,21;
```

### *See Also* {#see-also}
[The Stack and Objects Lists](/igorpro/programming/debugging.md#the-stack-and-objects-lists), [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking), [GetRTError](/igorpro/commands/getrterror.md)