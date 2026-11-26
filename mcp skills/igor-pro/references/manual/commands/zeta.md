---
description: "The zeta function returns the Hurwitz Zeta function for real or complex arguments a and b."
slug: /commands/zeta
---

<div className="command-signature">

## <strong>zeta</strong> (<em>a</em>, <em>b</em> [, <em>terms</em>]) {#zeta}

</div>

The zeta function returns the Hurwitz Zeta function for real or complex arguments *a* and *b*

$$
\begin{array}{l}
\zeta(a, b)=\displaystyle \sum_{k=0}^{\infty} \frac{1}{(k+b)^{a}}, \\
\\
\Re(a)>1, \\
\\
b \neq 0,-1,-2, \ldots
\end{array}
$$

The Riemann zeta function is the special case:

$$
\displaystyle \zeta(a)=\zeta(a, 1) .
$$

The zeta function was added in Igor Pro 7.00.

### *Parameters* {#parameters}
The *terms* parameter defaults to 40. In practice evaluation may terminate before the specified number of terms when convergence is achieved.

### *References* {#references}
Olver, Frank W. J.; Lozier, Daniel W.; Boisvert, Ronald F.; Clark, Charles W., eds., "NIST Handbook of Mathematical Functions", 607 pp., Cambridge University Press, 2010.

### *See Also* {#see-also}
[Dilogarithm](/igorpro/commands/dilogarithm.md)