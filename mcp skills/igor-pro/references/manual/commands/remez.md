---
description: "The Remez operation calculates the coefficients for digital filters given a desired frequency response as input."
slug: /commands/remez
---

<div className="command-signature">

## <strong>Remez</strong>  [/N=<em>num</em> /Q[=<em>iter</em>] ] <em>frWave</em>, <em>wtWave</em>, <em>gridWave</em>, <em>coefsWave</em> {#remez}

</div>

The Remez operation calculates the coefficients for digital filters given a desired frequency response as input.

Remez is primarily used for the MPR filter feature of the [Igor Filter Design Laboratory (IFDL)](/igorpro/analysis/igor-filter-design-laboratory.md) package.

### *Parameters* {#parameters}
*frWave* contains the desired response.

*wtWave* contains the weight function array. For a differentiator, the weight function is inversely proportional to frequency.

*gridWave* contains the frequencies corresponding to each point in *frWave* and *wtWave*. Its values range from 0 to 0.5 with gaps where the band edges occur.

*coefsWave* receives the resulting coefficients. Its length defines the number of coefficients (nfilt in the IEEE program referenced below).

### *Flags* {#flags}

|  |  |
| --- | --- |
| /N=*mode* |<table class="nested-table"><tbody><tr><td>*mode*=0:</td><td>Selects multiple passband/stopband filter (default).</td></tr><tr><td>*mode*=1:</td><td>Selects differentiator or Hilbert transform filter.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Q[ = *iter*]</span> | Determines if execution stops if the filter doesn't converge. |
|  | If you omit /Q, execution stops if the filter doesn't converge. |
|  | If you specify /Q or /Q=0, execution continues if the filter doesn't converge, regardless of the number of iterations. |
|  | For *iter*>=1, execution stops if the filter fails to converge in *iter*  iterations or less. If the filter does converge after *iter*  iterations, execution does stop. |
|  | Use /Q=3 to stop execution for serious errors (after only 1, 2, or 3 iterations) but not for minor errors (after 4 or more iterations). |

### *Details* {#details}
Remez returns symmetrical coefficients suitable for use with [FilterFIR](/igorpro/commands/filterfir.md) in *coefsWave*.

The algorithm is based upon the McClellan-Parks-Rabiner Fortran program as found in the IEEE and Elliot references cited below.

If the filter converged, Remez sets V_Flag to 0. Otherwise it sets it to the number of iterations before it failed.

### *Example* {#example}
This example specifies a length 41 lowpass filter with passband 0 to 0.14 x f<sub>s</sub> and stopband 0.18 x f<sub>s</sub> to 0.5 x f<sub>s</sub>.  The passband weight is equal to the stopband weight.


```igor
Make/O/N=41 coefs = NaN
Make/O/N=(41*16) fr, wt, grid
grid = 0.5*p/numpnts(grid)      // Frequencies where fr and wt define desire response
wt = 1
fr[0,0.14*numpnts(fr)] = 1      // Low pass from 0 to 0.14 x fs

// Remove transition frequencies
DeletePoints 0.14*numpnts(fr), 0.04*numpnts(fr), fr, wt, grid

// Compute filter coefs
Remez fr, wt, grid, coefs

// Analyze the filter's frequency response
FFT/OUT=3/PAD={256}/DEST=coefs_FFT coefs

// Display filter response for 1Hz sample rate
Display coefs_FFT
```

### *References* {#references}
J. H. McClellan, T.W. Parks, and L. R. Rabiner, *A computer program for designing optimum FIR linear phase digital filters*.  IEEE Transactions on Audio and Electroacoustics, AU-21, 506-526 (December 1973).

L. R. Rabiner, J. H. McClellan, and T.W. Parks, *FIR digital filter design techniques using weighted Chebyschev approximation*, Proc. IEEE 63, 595-610 (April 1975)

Elliot, Douglas F.,contributing editor, *Handbook of Digital Signal Processing Engineering Application*s, Academic Press, San Diego, CA, 1987.

IEEE Digital Signal Processing Committee, Editor, *Programs for Digital Signal Processing*, IEEE Press, New York, 1979 .

### *See Also* {#see-also}
[FMaxFlat](/igorpro/commands/fmaxflat.md), [FilterFIR](/igorpro/commands/filterfir.md), [Igor Filter Design Laboratory (IFDL)](/igorpro/analysis/igor-filter-design-laboratory.md)