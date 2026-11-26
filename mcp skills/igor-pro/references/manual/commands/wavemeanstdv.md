---
description: "The WaveMeanStdv operation calculates the standard deviation of the means for the specified bin distribution saving the result in the wave W_MeanStdv."
slug: /commands/wavemeanstdv
---

<div className="command-signature">

## <strong>WaveMeanStdv</strong>  <em>srcWave</em>  <em>binSizeWave</em> {#wavemeanstdv}

</div>

The WaveMeanStdv operation calculates the standard deviation of the means for the specified bin distribution saving the result in the wave W_MeanStdv.

For each entry in *binSizeWave*, *srcWave*  is divided into the specified number of bins. The values in each bin are averaged and then the mean and standard deviation of the averages (among all bins) are calculated. The value of the standard deviation of the bin averages divided by the mean is then stored in W_MeanStdv corresponding to the bin size entry in *binSizeWave*.

All entries in *binSizeWave*  must be positive integers.

### *Details* {#details}
When the number of points in *srcWave*  does not divide evenly into the bin size entry from *binSizeWave*, the last bin will have a smaller number of data points. In order not to skew the results the values corresponding to the last bin will be dropped. If your data set is small compared to the bin size you might want to pad *srcWave*  with additional values (e.g., duplicate values from the beginning of the wave).

This operation does not support NaNs. If you get a NaN as an entry in the output wave then there is either a NaN in *srcWave*  or something is wrong with the calculation for that entry.