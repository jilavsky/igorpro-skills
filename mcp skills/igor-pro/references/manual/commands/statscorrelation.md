---
description: "The StatsCorrelation function computes Pearson's correlation coefficient between two real valued arrays of data of the same length."
slug: /commands/statscorrelation
---

<div className="command-signature">

## <strong>StatsCorrelation</strong> (<em>waveA</em> [, <em>waveB</em>]) {#statscorrelation}

</div>

The StatsCorrelation function computes Pearson's correlation coefficient between two real valued arrays of data of the same length. Pearson r is give by:

$$
r=\frac{\displaystyle \sum_{i=0}^{n-1}({ waveA } [i]-A)({ waveB } [i]-B)}{\sqrt{\displaystyle \sum_{i=0}^{n-1}({ waveA }[i]-A)^{2} \sum_{i=0}^{n-1}({ waveB }[i]-B)^{2}}}
$$

Here *A* is the average of the elements in *waveA*, *B* is the average of the elements of *waveB* and the sum is over all wave elements.

### *Details* {#details}
If you use both *waveA* and *waveB* then the two waves must have the same number of points but they could be of different number type. If you use only the *waveA* parameter then *waveA* must be a 2D wave. In this case StatsCorrelation will return 0 and create a 2D wave M_Pearson where the (*i*,*j* ) element is Pearson's r corresponding to columns *i* and *j*.

Fisher's z transformation converts Person's r to a normally distributed variable *z*:

$$
\displaystyle z=\frac{1}{2} \ln \left(\frac{1+r}{1-r}\right),
$$

with a standard error

$$
\displaystyle \sigma_{z}=\frac{1}{\sqrt{n-3}} .
$$

You can convert between the two representations using the following functions:


```igor
Function pearsonToFisher(inr)
	Variable inr
	return 0.5*(ln(1+inr)-ln(1-inr))
End

Function fisherToPearson(inz)
	Variable inz
	return tanh(inz)
End
```

### *See Also* {#see-also}
[Correlate](/igorpro/commands/correlate.md), [StatsLinearCorrelationTest](/igorpro/commands/statslinearcorrelationtest.md), [StatsCircularCorrelationTest](/igorpro/commands/statscircularcorrelationtest.md)