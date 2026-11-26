---
description: "This function is deprecated. New code should use the more accurate StatsStudentCDF."
slug: /commands/studenta
---

<div className="command-signature">

## <strong>StudentA</strong> (<em>t</em>, <em>DegFree</em>) {#studenta}

</div>

:::warning
This function is deprecated. New code should use the more accurate [StatsStudentCDF](/igorpro/commands/statsstudentcdf.md).
:::

The StudentA function returns the area from -*t* to *t* under the Student's T distribution having *DegFree* degrees of freedom. That is, it returns the probability that a random sample from Student's T is between -t and t.

Note that this is the *bi-tail* result. That is, it gives the area from -t to t, rather than the cumulative area from -∞ to t. It is this latter number that is commonly tabulated -- StudentA returns the probability 1-α where the area from -∞ to t is the probability 1-α/2.

StudentA tests whether a normally-distributed statistic is significantly different from a certain value. You could use it to test whether an intercept from a line fit is significantly different from zero:


```igor
Make/O/N=20 Data=0.5*x+2+gnoise(1)	// line with Gaussian noise
Display Data
CurveFit line Data /D
Print "Prob = ", StudentA(W_coef[0]/W_sigma[0], V_npnts-2)
```

Because the noise is random, the results will differ slightly each time this is tried. When we did it, the result was:


```igor
Prob =   0.999898
```

which indicates that the intercept of the line fit was different from zero with 99.99 per cent probability.

### *See Also* {#see-also}
[StatsStudentCDF](/igorpro/commands/statsstudentcdf.md), [StatsStudentPDF](/igorpro/commands/statsstudentpdf.md), [StatsInvStudentCDF](/igorpro/commands/statsinvstudentcdf.md)