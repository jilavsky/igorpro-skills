---
description: "The Unwrap operation scans through each named wave trying to undo the effect of a modulus operation."
slug: /commands/unwrap
---

<div className="command-signature">

## <strong>Unwrap</strong>  <em>modulus</em>, <em>waveName</em> [, <em>waveName</em> ]... {#unwrap}

</div>

The Unwrap operation scans through each named wave trying to undo the effect of a modulus operation.

### *Parameters* {#parameters}
*modulus*  is the value applied to the named waves through the mod function as if the command:


```igor
waveName = mod(waveName,modulus)
```

had been executed. It is this calculation which Unwrap attempts to undo.

### *Details* {#details}
The Unwrap operation works with 1D waves only.  See [ImageUnwrapPhase](/igorpro/commands/imageunwrapphase.md) for phase unwrapping in two dimensions..

### *Examples* {#examples}
If you perform an FFT on a wave, the result is a complex wave in rectangular coordinates. You can create a real wave which contains the phase of the result of the FFT with the command:


```igor
wave2 = imag(r2polar(wave1))
```

However the rectangular to polar conversion leaves the phase information modulo 2π. You can restore the phase information with the command:


```igor
Unwrap 2*pi, wave2
```

Because the first point of a wave that has been FFTed has no phase information, in this example you would *precede* the Unwrap command with the command:


```igor
wave2[0] = wave2[1]
```

### *See Also* {#see-also}
[mod](/igorpro/commands/mod.md), [ImageUnwrapPhase](/igorpro/commands/imageunwrapphase.md)


```igor
```