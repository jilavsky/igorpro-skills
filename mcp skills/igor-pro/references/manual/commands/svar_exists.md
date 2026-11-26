---
description: "The SVAR_Exists function returns 1 if the specified SVAR reference is valid or 0 if not. It can be used only in user-defined functions."
slug: /commands/svar_exists
---

<div className="command-signature">

## <strong>SVAR_Exists</strong> (<em>name</em>) {#svar_exists}

</div>

The SVAR_Exists function returns 1 if the specified SVAR reference is valid or 0 if not. It can be used only in user-defined functions.

For example, in a user function you can test if a global string variable exists like this:


```igor
SVAR /Z str1 = gStr1    // /Z prevents debugger from flagging bad SVAR
if (!SVAR_Exists(str1)) // No such global string variable?
    String/G gStr1 = "" // Create and initialize it
endif
```

### *See Also* {#see-also}
[WaveExists](/igorpro/commands/waveexists.md), [NVAR_Exists](/igorpro/commands/nvar_exists.md), [Accessing Global Variables and Waves](/igorpro/programming/programming.md#accessing-global-variables-and-waves)