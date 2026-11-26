---
description: "SmoothCustom is obsolete. Use the FilterFIR operation instead. For multidimensional applications use the MatrixConvolve or MatrixFilter operations."
slug: /commands/smoothcustom
---

<div className="command-signature">

## <strong>SmoothCustom</strong>  [/E=<em>endEffect</em>] <em>coefsWaveName</em>, <em>waveName</em> [, <em>waveName</em> ]... {#smoothcustom}

</div>

:::note
SmoothCustom is obsolete. Use the FilterFIR operation instead. For multidimensional applications use the MatrixConvolve or MatrixFilter operations.
:::

The SmoothCustom operation smooths the named waves by convolving them with coefsWaveName.

### *Parameters* {#parameters}
*coefsWaveName* must be single or double floating point, must not be one of the destination *waveName*s, must not be complex.

*waveName* is a numeric destination wave that is overwritten by the convolution of itself and *coefsWaveName*.

### *Flags* {#flags}
/E=*endEffect*	End effect method, a value between 0 and 3.

### *Details* {#details}
The convolution is performed in the time-domain. That is, the FFT is not employed. For this reason the length of *coefsWaveName* should be small or small in comparison to the destination waves.

SmoothCustom presumes that the middle point of *coefsWaveName* corresponds to the delay = 0 point. The "middle" point number = trunc(numpnts(*coefsWaveName* -1)/2). *coefsWaveName* usually contains the two-sided impulse response of a filter, and contains an odd number of points. This is the type of wave created by [FilterFIR](/igorpro/commands/filterfir.md).

SmoothCustom ignores the X scaling of all the waves.

The SmoothCustom operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.