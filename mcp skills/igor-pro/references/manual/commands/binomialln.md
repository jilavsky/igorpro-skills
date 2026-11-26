---
description: "The binomialln function returns the natural log of the binomial coefficient for a and b."
slug: /commands/binomialln
---

<div className="command-signature">

## <strong>binomialln</strong> (<em>a</em>, <em>b</em>) {#binomialln}

</div>

The binomialln function returns the natural log of the binomial coefficient for *a* and *b*.

$$
\displaystyle \text { Binomialln(a, b)=ln(a!)-ln(b!)-ln((a-b)!) }
$$

If you encounter overflow when the arguments are large you can use [APMath](/igorpro/commands/apmath.md) or [Binomialln](/igorpro/commands/binomialln.md). For example:


```igor
Print binomial(2800,333)
  inf
APMath/V result = binomial(2800,333)
  9.00198266850214464998502850373044733821917603122330E+441
Print/D binomialln(2800,333)
  1017.63747085995
APMath/V result = log(binomial(2800,333))
  1.01763747085994889343514158007045064106357813268781E+3
```

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [binomial](/igorpro/commands/binomial.md), [StatsBinomialCDF](/igorpro/commands/statsbinomialcdf.md), [StatsBinomialPDF](/igorpro/commands/statsbinomialpdf.md), [StatsInvBinomialCDF](/igorpro/commands/statsinvbinomialcdf.md)