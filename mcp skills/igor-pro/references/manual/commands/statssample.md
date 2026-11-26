---
description: "StatsSample creates a random, non-repeating sample from srcWave. It samples srcWave by drawing without replacement numPoints values from srcWave and storing…"
slug: /commands/statssample
---

<div className="command-signature">

## <strong>StatsSample</strong>  /N=<em>numPoints</em> [ /CMPL /MC /MR /Z ] <em>srcWave</em> {#statssample}

</div>

StatsSample creates a random, non-repeating sample from *srcWave*.

It samples *srcWave* by drawing without replacement *numPoints* values from *srcWave* and storing them in the output wave W_Sampled or M_Sampled if /MC or /MR are used.

The /N flag is required.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ACMB</span> | Creates a wave containing all unique combinations of *numPoints* samples from *srcWave*. Here *srcWave* is a 1D numeric wave containing more than *numPoints* elements. The results are stored in the wave M_Combinations in the current data folder. Each row in M_Combinations corresponds to a unique combination of *numPoints* samples.  If *srcWave* consists of *ns* points and /N=*numPoints*, the output wave has dimensions (binomial(*ns*,*numPoints*), *numPoints*). |
|  | Note that the operation does not test the values of the samples for uniqueness. |
|  | Added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/CMPL</span> | Stores all data elements from *srcWave* that were excluded from the random sample in the wave W_CompWave or M_CompWave in the current data folder. /CMPL was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">/DSTB = *bWave*</span> | Specify the destination wave for unique combinations of samples (/ACMB).  If you do not use this flag, the operation saves the samples in the wave M_Combinations in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTC = *cWave*</span> | Specify the destination wave for the complementary set, i.e., all elements that were excluded from the sample (see /CMPL).  If you do not use this flag, the operation saves the complementary samples in the wave W_CompWave or M_CompWave in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTS = *sWave*</span> | Specify the destination wave for unique samples from *srcWave*.  If you do not use this flag, the operation saves the samples in the wave W_Sampled or M_Sampled in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all user-specified destination waves as free waves. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/MC</span> | Use /MC (multi-column) to randomly sample full rows from *srcWave*, i.e., the output consists of all columns of each selected row. /MC and /MR are mutually exclusive flags. |
| <span class="table-cell-nowrap">/MR</span> | Use /MR (multi-row) to randomly sample full columns from *srcWave*, i.e., the output consists of all rows of each of the selected columns. /MC and /MR are mutually exclusive flags. |
| <span class="table-cell-nowrap">/N = *numPoints*</span> | Specifies the number of points sampled from *srcWave*. When combined with /MC, *numPoints* is the number of sampled rows and when combined with /MR, it is the number of sampled columns. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. |

### *Details* {#details}
If you omit /MC and /MR, the output is a 1D wave named W_Sampled where the samples are chosen from *srcWave* without regard to its dimensionality.

If you use either /MC or /MR the output is a 2D wave named M_Sampled which will have either the same number of columns (/MC) as *srcWave* or the same number of rows (/MR) as *srcWave.*

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsResample](/igorpro/commands/statsresample.md)