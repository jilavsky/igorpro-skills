---
description: "The NameOfWave function returns a string containing the name of the specified wave."
slug: /commands/nameofwave
---

<div className="command-signature">

## <strong>NameOfWave</strong> (<em>wave</em>) {#nameofwave}

</div>

The NameOfWave function returns a string containing the name of the specified wave.

In a user-defined function that has a parameter or local variable of type WAVE, NameOfWave returns the actual name of the wave identified by the WAVE reference. It can also be used with wave reference functions such as [WaveRefIndexedDFR](/igorpro/commands/waverefindexeddfr.md).

NameOfWave does not return the full data folder path to the wave. Use [GetWavesDataFolder](/igorpro/commands/getwavesdatafolder.md) for this information.

A null wave reference returns a zero-length string. This might be encountered, for instance, when using WaveRefIndexedDFR in a loop to act on all waves in a data folder, and the loop has incremented beyond the highest valid index.

### *Examples* {#examples}

```igor
Function ZeroWave(w)
	Wave w
	w = 0
	Print "Zeroed the contents of", NameOfWave(w)
End
```

The following results in a blank line printed in the history:


```igor
print NameOfWave($"")
```