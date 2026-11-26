---
description: "The WaveExists function returns one if wave reference is valid, or zero if the wave reference is null. For example if, in a user function, you have."
slug: /commands/waveexists
---

<div className="command-signature">

## <strong>WaveExists</strong> (<em>wave</em>) {#waveexists}

</div>

The WaveExists function returns one if wave reference is valid, or zero if the wave reference is null. For example if, in a user function, you have:


```igor
Wave w= $"no such wave"
```

then WaveExists(w) will return zero.

### *Details* {#details}
If *wave* is not a valid wave reference, WaveExists also checks whether *wave* itself is the name of an existing wave when executing the function. WaveExists should be used in functions only. In a macro, use the [exists](/igorpro/commands/exists.md) function instead.

### *See Also* {#see-also}
[WAVE](/igorpro/programming/keywords/object-reference-keywords.md#wave), [Exists](/igorpro/commands/exists.md), [NVAR_Exists](/igorpro/commands/nvar_exists.md), [SVAR_Exists](/igorpro/commands/svar_exists.md), [Accessing Global Variables and Waves](/igorpro/programming/programming.md#accessing-global-variables-and-waves)