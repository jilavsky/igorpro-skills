---
description: "The ExecuteScriptText operation passes your text for compilation and execution to the Windows command line."
slug: /commands/executescripttext
---

<div className="command-signature">

## <strong>ExecuteScriptText</strong>  [/B /W=<em>waitTime</em> /UNQ /Z] <em>textStr</em> {#executescripttext}

</div>

The ExecuteScriptText operation passes your text for compilation and execution to the Windows command line.

Text produced by the script, including error messages, is returned in the string output variable S_value. S_value is set only if you include the /B (execute in background) flag.

### *Parameters* {#parameters}
*textStr*  must contain a valid Windows command line.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Execute the script in the background, i.e., leaving Igor as the active application. |
|  | If you omit /B, the program invoked by the script becomes the active program. If you include /B, Igor remains the active program. |
| <span class="table-cell-nowrap">/W = *waitTime*</span> | *waitTime* is the maximum time in seconds to wait before ExecuteScriptText returns. |
| <span class="table-cell-nowrap">/UNQ</span> | This flag has no effect. |
|  | The /UNQ flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/Z</span> | Include /Z if you want to handle errors in your code. Omit it if you want ExecuteScriptText to report errors to Igor. See ***ExecuteScriptText Error Handling*** below for details. |

### *ExecuteScriptText Error Handling* {#executescripttext-error-handling}
If you omit the /Z flag, if the script returns an error, ExecuteScriptText returns the error to Igor and procedure execution stops.

If you include the /Z flag then ExecuteScriptText sets the V_flag output variable to a nonzero value if the script returned an error or to zero if no error occurred. ExecuteScriptText does not report the error to Igor so procedure execution continues.

### *ExecuteScriptText* {#executescripttext-executescripttext}
*textStr* contains the full path to a batch file or the name of an executable file with optional Windows-style path and optional arguments:


```igor
[path]executableName  [.exe]  [arg1 ]...
```

If you omit *path* and *executableName*  ends with ".exe" or with no extension, Igor locates the executable by searching first the registry and then along the PATH environment variable. If not found, then the Igor Pro Folder directory is assumed. Here is an example of a command consisting of just the name of an executable:


```igor
ExecuteScriptText "calc" // calc.exe, calculator
```

When calling a batch file or other non-*.exe file, supply the full path. If the path (or file name) contains spaces, you must quote the path:


```igor
ExecuteScriptText "\"C:\\Program Files\\my.bat\""
```

The outer double-quotes are consumed by ExecuteScriptText. The inner double quotes, represented by the \\" escape sequence, remain in the command passed to the operating system.

Use the /B flag to run the command in the background, keeping Igor as the active application. Omit /B to allow the program launched by the command to become the active program. When executing a batch file, /B prevents the DOS window from appearing.

If you include /B, output from the command is returned via the S_value output string variable. If you omit /B, S_value is set to "".

The /W=*waitTime* flag provides a way to time out if a command takes too long. It is useful when calling non-GUI programs only. For GUI programs, ExecuteScriptText returns as soon as the GUI program starts processing events, regardless of the value specified for *waitTime*.

For non-GUI programs, if you specify a positive value for *waitTime*, ExecuteScriptText waits up to that many seconds for the command to complete. If the command fails to complete within that period of time, ExecuteScriptText returns an error. If you omit the /W flag or if you pass zero for *waitTime*, ExecuteScriptText waits until the command completes no matter how long it takes. If the script being executed creates a Windows command window, via cmd.exe for example, the Windows process completes only when the command window closes, not after the script commands execute.

### *Examples* {#examples}

```igor
// Execute a DOS command in the background
ExecuteScriptText/B "hostname"; Print S_value

// Open MatLab in background
ExecuteScriptText/B "C:\\Matlab\\bin\\matlab.exe myFile.m"

// Pass a script to Windows Script Host
ExecuteScriptText/W=5 "WScript.exe \"C:\\Test Script.vbs\""

// Execute a batch file and leave the command window open
ExecuteScriptText "cmd.exe /K \"C:\\mybatch.bat\""

// Execute a DOS command and get output, if any
// ExecuteDOSCommand(command, maxSecondsToWait)
// Executes a DOS command and returns any output text as the function result.
// Returns "" if the DOS command returns no text.
// maxSecondsToWait is the maximum number of seconds to wait for DOS to finish
// the command. If it takes longer than that, an error is generated.
// This function creates files in the Igor Pro User Folder:
//		IgorBatch.bat	Holds command that DOS is to execute
//		IgorBatchOutput.txt	Holds output generated by DOS command, if any
// Example:
//		Print ExecuteDOSCommand("echo %PATH%", 3)
Function/S ExecuteDOSCommand(command, maxSecondsToWait)
	String command	// e.g., "echo %PATH%"
	Variable maxSecondsToWait	// Error if DOS takes longer than this
	
	String quoteStr = "\""
	
	// Get path to batch file in "Igor Pro User Files"
	String dirPath = SpecialDirPath("Igor Pro User Files", 0, 0, 0)
	dirPath = ParseFilePath(5, dirPath, "\\", 0, 0)	// Convert to Windows path
	String batchFilePath = dirPath + "IgorBatch.bat"
	String batchOutputFilePath = dirPath + "IgorBatchOutput.txt"
	
	DeleteFile/Z batchOutputFilePath

	// Write DOS command to batch file
	String dosCommand = command + " > " + quoteStr + batchOutputFilePath + quoteStr
	Variable refNum
	Open refNum as batchFilePath
	FBinWrite refNum, dosCommand
	Close refNum
	
	// Execute batch file
	// The DOS command must complete in the number of seconds specified via /W
	// /C means cmd.exe quits after executing the command
	String text
	sprintf text, "cmd.exe /C \"%s\"", batchFilePath
	ExecuteScriptText/W=(maxSecondsToWait) text
	
	// Get output
	String result = ""
	Open/R/Z refNum as batchOutputFilePath
	if (V_flag != 0)
		result = ""
		// result = "<No output was generated by batch file>"	// For debugging
	else
		// Read contents of batch file into string
		FStatus refNum
		Variable numBytesInFile = V_logEOF
		result = PadString("", numBytesInFile, 0x20)
		FBinRead refNum, result
		Close refNum
	endif
	
	return result
End
```