---
description: "The StatsStudentPDF function returns the Student (uniform) probability distribution function."
slug: /commands/statsstudentpdf
---

<div className="command-signature">

## <strong>StatsStudentPDF</strong> (<em>t</em>, <em>n</em>) {#statsstudentpdf}

</div>

The StatsStudentPDF function returns the Student (uniform) probability distribution function.

$$
f(t, n)=\frac{\left(\displaystyle \frac{n}{n+t^{2}}\right)^{(n+1) / 2}}{\displaystyle \sqrt{n} B\left(\frac{n}{2}, \frac{1}{2}\right)} .
$$

where *n* >0 is the degrees of freedom and *B* () is the [beta](/igorpro/commands/beta.md) function.

### *See Also* {#see-also}
[Statistical Analysis](/igorpro/analysis/statistics.md), [StatsStudentCDF](/igorpro/commands/statsstudentcdf.md), [StatsInvStudentCDF](/igorpro/commands/statsinvstudentcdf.md)