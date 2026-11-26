---
description: "The factorial function returns n!, where n is assumed to be a positive integer."
slug: /commands/factorial
---

<div className="command-signature">

## <strong>factorial</strong> (<em>n</em>) {#factorial}

</div>

The factorial function returns *n* !, where *n* is assumed to be a positive integer.

Note that while factorial is an integer-valued function, a double-precision number has 53 bits for the mantissa. This means that numbers over 2<sup>52</sup> will be accurate to about one part in about 2x10<sup>16</sup>. Values of *n* greater than 170 result in overflow and return the nonnumber Inf.