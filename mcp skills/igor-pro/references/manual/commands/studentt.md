---
description: "This function is deprecated. New code should use the more accurate StatsInvStudentCDF."
slug: /commands/studentt
---

<div className="command-signature">

## <strong>StudentT</strong> (<em>Prob</em>, <em>DegFree</em>) {#studentt}

</div>

:::warning
This function is deprecated. New code should use the more accurate [StatsInvStudentCDF](/igorpro/commands/statsinvstudentcdf.md).
:::

The StudentT function returns the t value corresponding to an area *Prob* under the Student's T distribution from -t to t for DegFree degrees of freedom.

Note that this is a "bi-tail" result, which is what is usually desired. Tabulated values of the Student's T distribution are commonly the one-sided result.

StudentT calculates confidence intervals from standard deviations for normally-distributed statistics. For instance, you can use it to calculate a confidence interval for the coefficients from a curve fit:


```igor
Make/O/N=20 Data=0.5*x+2+gnoise(1)	// line with Gaussian noise
Display Data
CurveFit line Data /D
Print "intercept = ", W_coef[0], "±", W_sigma[0]*StudentT(0.95, V_npnts-2)
Print "slope = ", W_coef[1], "±", W_sigma[1]*StudentT(0.95, V_npnts-2)
```

### *See Also* {#see-also}
[StatsStudentCDF](/igorpro/commands/statsstudentcdf.md), [StatsStudentPDF](/igorpro/commands/statsstudentpdf.md), [StatsInvStudentCDF](/igorpro/commands/statsinvstudentcdf.md)