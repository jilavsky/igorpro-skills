---
description: "The FMaxFlat operation calculates the coefficients of Kaiser's maximally flat filter."
slug: /commands/fmaxflat
---

<div className="command-signature">

## <strong>FMaxFlat</strong>  [/SYM[=<em>sym</em>] /Z[=<em>z</em>] ] <em>beta</em>, <em>gamma</em>, <em>coefsWave</em> {#fmaxflat}

</div>

The FMaxFlat operation calculates the coefficients of Kaiser's maximally flat filter.

FMaxFlat is primarily used for the Kaiser maximally flat filter feature of the [Igor Filter Design Laboratory (IFDL)](/igorpro/analysis/igor-filter-design-laboratory.md) package.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/SYM[ = *sym*]</span> | Return symmetrical FIR filter coefficients without a leading length point (see ***Details***). The /SYM flag was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">/Z[ = *z*]</span> | Prevents procedure execution from aborting if FMaxFlat generates an error. The /Z flag was added in Igor Pro 8.00. |
|  | V_Flag is set to a non-zero error code or zero if no error occurred. |
|  | Use /Z or the equivalent, /Z=1, if you want to handle errors in your procedures rather than having execution abort. Unlike some other operations /Z does suppress invalid *beta* and *gamma* value parameter errors. |

### *Parameters* {#parameters}
*beta* is the transition frequency ("cutoff") expressed as a fraction of the sampling frequency, more than 0 and less than 0.5.

*gamma* is the transition width in fraction of sampling frequency, a number more than 0 and less than 0.5, and less than both *beta*\*2 and 1-2\**beta*.

*coefsWave* is the 1D single- or double-precision floating point wave that receives the resulting coefficients. In Igor 8 or later, FMaxFlat resizes *coefsWave* as necessary to fit the number of returned values. The upper bound on the number of coefficients can be computed as: 

```igor
ceil(5/16/gamma/gamma)+1
```

### *Details* {#details}
The operation is based on the "mxflat" program as found in Elliot and Kaiser (see references below).

Use the /SYM flag to return a *coefsWave* with symmetrical coefficients suitable for use with [FilterFIR](/igorpro/commands/filterfir.md), in which case the number of points in *coefsWave* identifies the number of filter coefficients.

If you omit /SYM or specify /SYM=0, only half of the coefficients are computed by FMaxFlat. The rest can be obtained by symmetry, but the first point of *coefsWave* contains the number of computed coefficients in the designed filter. This unusual format is compatible with pre-Igor 8 IFDL procedures.

### *Example* {#example}

```igor
// Make a maximally-flat low pass filter with cutoff at 1/4 sampling frequency
Make/O/D/N=0 coefs                                  // coefs will be resized
FMaxFlat/SYM 0.25, 0.05, coefs                      // Make symmetrical FIR filter
Display coefs

// Analyze the filter's frequency response
FFT/OUT=3/PAD={256}/DEST=coefs_FFT coefs
Display coefs_FFT                                   // Filter response for 1Hz sample rate

// Make sample data: a sweep from 0 to 20500 Hz
Make/O/N=1000 data= sin(p*p/1000*pi/2)              // 0 to fs/2
SetScale/P x, 0, 1/41000, "s" data                  // 41000 Hz sample rate
Display data

// Analyse unfiltered data's frequency content
FFT/OUT=3/PAD={1000}/DEST=data_FFT  data            // Data frequency response
Display data_FFT

// Apply filter to copy of data
Duplicate/O data, filtered; DelayUpdate
FilterFIR/DIM=0/COEF=coefs filtered
Display filtered

// Analyse filtered data's frequency content
FFT/OUT=3/PAD={1000}/DEST=filtered_FFT  filtered    // Filtered data frequency response
Display filtered_FFT
TileWindows/O=1                                     // Tile Graphs
```

### *References* {#references}
Elliot, Douglas F.,contributing editor, *Handbook of Digital Signal Processing Engineering Applications*, Academic Press, San Diego, CA, 1987.

Kaiser, J.F., *Design subroutine (MXFLAT) for symmetric FIR low pass digital filters with maximally flat pass and stop bands*.

IEEE Digital Signal Processing Committee, Editor, *Programs for Digital Signal Processing*, IEEE Press, New York, 1979.

### *See Also* {#see-also}
[Remez](/igorpro/commands/remez.md), [FilterFIR](/igorpro/commands/filterfir.md), [Igor Filter Design Laboratory (IFDL)](/igorpro/analysis/igor-filter-design-laboratory.md)