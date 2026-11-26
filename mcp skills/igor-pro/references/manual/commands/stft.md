---
description: "The STFT operation computes the Short-Time Fourier Transform of srcWave. STFT was added in Igor Pro 8.00."
slug: /commands/stft
---

<div className="command-signature">

## <strong>STFT</strong>  [<em>flags</em>] <em>srcWave</em> {#stft}

</div>

The STFT operation computes the Short-Time Fourier Transform of *srcWave*. STFT was added in Igor Pro 8.00.

Output is stored in the wave M_STFT in the current data folder or in a wave specified by the /DEST flag.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DB = *dbMode*</span> | *dbMode* determines if output is scaled in decibels: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>No dB scaling (default)</td></tr><tr><td>1:</td><td>Scale the output to standard dB using 20*log(wave)</td></tr><tr><td>2:</td><td>Compute dBFS (dB relative to full scale where 0 is the maximum value)</td></tr></tbody></table>
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the output wave created by the FFT operation. |
|  | It is an error to specify the same wave as both *srcWave* and *destWave*. |
|  | The default output wave name M_STFT is used if you omit /DEST. |
|  | When used in a function, the STFT operation by default creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/HOPS = *hopSize*</span> | Specifies the offset in points between centers of consecutive source segments. By default this value is 1 and the transform is computed for segments that are offset by a single points from each other. |
| /OUT=*mode* |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=1:</td><td>Default for complex output</td></tr><tr><td>*mode*&nbsp;=2:</td><td>Real output</td></tr><tr><td>*mode*&nbsp;=3:</td><td>Magnitude</td></tr><tr><td>*mode*&nbsp;=4:</td><td>Magnitude square</td></tr><tr><td>*mode*&nbsp;=5:</td><td>Phase</td></tr><tr><td>*mode*&nbsp;=6:</td><td>Scaled magnitude</td></tr><tr><td>*mode*&nbsp;=7:</td><td>Scaled magnitude squared</td></tr></tbody></table>
|  | The scaled quantities apply to transforms of real valued inputs where the output is normally folded in the first dimension (because of symmetry). The scaling applies a factor of 2 to the squared magnitude of all components except the DC. The scaled transforms should be used whenever Parseval's relation is expected to hold. |
| <span class="table-cell-nowrap">/PAD = *newSize*</span> | Converts each segment of *srcWave* into a padded array of length *newSize*. The padded array contains the original data at the center of the array with zeros elements on both sides. |
| <span class="table-cell-nowrap">/RP = [*startPoint*,*endPoint*]</span> |  |
|  | Specifies the range of *srcWave* from which data are sampled in point numbers. *startPoint* is the first point at which segments are centered. Wave data from points preceding *startPoint* are used as needed for the left parts of beginning segments. |
| <span class="table-cell-nowrap">/RX = (*startX*,*endX*)</span> |  |
|  | Specifies the range of *srcWave* from which data are sampled in X values. The operation expects *startX*<*endX*. *startX* corresponds to the first point at which segments are centered. Data from points preceding *startX* are used as necessary to fill left parts of the beginning segments. |
| <span class="table-cell-nowrap">/SEGS = *segSize*</span> | Sets the length of the segment sampled from *srcWave* in points. The segment is optionally padded to a larger dimension (see /PAD) and multiplied by a window function prior to FFT. The default segment size is 128 when the number of points in *srcWave* is greater than 128. Otherwise it is set to one less than the number of points in the *srcWave*. The operation requires that *segSize* is at least 32 points. |
| <span class="table-cell-nowrap">/WINF = *windowKind*</span> |  |
|  | Premultiplies a data seggment with the selected window function. The default window is Hanning. See ***Window Functions*** in the documentation for [FFT](/igorpro/commands/fft.md) for details. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag is set to -1 for any error and to zero otherwise. |

### *Details* {#details}
The Short-Time Fourier Transform is a time-frequency representation for a 1D array. The squared magnitude of the transform is known as the "spectrogram" for time series or "sonogram" in the case of sound input. The operation comprises the following steps:


1.	Sampling the data.

	A segment of size specified by /SEGS is sampled from *srcWave* centered about the first point in the wave or as specified by /RX or /RP flags. When the first point is at the beginning of the wave the centering implies that the first half of the segment is set to zero. If the first point is somewhere else the operation uses as many points as are available in the wave and sets the rest to zero. End effects are mitigated by scaling the result by a factor that accounts for the actual number of source data used in the segment. Subsequent segments are each centered at *hopSize* points from the previous center.


2.	Apply windowing.

	The selected segment is multiplied by the specified window function.


3.	Apply padding.

	If padding is specified the windowed data are centered onto a zero padded array. Padding may be used to simulate longer arrays for improved spectral resolution.


4.	Compute the FFT.

	Initial complex transform may be further processed according to the /OUT flag.

### *See Also* {#see-also}
[Fourier Transforms](/igorpro/analysis/signal-processing.md#fourier-transforms), [FFT](/igorpro/commands/fft.md), [CWT](/igorpro/commands/cwt.md), [WignerTransform](/igorpro/commands/wignertransform.md), [DSPPeriodogram](/igorpro/commands/dspperiodogram.md), [LombPeriodogram](/igorpro/commands/lombperiodogram.md).