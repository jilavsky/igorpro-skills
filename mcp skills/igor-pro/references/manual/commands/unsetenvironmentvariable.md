---
description: "The UnsetEnvironmentVariable function deletes the variable named varName from the environment of Igor's process, if it exists."
slug: /commands/unsetenvironmentvariable
---

<div className="command-signature">

## <strong>UnsetEnvironmentVariable</strong> (<em>varName</em>) {#unsetenvironmentvariable}

</div>

The UnsetEnvironmentVariable function deletes the variable named *varName*  from the environment of Igor's process, if it exists

The function returns 0 if it succeeds or a nonzero value if it fails.

The UnsetEnvironmentVariable function was added in Igor Pro 7.00.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *varName* | The name of an environment variable which does not need to actually exist. It must not be an empty string and may not contain an equals sign (=). |

### *Details* {#details}
The environment of Igor's process is composed of a set of key=value pairs that are known as environment variables.

The environment of Igor's process is composed of a set of key=value pairs that are known as environment variables. Any child process created by calling [ExecuteScriptText](/igorpro/commands/executescripttext.md) inherits the environment variables of Igor's process.

UnsetEnvironmentVariable changes the environment variables present in Igor's process and any future process created by ExecuteScriptText but does not affect any other processes already created.

On Windows, environment variable names are case-insensitive. On other platforms, they are case-sensitive.

### *Examples* {#examples}

```igor
Variable result
result = SetEnvironmentVariable("SOME_VARIABLE", "15")  // Sets the variable
result = UnsetEnvironmentVariable("SOME_VARIABLE")      // Unsets the variable
```

### *See Also* {#see-also}
[GetEnvironmentVariable](/igorpro/commands/getenvironmentvariable.md), [SetEnvironmentVariable](/igorpro/commands/setenvironmentvariable.md)