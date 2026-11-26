---
description: "The Execute operation executes the contents of cmdStr as if it had been typed in the command line."
slug: /commands/execute
---

<div className="command-signature">

## <strong>Execute</strong>  [/Z] <em>cmdStr</em> {#execute}

</div>

The Execute operation executes the contents of cmdStr  as if it had been typed in the command line.

The most common use of Execute is to call a macro or an external operation from a user-defined function. This is necessary because Igor does not allow you to make such calls directly. See [The Execute Operation](/igorpro/programming/programming-techniques.md#the-execute-operation) for other uses.

When the /Z flag is used, an error code is placed in V_flag. The error code will be -1 if a missing parameter style macro is called and the user clicks Quit Macro, or zero if there was no error.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Errors are not fatal and error dialogs are suppressed. |

### *Details* {#details}

Because the command line and command buffer are limited to 2500 bytes on a single line, *cmdStr* is likewise limited to a maximum of 2500 executable bytes.

Do not reference local variables in *cmdStr*. The command is not executed in the local environment provided by a macro or user-defined function.

Execute can accept a string expression containing a macro. The string must start with Macro, Proc, or Window, and must follow the normal rules for macros. All lines must be terminated with carriage returns including the last line. The name of the macro is not important but must exist. Errors will be reported except when using the /Z flag, which will assign V_Flag a nonzero number in an error condition.

### *Examples* {#examples}

It is a good idea to compose the command to be executed in a local string variable and then pass that string to the Execute operation. This prints the string to the history for debugging:

```igor
String cmd
sprintf cmd, "GBLoadWave/P=%s/S=%d \"%s\"", pathName, skipCount, fileName
Print cmd			// For debugging
Execute cmd
// Execute with a macro:
Execute "Macro junk(a,b)\rvariable a=1,b=2\r\rprint \"hello from macro\",a,b\rEnd\r"
```

<div className="command-signature">

## <strong>Execute</strong>  /P [/Q/Z] <em>cmdStr</em> {#execute}

</div>

Execute/P is similar to Execute except the command string, *cmdStr*, is not immediately executed but rather is posted to an operation queue. Items in the operation queue execute only when nothing else is happening. Macros and functions must not be running and the command line must be empty.

### *Flags* {#execute-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | Command is not printed in the command line or history area. |
| <span class="table-cell-nowrap">/Z</span> | Error dialogs are suppressed. |

### *See Also* {#see-also}
[Operation Queue](/igorpro/advanced-topics.md#operation-queue) for more details on using Execute/P with Igor's operation queue.