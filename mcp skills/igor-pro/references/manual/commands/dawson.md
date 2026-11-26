---
description: "The dawson function returns the value of the Dawson integral: $$ \\displaystyle F(x)=\\exp \\left(-x^{2}\\right) \\int_{0}^{x} \\exp \\left(t^{2}\\right) d t."
slug: /commands/dawson
---

<div className="command-signature">

## <strong>dawson</strong> (<em>x</em>) {#dawson}

</div>

The dawson function returns the value of the Dawson integral:

$$
\displaystyle F(x)=\exp \left(-x^{2}\right) \int_{0}^{x} \exp \left(t^{2}\right) d t .
$$

If x is real, dawson returns a real result. If x is complex, dawson returns a complex result.

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", 298 pp., Dover, New York, 1972.

The code used to compute the Dawson integral was written by Steven G. Johnson of MIT. See [http://ab-initio.mit.edu/Faddeeva](http://ab-initio.mit.edu/Faddeeva)