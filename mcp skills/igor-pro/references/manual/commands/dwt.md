---
description: "The DWT operation performs discrete wavelet transform on the input wave srcWaveName."
slug: /commands/dwt
---

<div className="command-signature">

## <strong>DWT</strong>  [/I/S/D/P=<em>num</em>/T=<em>type</em> /N=<em>num</em> /V=<em>value</em>] <em>srcWaveName</em>, <em>destWaveName</em> {#dwt}

</div>

The DWT operation performs discrete wavelet transform on the input wave *srcWaveName*.  The operation works on one or more dimensions only as long as the number of elements in each dimension is a power of 2 or when  the /P flag is specified.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | Denoises the source wave. Performs the specified wavelet transform in the forward direction. It then zeros all transform coefficients whose magnitude fall below *value* % of the maximum magnitude of the transform (*value*  specified by the /V flag). It then performs the inverse transform placing the result in *destWaveName*. The /I flag is incompatible with the /D flag. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWaveName* as a free wave. |
|  | /FREE is allowed only in functions and only if *destWaveName* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/I</span> | Perform the inverse wavelet transform. The /S and /D flags are incompatible with the /I flag. |
| <span class="table-cell-nowrap">/N = *num*</span> | Specifies the number of wavelet coefficients. See the table in the ***Details*** section for supported combinations. |
| /P=*num* |<table class="nested-table"><tbody><tr><td>*num*&nbsp;=1:</td><td>Adds zero padding to the end of the dimension up to nearest power of 2 when the number of data elements in a given dimension of *srcWaveName* is not a power of 2.</td></tr><tr><td>*num*&nbsp;=2:</td><td>Uses zero padding to compute the transform, but the resulting wave is truncated to the length of the input wave</td></tr></tbody></table>
| <span class="table-cell-nowrap">/S</span> | Smooths the source wave. This performs the specified wavelet transform in the forward direction. It then zeros all transform coefficients except those between 0 and the cut-off value (specified in % by /V flag). It then performs the inverse transform placing the result in *destWaveName*. The /I flag is incompatible with the /S flag. |
| <span class="table-cell-nowrap">/T = *type*</span> | Performs the wavelet transform specified by *type*. See the table in the ***Details*** section for the transform name associated with each *type* code for the transform and the allowed values of the *num* parameter used with the /N flag. "NA" means that the /N flag is not applicable to the corresponding transform. |
| <span class="table-cell-nowrap">/V = *value*</span> | Specifies the degree of smoothing with the /S and /D flags only. For /S, *value* gives the cutoff as % of data points above which coefficients are set to zero. For /D, *value* specifies the percentage of the maximum magnitude of the transform such that coefficients smaller than this value are set to zero. |

### *Details* {#details}

When using the /T or /N flags, the following combinations of *type* and *num* are permitted for the given transform:

| Transform | /T=*type* | /N=*num* |
| --- | --- | --- |
| Daubechies | 1 (default) | 4,6,8,10,12,20 |
| Haar | 2 | NA |
| Battle-Lemarie | 4 | NA |
| Burt-Adelson | 8 | NA |
| Coifman | 16 | 2, 4, 6 |
| Pseudo-Coifman | 32 | NA |
| Splines | 64 | 1 (2-2), 2 (2-4), |
|  |  | 3 (3-3), 4 (3-7) |

If *destWaveName*  exists, DWT overwrites it; if it does not exist, DWT creates it.

When used in a function, the DWT operation automatically creates a wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details.

If *destWaveName*  is not specified, the operation stores the results in W_DWT for 1D waves and M_DWT for higher dimensions.

When working with 1D waves, the transform results are packed such that the higher half of each array contains the detail components and the lower half contains the smooth components and each successive scale is packed in the lower elements.  For example, if the source wave contains 128 points then the lowest scale results are stored in elements 64-127, the next scale (power of 2) are stored from 32-63, the following scale from 16-31 etc.

### *Examples* {#examples}

```igor
Make/O/N=1024 testData=sin(x/100)+gnoise(0.05)
DWT /S/N=20/V=25 testData, smoothedData
```

### *See Also* {#see-also}
For continuous wavelet transforms use the [CWT](/igorpro/commands/cwt.md) operation. The [FFT](/igorpro/commands/fft.md) operation.

### *Demos* {#demos}
[Open Wavelet Demo 2.0.pxp](#igor-pxp/Examples/Analysis/Wavelet__Demo__2.0.pxp)