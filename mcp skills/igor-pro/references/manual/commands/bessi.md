---
description: "Obsolete -- use Besseli. The bessI function returns the modified Bessel function of the first kind, In (x), of ordern and argument x."
slug: /commands/bessi
---

<div className="command-signature">

## <strong>bessI</strong> (<em>n</em>,<em>x</em> [, <em>algorithm</em>  [, <em>accuracy</em> ]]) {#bessi}

</div>

:::warning
Obsolete -- use [Besseli](/igorpro/commands/besseli.md).
:::

The bessI function returns the modified Bessel function of the first kind, I<sub>n </sub>(*x* ), of order*n* and argument *x*.

For real x, the optional parameter *algorithm* selects between a faster, less accurate calculation method and slower, more accurate methods. In addition, when *algorithm* is zero or absent, the order *n* is truncated to an integer.

When *algorithm* is included and is 1, *accuracy* can be used to specify the desired fractional accuracy. See below for details about algorithms.

if *x* is complex, a complex result is returned. In this case, *algorithm* and *accuracy* are ignored. The order *n* can be fractional, and must be real.

### *Details* {#details}
The *algorithm* parameter has three options, each selecting a different calculation method:


| Algorithm | What You Get |
| --- | --- |
| 0 (default) | Uses a calculation method that has fractional accuracy better than 10<sup>-</sup><sup>6</sup> everywhere and is generally better than 10<sup>-</sup><sup>8</sup>. This method does not handle fractional order *n*; the order is truncated to an integer before the calculation is performed. |
|  | Algorithm 0 is fastest by a large margin. |
| 1 | Fractional order is allowed. The calculation is performed using methods described in Numerical Recipes in C, edition 2, section 6.7 "Bessel Functions of Fractional Order", pp. 240-245. |
|  | Using algorithm 1, *accuracy* specifies the fractional accuracy that you desire. That is, if you set *accuracy* to 1e-7 (that is, 10<sup>-</sup><sup>7</sup>), that means that you wish that the absolute value of (f<sub>actual</sub>-f<sub>returned</sub>)/f<sub>actual</sub> be better than 10<sup>-</sup><sup>7</sup>. Asking for less accuracy gives some increase in speed. |
|  | You pay a heavy price for higher accuracy or fractional order. When *algorithm* is nonzero, calculation time is increased by an order of magnitude for small *x* ; at larger *x* the penalty is even greater. |
|  | If *accuracy* is greater than 10<sup>-</sup><sup>8</sup> and *n* is an integer, algorithm 0 is used. |
|  | The algorithm used calculates bessI and bessK simultaneously. Igor stores both values, and if a call to bessI is followed by a call to bessK (or bessK is followed by bessI) with the same *n*, *x*, and *accuracy* the previously-stored value is returned, making the second call very fast. |
| 2 | Fractional order is allowed. The calculation is performed using code from the SLATEC library. The accuracy achievable is often better than algorithm 1, but not always. Algorithm 2 is 1.5 to 3 times faster than algorithm 1, but still slower than algorithm 0. The *accuracy* parameter is ignored. |

The achievable accuracy of algorithms 1 and 2 is a complicated function *n* and *x*. To see a summary of accuracy achievable, pull down the File menu and select Example Experiments→Testing and Misc→Bessel Accuracy.