---
description: "The StatsStudentCDF function returns the Student (uniform) cumulative distribution function."
slug: /commands/statsstudentcdf
---

<div className="command-signature">

## <strong>StatsStudentCDF</strong> (<em>t</em>, <em>n</em>) {#statsstudentcdf}

</div>

The StatsStudentCDF function returns the Student (uniform) cumulative distribution function.

$$
F(t, n)=\left\{\begin{array}{ll}
\displaystyle \frac{1}{2}\left\{1+I\left(\frac{n}{2}, \frac{1}{2} ; 1\right)-I\left(\frac{n}{2}, \frac{1}{2} ; \frac{n}{n+t^{2}}\right)\right\} & t>0 \\
\\
\displaystyle \frac{1}{2}\left\{1+I\left(\frac{n}{2}, \frac{1}{2} ; \frac{n}{n+t^{2}}\right)-I\left(\frac{n}{2}, \frac{1}{2} ; 1\right)\right\} & t<0 \\
\\
\displaystyle \frac{1}{2} & t=0 .
\end{array}\right.
$$

where *n* >0 is the degrees of freedom and  is the incomplete beta function [betai](/igorpro/commands/betai.md).

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsStudentPDF](/igorpro/commands/statsstudentpdf.md), [StatsInvStudentCDF](/igorpro/commands/statsinvstudentcdf.md)