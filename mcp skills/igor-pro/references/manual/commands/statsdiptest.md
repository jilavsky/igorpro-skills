---
description: "The StatsDIPTest operation performs Hartigan test for unimodality. The input to the operation srcWave is any real numeric wave."
slug: /commands/statsdiptest
---

<div className="command-signature">

## <strong>StatsDIPTest</strong>  [/Z] <em>srcWave</em> {#statsdiptest}

</div>

The StatsDIPTest operation performs Hartigan test for unimodality.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *dipWave*</span> | Specify the destination wave for the Hartigan Dip test results.  The destination wave contains three values: the Min, Max and DIP. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the user-specified destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Z</span> | Ignores errors. V_flag will be set to -1 for any error and to zero otherwise. |

### *Details* {#details}
The input to the operation *srcWave*  is any real numeric wave. Outputs are: V_Value contains the dip statistic; V_min is the lower end of the modal interval; and V_max is the higher end of the modal interval. Percentage points or critical values for the dip statistic can be obtained from simulations using an identical sample size as in this example:


```igor
Function getCriticalValue(iterations,sampleSize,alpha)
	Variable iterations,sampleSize,alpha

	Make/O/N=(sampleSize) dataWave
	Make/O/N=(iterations)  dipResults

	MultiThread dipResults=getIndexedResults(p,sampleSize)

	Histogram/P/B=4 dipResults              // Compute the PDF.
	Wave W_Histogram
	Integrate/METH=1 W_Histogram/D=W_INT    // Compute the CDF.
	Findlevel/Q  W_int,(1-alpha)            // Find the critical value.
	return V_LevelX
End

ThreadSafe Function getIndexedResults(variable id,variable sampleSize)

	Make/FREE/n=(sampleSize) data=enoise(100)
	StatsDipTest data
	return V_Value
End
```

### *References* {#references}
Hartigan, P. M., Computation of the Dip Statistic to Test for Unimodality, *Applied Statistics*, *34*, 320-325, 1985.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md)