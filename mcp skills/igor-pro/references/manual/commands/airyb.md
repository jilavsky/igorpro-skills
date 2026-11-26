---
description: "The airyB function returns the value of the Airy Bi (x) function: $$ \\displaystyle B i(x)=\\sqrt{\\frac{x}{3}}\\left[I_{-1 / 3}\\left(\\frac{2}{3} x^{3 /…"
slug: /commands/airyb
---

<div className="command-signature">

## <strong>airyB</strong> (<em>x</em> [, <em>accuracy</em> ]) {#airyb}

</div>

The airyB function returns the value of the Airy *Bi* (*x* ) function:

$$
\displaystyle B i(x)=\sqrt{\frac{x}{3}}\left[I_{-1 / 3}\left(\frac{2}{3} x^{3 / 2}\right)+I_{1 / 3}\left(\frac{2}{3} x^{3 / 2}\right)\right],
$$

where *I* is the modified Bessel function.

### *Details* {#details}
See the [bessI](/igorpro/commands/bessi.md) function for details on accuracy and speed of execution.

### *See Also* {#see-also}
[airyBD](/igorpro/commands/airybd.md), [airyA](/igorpro/commands/airya.md)

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", 446 pp., Dover, New York, 1972.