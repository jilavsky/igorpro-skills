---
description: "Faddeeva computes the Faddeeva function, also commonly denoted as \"w\", using an approximation that has an accuracy, as described by the author, of \"typically…"
slug: /commands/faddeeva
---

<div className="command-signature">

## <strong>Faddeeva</strong> (<em>z</em>) {#faddeeva}

</div>

Faddeeva computes the Faddeeva function, also commonly denoted as "w", using an approximation that has an accuracy, as described by the author, of "typically at least 13 significant digits". Both the input and the output are complex numbers.

The Faddeeva function was added in Igor Pro 8.00.

The Faddeeva function is the basis of the Voigt function, implemented in Igor as [VoigtFunc](/igorpro/commands/voigtfunc.md).

```igor
VoigtFunc(X, Y) = real(Faddeeva(cmplx(X, Y)).
```

### *References* {#references}
The code used to compute the VoigtFunc was written by Steven G. Johnson of MIT. You can learn more about it at [http://ab-initio.mit.edu/Faddeeva](http://ab-initio.mit.edu/Faddeeva).

### *See Also* {#see-also}
[VoigtPeak](/igorpro/commands/voigtpeak.md), [VoigtFunc](/igorpro/commands/voigtfunc.md), [Built-in Curve Fitting Functions](/igorpro/analysis/curve-fitting.md#built-in-curve-fitting-functions)