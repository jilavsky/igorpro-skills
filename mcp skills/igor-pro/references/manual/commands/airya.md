---
description: "The airyA function returns the value of the Airy Ai (x) function: $$ \\displaystyle \\operatorname{Ai}(x)=\\frac{1}{\\pi} \\sqrt{\\frac{x}{3}} K_{1 /…"
slug: /commands/airya
---

<div className="command-signature">

## <strong>airyA</strong> (<em>x</em> [, <em>accuracy</em> ]) {#airya}

</div>

The airyA function returns the value of the Airy *Ai* (*x* ) function:

$$
\displaystyle \operatorname{Ai}(x)=\frac{1}{\pi} \sqrt{\frac{x}{3}} K_{1 / 3}\left(\frac{2}{3} x^{3 / 2}\right),
$$

where *K* is the modified Bessel function.

### *Details* {#details}
See the [bessI](/igorpro/commands/bessi.md) function for details on accuracy and speed of execution.

### *See Also* {#see-also}
[airyAD](/igorpro/commands/airyad.md), [airyB](/igorpro/commands/airyb.md)

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", 446 pp., Dover, New York, 1972.