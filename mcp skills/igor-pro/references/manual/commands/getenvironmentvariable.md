---
description: "The GetEnvironmentVariable function returns a string containing the current value of the specified environment variable for the currently running Igor process."
slug: /commands/getenvironmentvariable
---

<div className="command-signature">

## <strong>GetEnvironmentVariable</strong> (<em>varName</em>) {#getenvironmentvariable}

</div>

The GetEnvironmentVariable function returns a string containing the current value of the specified environment variable for the currently running Igor process. If the variable does not exist, an empty string ("") is returned.

The GetEnvironmentVariable function was added in Igor Pro 7.00.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| var*Name* | The name of an environment variable which may or may not exist. It must not be an empty string and may not contain an equals sign (=). |
|  | As a special case, if a single equals sign ("=") is passed for *varName*, a carriage return (\\r) separated list of all current key=value environment variable pairs is returned. |

### *Details* {#details}
The environment of Igor's process is composed of a set of key=value pairs that are known as environment variables. Any child process created by calling [ExecuteScriptText](/igorpro/commands/executescripttext.md) inherits the environment variables of Igor's process.

On Windows, environment variable names are case-insensitive. On other platforms, they are case-sensitive.

GetEnvironmentVariable returns an empty string if *varName* does not exist or if it does exist but its value is empty. If you need to know whether or not the environment variable itself actually exists, you can use the following function:


```igor
Function EnvironmentVariableExists(varName)
	String varName
	String varList = GetEnvironmentVariable("=")

	// Replace \r with \n because GrepString treats \n only as line separator, not \r.
	varList = ReplaceString("\r", varList, "\n")
	String regExp = "(?m)^" + varName + "="	// ?m means treat ^ as beginning of line, not entire string.
	return GrepString(varList, regExp)
End
```

### *Examples* {#examples}

```igor
String currentUser = GetEnvironmentVariable("USER")
String varList = GetEnvironmentVariable("=")
```

### *See Also* {#see-also}
[SetEnvironmentVariable](/igorpro/commands/setenvironmentvariable.md), [UnsetEnvironmentVariable](/igorpro/commands/unsetenvironmentvariable.md)