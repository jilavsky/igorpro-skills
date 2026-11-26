---
description: "The NVAR_Exists function returns one if specified NVAR reference is valid or zero if not. It can be used only in user-defined functions."
slug: /commands/nvar_exists
---

<div className="command-signature">

## <strong>NVAR_Exists</strong> (<em>name</em>) {#nvar_exists}

</div>

The NVAR_Exists function returns one if specified NVAR reference is valid or zero if not. It can be used only in user-defined functions.

For example, in a user function you can test if a global numeric variable exists like this:


```igor
NVAR /Z var1 = gVar1        // /Z prevents debugger from flagging bad NVAR
if (!NVAR_Exists(var1))     // No such global numeric variable?
    Variable/G gVar1 = 0    // Create and initialize it
endif
```

will print 1 if MyGlobalVar is present in the current data folder.

### *See Also* {#see-also}
[WaveExists](/igorpro/commands/waveexists.md), [SVAR_Exists](/igorpro/commands/svar_exists.md), [Accessing Global Variables and Waves](/igorpro/programming/programming.md#accessing-global-variables-and-waves)