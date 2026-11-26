---
description: "GetErrMessage returns a string containing an explanation of the error associated with errorCode."
slug: /commands/geterrmessage
---

<div className="command-signature">

## <strong>GetErrMessage</strong> (<em>errorCode</em> [, <em>substitutionOption</em>]) {#geterrmessage}

</div>

GetErrMessage returns a string containing an explanation of the error associated with *errorCode*. It is most useful for programmers providing custom error handling in user-defined functions.

The [GetRTErrMessage](/igorpro/commands/getrterrmessage.md) function provides a simpler way to get a description of an error in a user-defined function.

For an overview of error handling, see [Flow Control for Aborts](/igorpro/programming/programming.md#flow-control-for-aborts).

### *Details* {#details}
*errorCode* is an Igor error code. Usually you obtain the error code during execution of a user-defined function via the [GetRTError](/igorpro/commands/getrterror.md) function or from the V_Flag variable created by many Igor operations.

If multiple errors occur in a user-defined function, this may result in GetErrMessage returning an incomplete error message. See the MultipleErrors example below. You can achieve more reliable error reporting by calling [GetRTErrMessage](/igorpro/commands/getrterrmessage.md) from a [try-catch-endtry](/igorpro/programming/keywords/flow-control.md#try-catch-endtry) block.

### *Substitution* {#substitution}
For a few error codes, the corresponding error message is designed to be combined with "substituted" information available only immediately after the error occurs. An example is the "parameter out of range" error which produces an error message such as "expected number between *x* and *y*".  The optional *substitutionOption* parameter gives you control over substitution.

To get the correct error message, you must call GetErrMessage immediately after calling the function or operation that generated the error and you must pass the appropriate value for *substitutionOption*.

Igor maintains two contexts which store the substitution information: one for user-defined functions and one for all other contexts (command line execution, macros, and the Execute operation).

Set *substitutionOption* to one of these values:


| substitutionOption | GetErrMessage Action |
| --- | --- |
| 0 | Substitution values are filled in with "\_Not Available\_". This is the default when *substitutionOption* is not specified. |
| 1 | Substitution values are blank. |
| 2 | Substitution is performed based on the assumption that the error was received while executing a macro or a command using Igor's command line. This includes a command executed via the Execute operation even from a user-defined function because such commands are executed as if entered in the command line. |
| 3 | Substitution is performed based on the assumption that the error was received while executing a user-defined function. |

For most purposes you should pass 3 for *substitutionOption* when the error was generated in a user-defined function other than through the Execute operation and pass 2 otherwise.

### *Examples* {#examples}

```igor
// Macro, Execute or command line example
Execute/Q/Z "Duplicate/O nonexistentWave, dup"
Print GetErrMessage(V_Flag,2)
// Prints: expected wave name

// Function example
Function Test()
    Make/O/N=(2,2) data= 0
    FilterIIR/COEF=data/LO=999/Z data   // Purposely wrong /LO value
    Print GetErrMessage(V_Flag,3)       // Substitution assuming user-defined function
End
// Executing Test() prints:
// "expected /LO frequency between 0 and 0.5"

// Multiple error example
// Because of the first error, an assignment to a null wave reference,
// the substitution information for the FilterIIR operation is not available.
Function MultipleErrors()
	Make/O/N=(2,2) data= 0
	WAVE ww = $""

	// Generates error because ww is not valid
	ww = 0

	// Generates another error because of purposely wrong /LO value
	FilterIIR/COEF=data/LO=999/Z data

    Print GetErrMessage(V_Flag,3)       // Substitution assuming user-defined function
End
// Executing MultipleErrors() prints:
// "expected  between  and "            // Wave error masks /LO error reporting
```

### *See Also* {#see-also}
[Flow Control for Aborts](/igorpro/programming/programming.md#flow-control-for-aborts), [GetRTErrMessage](/igorpro/commands/getrterrmessage.md), [GetRTError](/igorpro/commands/getrterror.md)