---
description: "The EstimatePeakSizes operation estimates the amplitudes and widths of peaks whose estimated centers are given."
slug: /commands/estimatepeaksizes
---

<div className="command-signature">

## <strong>EstimatePeakSizes</strong>  [/B=<em>baseWave</em> ] [/X=<em>xWave</em> ] [/E=<em>bothEdgesWave</em> ] <em>edgePct</em>, <em>maxWidth</em>, <em>box</em>, <em>npks</em>, <em>peakCentersWave</em>, <em>peakWave</em>, <em>peakAmplitudesWave</em>, <em>peakWidthsWave</em> {#estimatepeaksizes}

</div>

The EstimatePeakSizes operation estimates the amplitudes and widths of peaks whose estimated centers are given.

The EstimatePeakSizes operation is used primarily by the Igor Technical Note #20 and its variants.

### *Parameters* {#parameters}
*edgePct* is the percentage of peak height at which the edge is detected, relative to the baseline. It must be between 1 and 99, and is usually 50.

*maxWidth* is the maximum width that will be returned in *peakWidthsWave*, in X coordinates.

*box* is the number of peak values included in the sliding average when smoothing *peakWave* and *baseWave*. If you specify an even number, the next-higher odd number is used.

*npks* is the number of peaks whose sizes are to be estimated. It must be at least 1.

*peakCentersWave* must contain the point numbers of the centers of the peaks and have a length of at least *npks*. The peak sizes are estimated by starting the search for the peak edges from these peak centers. The i-th peak center must be stored in *peakCentersWave*[i] where i ranges from 0 to *npks*-1. The peak center values in *peakCentersWave* must be monotonically increasing or decreasing.

*peakWave* is the input wave containing the peaks.

*peakAmplitudesWave* is an output wave that will contain the baseline-corrected peak amplitudes of the peaks. It must have a length of at least *npks*. The i-th peak amplitude is stored in *peakAmplitudesWave*[i].

*peakWidthsWave* is an output wave that will contain the widths of the peaks in X coordinates. It must have a length of at least *npks*. The i-th peak width is stored in *peakWidthsWave*[i].

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *baseWave*</span> | *baseWave* is subtracted from *peakWave* to compute the derived data which is searched for edges. It must be the same length as *peakWave*. |
| <span class="table-cell-nowrap">/E = *bothEdgesWave*</span> | *bothEdgesWave* specifies an already-existing output wave. It must have a length of at least *npks*\*2. The point coordinates of the i-th peak edges are stored in *bothEdgesWave*[i\*2] and *bothEdgesWave*[i\*2+1]. |
|  | If the X values increase with point number, *bothEdgesWave*[i\*2] will be greater than *bothEdgesWave*[i\*2+1], which may defy expectations. |
| <span class="table-cell-nowrap">/X = *xWave*</span> | *xWave* supplies the X coordinates for the corresponding points in *peakWave* and *baseWave*. It must be of the same length as *peakWave* and must be monotonically increasing or decreasing. |

### *See Also* {#see-also}
[FindPeak](/igorpro/commands/findpeak.md)