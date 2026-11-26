---
description: "The gcd function calculates the greatest common divisor of A and B. Both A and B are assumed to be integers."
slug: /commands/gcd
---

<div className="command-signature">

## <strong>gcd</strong> (<em>A</em>, <em>B</em>) {#gcd}

</div>

The gcd function calculates the greatest common divisor of *A* and *B*.  Both *A* and *B* are assumed to be integers.

### *Examples* {#examples}

```igor
// Compute least common multiple.
Function LCM(a,b)
	Variable a, b
	return((a*b)/gcd(a,b))
End
```

### *See Also* {#see-also}
[PrimeFactors](/igorpro/commands/primefactors.md), [RatioFromNumber](/igorpro/commands/ratiofromnumber.md)