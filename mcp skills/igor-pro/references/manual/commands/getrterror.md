---
description: "The GetRTError function returns information about the error state of Igor's user-defined function runtime execution environment."
slug: /commands/getrterror
---

<div className="command-signature">

## <strong>GetRTError</strong> (<em>flag</em>) {#getrterror}

</div>

The GetRTError function returns information about the error state of Igor's user-defined function runtime execution environment.

If *flag* is 0, GetRTError returns an error code if an error has occurred or 0 if no error has occurred.

If *flag* is 1, GetRTError returns an error code if an error has occurred or 0 if no error has occurred and it clears the error state of Igor's runtime execution environment. Use this if you want to detect and handle runtime errors yourself.

If *flag* is 2, GetRTError returns the state of Igor's internal abort flag but does not clear it.

For *flag*=0 and *flag*=1, you can call [GetErrMessage](/igorpro/commands/geterrmessage.md) to obtain the error message associated with the returned error code, if any.

In Igor Pro 7.00 or later, using GetRTError(1) on the same line as a command that causes an error overrides the debugger "debug on error" setting and prevents the debugger from activating for that error.

### *Example* {#example}

```igor
// Detect and handle a runtime error rather than allowing it to cause
// Igor to abort execution or invoke the debugger. The error must be
// recorded, using GetErrMessage, and cleared, using GetRTError,
// on the same line as the error.
Function Demo()
	String msg
	Variable err
	Make/O/N=(-2) wave0; msg=GetErrMessage(GetRTError(0),3); err=GetRTError(1)
	if (err != 0)
		Print "Error in Demo: " + msg
		Print "Continuing execution"
	endif
	// Do more things here
End
```

### *See Also* {#see-also}
[GetErrMessage](/igorpro/commands/geterrmessage.md), [GetRTErrMessage](/igorpro/commands/getrterrmessage.md)