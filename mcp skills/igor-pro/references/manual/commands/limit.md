---
description: "The limit function returns num, limited to the range from low to high."
slug: /commands/limit
---

<div className="command-signature">

## <strong>limit</strong> (<em>num</em>, <em>low</em>, <em>high</em>) {#limit}

</div>

The limit function returns *num*, limited to the range from *low* to *high* :

*num* if *low* <= *num* <= *high*

*low* if *num* < *low*

*high* if *num* > *high*

### *Details* {#details}
Since all comparisons with NaN return false, limit will not work as expected with NaNs. If a parameter may be NaN, use [numtype](/igorpro/commands/numtype.md) to test it before calling limit.

### *See Also* {#see-also}
[SelectNumber](/igorpro/commands/selectnumber.md), [min](/igorpro/commands/min.md), [max](/igorpro/commands/max.md)