---
description: "The cequal function determines the equality of two complex numbers z1 and z2. It returns 1 if they are equal, or 0 if not."
slug: /commands/cequal
---

<div className="command-signature">

## <strong>cequal</strong> (<em>z1</em>, <em>z2</em>) {#cequal}

</div>

The cequal function determines the equality of two complex numbers *z1* and *z2*. It returns 1 if they are equal, or 0 if not.

This is in contrast to the == operator, which compares only the real components of z1 and z2, ignoring the imaginary components.

### *Examples* {#examples}

```igor
Function TestComplexEqualities()
	Variable/C z1= cmplx(1,2), z2= cmplx(1,-2)

	// This test compares only the real parts of z1 and z2:
	if( z1 == z2 )
		Print "== match"
	else
		Print "no == match"
	endif

	// This test compares both real and imaginary parts of z1 and z2:
	if( cequal(z1,z2) )
		Print "cequal match"
	else
		Print "no cequal match"
	endif
End
```

```
TestComplexEqualities()
  == match
  no cequal match
```

### *See Also* {#see-also}
[imag](/igorpro/commands/imag.md), [real](/igorpro/commands/real.md), [cmplx](/igorpro/commands/cmplx.md)