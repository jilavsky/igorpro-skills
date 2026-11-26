---
description: "The ToCommandLine operation sends command text to the command line without executing the command(s)."
slug: /commands/tocommandline
---

<div className="command-signature">

## <strong>ToCommandLine</strong>  <em>commandsStr</em> {#tocommandline}

</div>

The ToCommandLine operation sends command text to the command line without executing the command(s).

The intended usage is for user-created panel windows with "To Cmd Line" buttons that are mimicking built-in Igor dialogs. You'll usually want to use [Execute](/igorpro/commands/execute.md), instead.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *commandsStr* | The text of one or more commands. |

### *Details* {#details}
To send more than one line of commands, separate the commands with "\r" characters.

:::note
ToCommandLine does not work when typed on the command line; use it only in a Macro, Proc, or Function.
:::

### *Examples* {#examples}

```igor
Macro CmdPanel()
	PauseUpdate; Silent 1
	NewPanel /W=(150,50,430,229)
	Button toCmdLine,pos={39,148},size={103,20},title="To Cmd Line"
	Button toCmdLine,proc=ToCmdLineButtonProc
End

Function ToCmdLineButtonProc(ctrlName) : ButtonControl
	String ctrlName
	
	String cmd="MyFunction(xin,yin,\"yResult\")"		// line 1: generate results
	cmd +="\rDisplay yOutput vs wx as \"results\""	// line 2: display results
	ToCommandLine cmd

	return 0
End
```

### *See Also* {#see-also}
[Execute](/igorpro/commands/execute.md), [DoIgorMenu](/igorpro/commands/doigormenu.md)