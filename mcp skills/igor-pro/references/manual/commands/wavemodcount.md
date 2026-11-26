---
description: "The WaveModCount function returns a value that can be used to tell if a global wave has been changed between one call to WaveModCount and another."
slug: /commands/wavemodcount
---

<div className="command-signature">

## <strong>WaveModCount</strong> (<em>wave</em>) {#wavemodcount}

</div>

The WaveModCount function returns a value that can be used to tell if a global wave has been changed between one call to WaveModCount and another.

WaveModCount was added in Igor Pro 8.00.

The exact value returned by WaveModCount has no significance. The only use for it is to compare the values returned by two calls to WaveModCount. If they are the different, the wave was changed in the interim.

The wave mod count for free and thread-local waves is undefined, so WaveModCount should only be used with global waves in the data hierarchy of the main thread.

A wave's mod count changes when the wave's data or properties, such as scaling, note, and dimensionality, are set. The mod count changes even if the new data or property values are the same as the old. For example, executing:


```igor
wave1 += 0
```

causes the mod count to change even though the data itself was not actually changed.

### *Examples* {#examples}

```igor
Make/O wave1 = 5
Variable waveModCount1, waveModCount2
waveModCount1 = WaveModCount(wave1);
wave1 += 1				// Modify wave1
waveModCount2 = WaveModCount(wave1);
if (waveModCount2 != waveModCount1)
	Print "Wave has changed"
endif
```

### *See Also* {#see-also}
[WaveInfo](/igorpro/commands/waveinfo.md), [ModDate](/igorpro/commands/moddate.md)