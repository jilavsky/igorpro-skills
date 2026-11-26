---
description: "The sawtooth function returns ((num +n2π) mod 2π)/2π where n is used to correct if num is negative."
slug: /commands/sawtooth
---

<div className="command-signature">

## <strong>sawtooth</strong> (<em>num</em>) {#sawtooth}

</div>

The sawtooth function returns ((*num* +n2π) mod 2π)/2π where n is used to correct if *num* is negative. Sawtooth is used to create arbitrary periodic waveforms analogous to sine and cosine.

### *Examples* {#examples}

```igor
wave1 = sawtooth(x)
```

creates a sawtooth in wave1 whose Y values range from 0 to 1 as its X values go through 2π units.


```igor
wave1 = exp(sawtooth(x))
```

creates a series of exponentials in wave1 of amplitude exp(1) and period 2π.

You can also use sawtooth to create periodic repetitions of a given part of a wave:


```igor
wave1 = wave2(sawtooth(x))
```

creates a periodic repetition of wave2 in wave1 given the appropriate X scaling for the waves.