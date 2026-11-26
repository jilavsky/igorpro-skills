---
description: "The numtype function returns a number which indicates what kind of value num contains."
slug: /commands/numtype
---

<div className="command-signature">

## <strong>numtype</strong> (<em>num</em>) {#numtype}

</div>

The numtype function returns a number which indicates what kind of value *num* contains.

### *Details* {#details}
If *num* is a real number, numtype returns a real number whose value is:

0:	*num* contains a normal number.

1:	*num* contains +/-INF.

2:	*num* contains NaN.

If *num* is a complex number, numtype returns a complex number in which the real part is the number type of the real part of *num* and the imaginary part is the number type of the imaginary part of *num* .