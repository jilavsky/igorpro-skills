---
description: "The NaN function returns the \"Not a Number\" value, according to the IEEE standards."
slug: /commands/nan
---

<div className="command-signature">

## <strong>NaN</strong> {#nan}

</div>

The NaN function returns the "Not a Number" value, according to the IEEE standards.

Comparison operators do not work with NaN parameters because, by definition, NaN compared to anything, even another NaN, is false. Use [numtype](/igorpro/commands/numtype.md) to test if a value is NaN.