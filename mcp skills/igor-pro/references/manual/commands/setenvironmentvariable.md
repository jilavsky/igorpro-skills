---
description: "The SetEnvironmentVariable function creates an environment variable in Igor's process and sets its value to varValue."
slug: /commands/setenvironmentvariable
---

<div className="command-signature">

## <strong>SetEnvironmentVariable</strong> (<em>varName</em>, <em>varValue</em>) {#setenvironmentvariable}

</div>

The SetEnvironmentVariable function creates an environment variable in Igor's process and sets its value to *varValue*. If a variable named *varName* already exists, its value is set to *varValue*.

The function returns 0 if it succeeds or a nonzero value if it fails.

The SetEnvironmentVariable function was added in Igor Pro 7.00.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *varName* | The name of an environment variable which does not need to actually exist. It must not be an empty string and may not contain an equals sign (=). |
| *varValue* | The new contents for the variable. |
|  | On Windows, if *varValue* is an empty string, the variable is removed. On other platforms, the variable is always set to *varValue*. |

### *Details* {#details}
The environment of Igor's process is composed of a set of key=value pairs that are known as environment variables. Any child process created by calling [ExecuteScriptText](/igorpro/commands/executescripttext.md) inherits the environment variables of Igor's process.

SetEnvironmentVariable changes the environment variables present in Igor's process and any future process created by ExecuteScriptText but does not affect any other processes already created.

On Windows, environment variable names are case-insensitive. On other platforms, they are case-sensitive.

### *Examples* {#examples}

```igor
Variable result
result = SetEnvironmentVariable("SOME_VARIABLE", "15")
result = SetEnvironmentVariable("SOME_OTHER_VARIABLE", "string value")
```

### *See Also* {#see-also}
[GetEnvironmentVariable](/igorpro/commands/getenvironmentvariable.md), [UnsetEnvironmentVariable](/igorpro/commands/unsetenvironmentvariable.md)